---
permalink: /
title: "Control Theory for Neural Systems"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
  - /research/
  - /research.html
---

Aerospace controls PhD turned computational neuroscientist · seeking research scientist roles
{: .page__lead}

I'm currently **open to research scientist positions** in computational neuroscience, neural engineering, and control of complex dynamical systems. Reach out at [aditya.158@gmail.com](mailto:aditya.158@gmail.com) or on [LinkedIn](https://www.linkedin.com/in/aditya-deole-26aab3101).
{: .notice--info}

[<i class="fas fa-file-pdf"></i> Download my CV](./files/Aditya_Deole_CV.pdf){: .btn .btn--info .btn--large}

Hi, I'm Aditya. I'm a control theorist working on closed-loop control of neural systems. I design real-time feedback controllers and estimators that read population neural activity and steer it toward physiologically meaningful targets — across optogenetic and electrical stimulation, and across recording modalities from widefield imaging to µECoG.

I received my PhD in Control Theory from the Dept. of Aeronautics & Astronautics at the University of Washington in June 2025, advised by Prof. Mesbahi, where I worked on robust control and estimation for spacecraft guided by machine-learned perception. The questions turn out to transfer directly: controllability, observability, and robust synthesis under uncertainty are the same tools whether the plant is a spacecraft with an unreliable sensor or a cortical population you can only partially observe and only partially drive. I now bring that foundation to the design of neural interfaces and stimulation therapies, as a postdoctoral researcher at UW's Steinmetz Lab and NERD Lab.

My research interests include:

- Closed-loop control of neural population dynamics
- System identification for high-dimensional, partially-observed biological systems
- Controllability and reachability analysis for neural stimulation
- Estimation-aware planning and robust control under set-valued uncertainty

## Selected Work

### Closed-loop control of neural systems

*Current work — Steinmetz Lab and NERD Lab, UW.* Presented at **NeuroAI 2026**, Allen Institute, Seattle, with Anna Li, Eric Shea-Brown, Mehran Mesbahi and Nick Steinmetz. [Slides (PDF)](./files/Deole_NeuroAI2026_slides.pdf)

Cortex-wide activity can be measured, and it can be driven. That makes it a plant — something you can wrap a controller around and ask the usual questions of: what can this input actually reach, how well can this output be tracked, and what does the answer tell you about the system underneath?

**Measure, and act.** Widefield calcium imaging reads activity across the dorsal cortex at 35 Hz, while a steerable laser delivers spatially targeted optogenetic stimulation to a chosen region. The stimulus lands where it is aimed and spreads from there.

{% include video src="/videos/cortical-response.mp4" poster="/videos/cortical-response.jpg" alt="Widefield cortical activity map showing a localized response spreading from the optogenetic stimulation site while the laser is on" caption="Cortex-wide ΔF/F during targeted optogenetic stimulation. The response is centred on the stimulation site (ringed) and spreads from there." %}

**The response is graded, so there is a plant to identify.** Sweeping laser power produces a systematic, repeatable change in the cortical response — the basis for treating the trial-averaged dynamics as a low-order LTI system, cross-validated across trials.

{% include video src="/videos/dose-response.mp4" poster="/videos/dose-response.jpg" alt="Cortical response maps as optogenetic laser power increases from 0.4 to 1.8 milliwatts" caption="Dose-response: as laser power sweeps from 0.40 to 1.80 mW, the evoked response grows systematically — an input-output map you can fit a model to." %}

**Close the loop.** PI output feedback on top of a calibrated feedforward term, running in real time, with gains chosen by optimizing over a cost map rather than tuned by hand. The loop holds the target region at a −5% ΔF/F set-point, improves tracking over open loop, and reduces trial-to-trial variability across sessions.

{% include video src="/videos/neural-closed-loop.mp4" poster="/videos/neural-closed-loop.jpg" controls="true" alt="Closed-loop optogenetic control dashboard showing widefield cortical activity, laser command, and tracking error across 100 trials" caption="Real-time closed-loop control. A PI controller drives ΔF/F in the target ROI to a −5% set-point; across 100 trials, closed loop (green) tracks the reference and reduces trial-to-trial variance relative to open loop (red)." %}

**Then steer it.** The same loop against a moving reference rather than a fixed one. Feedback corrects the amplitude error; adding preview of where the reference is going corrects the phase lag that feedback alone leaves behind.

{% include video src="/videos/moving-reference.mp4" poster="/videos/moving-reference.jpg" controls="true" alt="Feedforward optogenetic control dashboard tracking a moving reference across 199 trials" caption="Tracking a moving reference. A controller with model knowledge can preview where the reference is heading, which recovers the phase that pure feedback loses to plant lag." %}

**What the controller reveals.** Closed-loop performance is itself a measurement. A wrong internal model shows up immediately as tracking error, which makes the controller an instrument for probing the system rather than only a means of driving it: brain state changes how controllable cortex is, with movement improving controllability and synchronization degrading it.

### Estimation-aware planning under set-valued uncertainty

