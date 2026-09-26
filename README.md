# adityadeole.com

Personal academic site for Aditya Deole. Jekyll, built on a fork of
[AcademicPages](https://github.com/academicpages/academicpages.github.io)
(itself a fork of Minimal Mistakes).

| | |
|---|---|
| **Live site** | https://adityadeole.com |
| **Host** | GitHub Pages, from this repo |
| **Build branch** | `master` — **pushing to it publishes immediately** |
| **Domain** | Registered at Cloudflare (registrar + DNS only, records unproxied) |
| **Old URL** | `smartadi.github.io/adityad.github.io` — still redirects here |

There is no deploy step and no staging environment. GitHub rebuilds the site
about a minute after any push to `master`, and whatever is on `master` is what
the public sees. Preview locally before pushing.

---

## Working on a new machine

Everything below is a one-time setup. macOS instructions; on Linux use your
package manager instead of Homebrew.

### 1. Clone

```bash
git clone https://github.com/smartadi/adityad.github.io.git
cd adityad.github.io
```

### 2. Install Ruby 3.2

The system Ruby on macOS is too old (2.6). Match the version GitHub Pages
uses:

```bash
brew install ruby@3.2
```

Ruby 3.2 does not go on your `PATH` automatically. Either prefix each session
with the export below, or add it to your `~/.zshrc` permanently:

```bash
export PATH="/opt/homebrew/opt/ruby@3.2/bin:$PATH"
```

### 3. Install the gems

```bash
bundle config set --local path vendor/bundle && bundle install
```

The `path` setting keeps gems inside `vendor/bundle` in the project rather
than installing them system-wide. It writes `.bundle/config`, which is
gitignored, so this step is needed on every new machine.

`Gemfile.lock` is also gitignored (inherited from the upstream template).
Versions therefore resolve fresh on each machine, which is usually fine since
`github-pages` pins the whole toolchain — but it means a build that works on
one machine can in principle differ on another.

### 4. Install ffmpeg, if you will touch video

```bash
brew install ffmpeg
```

Only needed for the media workflow below. Skip it for text-only edits.

---

## Everyday workflow

### Preview locally

```bash
export PATH="/opt/homebrew/opt/ruby@3.2/bin:$PATH" && bundle exec jekyll serve -w --config _config.yml,_config_docker.yml
```

Then open http://localhost:4000.

- `-w` watches for changes and rebuilds automatically.
- `_config_docker.yml` blanks `url` so local links resolve against
  `localhost` instead of the live domain. Always include it locally.
- **Jekyll does not reload `_config.yml`.** Restart the server after editing
  it, or your changes silently will not appear.

The repo contains a `docker-compose.yaml` from the upstream template. It is
unused — the native Ruby setup above is what this site is developed with.

### Publish

```bash
git add -A && git commit -m "your message" && git push origin master
```

Wait roughly a minute, then reload the live site. If it does not update,
check the Actions tab on GitHub for a failed build.

---

## Things that will bite you

These are all real problems that have already happened once.

### Use `absolute_url`, never `relative_url`

Asset URLs are built from `site.url`. `relative_url` produces root-relative
paths that work perfectly on `localhost` and **404 in production**. This class
of bug is invisible locally. If you add an include that emits a URL, use
`absolute_url`.

A useful consequence: because everything uses `absolute_url`, moving the site
to a new domain is a one-line change to `url` in `_config.yml`.

### Includes have no file extension

`{% include figure %}` looks for `_includes/figure`, not `figure.html`.
Adding the extension produces a "Could not locate the included file" build
error.

Custom includes in this repo:

| Include | Purpose |
|---|---|
| `figure` | Image with caption. Takes `image_path`, `alt`, `caption`, optional `url` to make it clickable. |
| `video` | Muted autoplay looping video. Takes `src`, `poster`, `alt`, `caption`, optional `controls="true"` for longer or detail-heavy clips. |

### Liquid runs inside HTML comments

`<!-- {% include foo %} -->` still executes the include; the comment only
hides the output from the browser. To genuinely disable a block, use
`{% comment %} ... {% endcomment %}`.

This is why the Publications page rendered empty for a long time while
placeholder text sat in the page source.

### All custom CSS goes in one file

`_sass/_custom.scss`, imported **last** in `assets/css/main.scss` so it
overrides the theme cleanly. Do not edit the theme's own partials under
`_sass/theme/` — changes there are hard to reason about and get lost if the
theme is ever updated.

Use the theme's CSS custom properties (`--global-text-color`,
`--global-bg-color`, `--global-border-color`, and so on) rather than hardcoded
colours, so both light and dark modes stay consistent. Note that the theme's
dark palette sets `--global-fig-caption-color` to a dark grey that is
unreadable on its own dark background; `_custom.scss` already overrides this.