*PhD work — RAIN Lab, UW Aeronautics & Astronautics.*

[Paper (JGCD 2025)](https://arxiv.org/abs/2501.09192) · [Code and videos](https://github.com/Rainlabuw/Obs_aware_opt)

This is where the observability machinery I now apply to neural systems came from. A neural network deployed in a physical environment often behaves like a *state-dependent sensor* — a keypoint network's uncertainty, for instance, depends on the illumination it happens to be in. If uncertainty depends on state, the trajectory itself becomes a design variable for estimation quality: you can plan a path that makes the system easier to estimate while still completing the task.

I model the ML uncertainty as bounded sets, define an observability condition on the resulting output tubes, and solve the optimal control problem with sequential convex programming.

{% include video src="/videos/estimation-aware-planning.mp4" poster="/videos/estimation-aware-planning.jpg" alt="Side-by-side comparison of nominal and estimation-aware trajectory planning for a satellite rendezvous" caption="Nominal planning takes the shortest path; estimation-aware planning takes the *most observable* one, reducing state variance during rendezvous." %}

With a network of agents the setup improves further, by quantifying the directions in which information is missing and solving the problem sequentially across agents.

{% include video src="/videos/multiagent-estimation-aware.mp4" poster="/videos/multiagent-estimation-aware.jpg" alt="Three agents planning complementary observation paths around a target, with the illumination each one sees" caption="Multi-agent case: each agent takes a complementary path, covering the directions the others leave unobserved — the bottom row shows the illumination conditions each one is exploiting." %}

### Experimental systems and hardware

Alongside the theory, I build the systems the theory runs on: real-time, multi-threaded image- and signal-processing pipelines in Python for online neural feedback, and before that a simulation and robotics stack for testing controllers against real sensor behaviour.

{% include video src="/videos/quadrotor-flight.mp4" poster="/videos/quadrotor-flight.jpg" alt="Quadrotor performing a multi-point flight test in a netted motion-capture lab" caption="Multi-point flight test of an in-house quadrotor built for trajectory-planning experiments at the RAIN Lab." %}

{% include figure image_path="./images/sim/spacecraft-sim-unreal.png" alt="Unreal Engine simulation of a satellite in Earth orbit with a chaser camera view" caption="Unreal Engine environment I built for vision-based rendezvous, coupling a custom dynamics engine to a learned perception pipeline." %}

I also built and supervised educational hardware testbeds for aerial and ground robots at the [RAIN Lab](https://depts.washington.edu/uwrainlab/), including a [ROS2 ground-robot platform](https://github.com/Rainlabuw/Johnny_demos) for testing trajectory optimization and an in-house indoor positioning system.

## Selected Publications

- **A. Deole**, N. Steinmetz, et al. "Towards Data-driven Feedback for Cortical Activity." *NeuroAI*, 2025.
- Z. Lu, **A. Deole**, et al. "Benchmarking Probabilistic Time Series Forecasting Models on Neural Activity." *NeurIPS 2025 Workshop*.
- **A. Deole**, M. Mesbahi. "[Estimation-Aware Trajectory Optimization with Set-Valued Measurement Uncertainties](https://arxiv.org/abs/2501.09192)." *Journal of Guidance, Control, and Dynamics*, 2025.

[See all publications →](./publications/)

## News

### Talk at NeuroAI 2026, Allen Institute — August 2026

Presented *Closed-loop control of mesoscale cortical activity* at NeuroAI in Seattle, hosted at the Allen Institute. [Slides (PDF)](./files/Deole_NeuroAI2026_slides.pdf)

### Poster presentation at NeuroAI 2025

{% include figure image_path="./images/neuroai-poster-2025.jpg" alt="Aditya presenting a research poster at NeuroAI 2025" caption="Presenting *Towards Data-driven Feedback for Cortical Activity* at NeuroAI 2025." %}

### Defended my PhD thesis — June 2025

{% include figure image_path="./images/adityaphd.jpeg" url="https://www.linkedin.com/posts/uwaeroastro_check-out-aditya-deoles-research-and-phd-activity-7336542345682698240-2bHG?utm_source=share&utm_medium=member_desktop&rcm=ACoAABn4GLIBIY-l8NiSMJXGW03Ryx5HSTMDBKc" alt="Aditya in doctoral regalia after his PhD defense" caption="PhD defense, June 2025 — click for the UW Aero & Astro post." %}

### UW Graduate Showcase 2025

{% include figure image_path="./images/adityasharc.jpeg" url="https://www.linkedin.com/posts/uwaeroastro_spotlight-on-aditya-deoles-research-presented-activity-7345511465841266688-uCPS?utm_source=share&utm_medium=member_desktop&rcm=ACoAABn4GLIBIY-l8NiSMJXGW03Ryx5HSTMDBKc" alt="Aditya presenting research at the UW Graduate Showcase 2025" caption="Presenting at the UW Graduate Showcase 2025 — click for the UW Aero & Astro post." %}