**Check both light and dark modes** after any style change — the toggle is in
the top navigation bar.

---

## Common edits

### Add a publication

Create a file in `_publications/` named `YYYY-MM-DD-short-slug.md`:

```yaml
---
title: "Paper Title"
collection: publications
category: conferences   # or: manuscripts (journal articles), books
permalink: /publication/YYYY-short-slug
date: YYYY-MM-DD
venue: 'Venue Name'
paperurl: 'https://doi.org/...'   # omit if none
citation: '<b>A. Deole</b>, et al. &quot;Title.&quot; <i>Venue</i>, YYYY.'
---
```

Category headings are defined under `publication_category` in `_config.yml`.
Entries sort by date, newest first.

### Add news or a homepage section

Everything on the homepage lives in `_pages/about.md`. It is ordinary
Markdown — add a `###` heading in the relevant place.

### Add a video

Never commit raw video or GIFs. Convert first:

```bash
ffmpeg -i input.mov -movflags +faststart -pix_fmt yuv420p -vf "scale=1280:-2" -c:v libx264 -crf 24 -preset slow -an videos/name.mp4
```

Then generate a poster frame so the page shows a still before playback:

```bash
ffmpeg -ss 3 -i videos/name.mp4 -vframes 1 -q:v 4 videos/name.jpg
```

Reference it with the `video` include:

```liquid
{% include video src="/videos/name.mp4" poster="/videos/name.jpg" alt="..." caption="..." %}
```

Check the poster is not a blank or title frame — adjust `-ss` if it is.

**Why convert:** GIFs are catastrophic for page weight. The clips on this site
were originally 6–10 MB GIFs each; as mp4 they are 180–750 KB, and they look
better. Use `-crf 26` to 28 for dense screen-recorded dashboards, 23 to 24 for
footage.

### Add images

Resize before committing. Photos straight off a phone are ~10 MB:

```bash
sips -Z 1600 -s format jpeg -s formatOptions 82 input.png --out images/name.jpg
```

Avoid spaces and parentheses in filenames — they break in URLs and have
already caused problems here.

---

## Limits to respect

| Limit | Value |
|---|---|
| Repo size | ~1 GB soft limit |
| Bandwidth | 100 GB/month soft limit |
| Per-file | 100 MB hard limit |

Long videos — gaming clips, full talk recordings — do **not** belong here.
Put them on YouTube and embed. The short research demos on this site are
fine because each is under 4 MB.

---

## Domain and DNS

Registered at Cloudflare. DNS records, all **unproxied** (grey cloud — the
proxy interferes with GitHub provisioning TLS certificates):

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153`, `.109.153`, `.110.153`, `.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` through `:8003::153` |
| CNAME | `www` | `smartadi.github.io` |

The `CNAME` file in the repo root tells GitHub which domain this repo serves.
Do not delete it — the site would revert to the github.io URL.

TLS is a Let's Encrypt certificate that GitHub provisions and renews
automatically.

### Moving to a different host later

The domain is independent of the host. To move to Cloudflare Pages, Netlify or
anywhere else: point DNS at the new host, update `url` in `_config.yml`, and
every existing link keeps working. Nothing else is tied to GitHub.

---

## Outstanding

- [ ] **Tick "Enforce HTTPS"** in
      [Settings → Pages](https://github.com/smartadi/adityad.github.io/settings/pages).
      Currently `http://adityadeole.com` serves over plain HTTP instead of
      redirecting. The old github.io URL was on the browser HSTS preload list
      and could not be reached insecurely; the custom domain gives that up
      until this is enabled.
- [ ] Verify the domain under Settings → Pages → Verified domains, to prevent
      anyone else claiming it on their own Pages site.
- [ ] Add links for the NeuroAI 2025 and NeurIPS 2025 workshop papers — they
      lead Selected Publications and are currently plain text.
- [ ] Set `description` and `og_image` in `_config.yml` so shared links render
      a preview card instead of a bare URL.
- [ ] Regenerate the CV PDF with the new domain printed on it.
- [ ] Teaching page: typo pass, and decide whether referees' names and emails
      should stay publicly listed.
