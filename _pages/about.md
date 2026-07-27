---
permalink: /
title: "Controls & Robotics Researcher"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
  - /research/
  - /research.html
---

PhD in Control Theory, UW Aeronautics & Astronautics · seeking industry robotics research roles
{: .page__lead}

I'm currently **open to industry robotics research roles** in navigation, estimation, and autonomy. Reach out at [adityad@uw.edu](mailto:adityad@uw.edu) or on [LinkedIn](https://www.linkedin.com/in/aditya-deole-26aab3101).
{: .notice--info}

[<i class="fas fa-file-pdf"></i> Download my CV](./files/Aditya_Deole_CV.pdf){: .btn .btn--info .btn--large}

Hi, I'm Aditya. I received my PhD in Control Theory from the Dept. of Aeronautics & Astronautics at the University of Washington in June 2025, advised by Prof. Mesbahi. I work on control and estimation for systems whose feedback loop runs through an imperfect, learning-based sensor — making autonomy safe and reliable when it depends on ML-driven perception.

I am currently a postdoctoral researcher at UW's Steinmetz Lab and NERD Lab, building real-time closed-loop controllers for cortical population dynamics. My motivation for control theory comes from hardware: I have worked on autonomous navigation for ground and aerial robots, and supervised robotics projects at the [RAIN Lab](https://depts.washington.edu/uwrainlab/).

## Selected Work

### Closed-loop control of neural systems

*Current work — Steinmetz Lab and NERD Lab, UW.*

I build real-time feedback controllers that read population neural activity and steer it toward a target. The loop uses widefield calcium imaging as an online state readout and drives a steerable stimulation laser as a function of the animal's brain state, with quantified end-to-end latency.

The control-theoretic core is system identification: fitting low-order dynamical models to stimulation-evoked cortical responses, so a controller can be designed rather than hand-tuned. On the µECoG side, I use reachability and controllability analysis to determine which cortical nodes a given stimulation site can actually drive — the same questions that govern where to sense and steer in a trajectory problem, asked of a brain instead of a spacecraft.

{% include video src="/videos/neural-closed-loop.mp4" poster="/videos/neural-closed-loop.jpg" controls="true" alt="Closed-loop optogenetic control dashboard showing widefield cortical activity, laser command, and tracking error across 100 trials" caption="Real-time closed-loop optogenetic control. A PI controller drives widefield ΔF/F activity in a target ROI to a −5% set-point; across 100 trials, closed-loop (green) tracks the reference and reduces trial-to-trial variance relative to open-loop (red)." %}

### Estimation-aware trajectory planning

[Paper (JGCD 2025)](https://arxiv.org/abs/2501.09192) · [Code and videos](https://github.com/Rainlabuw/Obs_aware_opt)

A neural network deployed in a physical environment often behaves like a *state-dependent sensor* — a keypoint network's uncertainty, for instance, depends on the illumination it happens to be in. If uncertainty depends on state, the trajectory itself becomes a design variable for estimation quality: you can plan a path that makes the system easier to estimate while still completing the task.

I model the ML uncertainty as bounded sets, define an observability condition on the resulting output tubes, and solve the optimal control problem with sequential convex programming.

{% include video src="/videos/estimation-aware-planning.mp4" poster="/videos/estimation-aware-planning.jpg" alt="Side-by-side comparison of nominal and estimation-aware trajectory planning for a satellite rendezvous" caption="Nominal planning takes the shortest path; estimation-aware planning takes the *most observable* one, reducing state variance during rendezvous." %}

With a network of agents the setup improves further, by quantifying the directions in which information is missing and solving the problem sequentially across agents.

{% include video src="/videos/multiagent-estimation-aware.mp4" poster="/videos/multiagent-estimation-aware.jpg" alt="Three agents planning complementary observation paths around a target, with the illumination each one sees" caption="Multi-agent case: each agent takes a complementary path, covering the directions the others leave unobserved — the bottom row shows the illumination conditions each one is exploiting." %}

### Robotics at the RAIN Lab

I built and supervised educational hardware testbeds for aerial and ground robots, integrating navigation with trajectory-optimization layers.

{% include video src="/videos/quadrotor-flight.mp4" poster="/videos/quadrotor-flight.jpg" alt="Quadrotor performing a multi-point flight test in a netted motion-capture lab" caption="Multi-point flight test of the in-house quadrotor built for trajectory-planning experiments." %}

- [ROS2 ground-robot platform for testing trajectory optimization](https://github.com/Rainlabuw/Johnny_demos)
- An indoor positioning-and-navigation system built in-house for mobile robots
- Crazyflie 2 platforms for trajectory optimization

{% include figure image_path="./images/hardware/johnny-ground-robots.jpg" alt="Two small differential-drive ground robots with motion-capture marker plates" caption="\"Johnny\" ground robots — the RAIN Lab's educational testbed." %}

{% include figure image_path="./images/sim/spacecraft-sim-unreal.png" alt="Unreal Engine simulation of a satellite in Earth orbit with a chaser camera view" caption="Unreal Engine environment I built for vision-based satellite rendezvous, coupling a custom dynamics engine to the perception pipeline." %}

## Selected Publications

- **A. Deole**, M. Mesbahi. "[Estimation-Aware Trajectory Optimization with Set-Valued Measurement Uncertainties](https://arxiv.org/abs/2501.09192)." *Journal of Guidance, Control, and Dynamics*, 2025.
- **A. Deole**, et al. "[MPC-based Estimation-Aware Trajectory Generation for Uncontrolled Satellite Pose Tracking](https://doi.org/10.2514/6.2024-0947)." AIAA SciTech Forum, 2024.
- **A. Deole**, et al. "[Multi-Agent Passivity-based Control for Perception-based Guidance](https://doi.org/10.2514/6.2023-2156)." AIAA SciTech Forum, 2023.

[See all publications →](./publications/)

## News

### Poster presentation at NeuroAI 2025

{% include figure image_path="./images/neuroai-poster-2025.jpg" alt="Aditya presenting a research poster at NeuroAI 2025" caption="Presenting *Towards Data-driven Feedback for Cortical Activity* at NeuroAI 2025." %}

### Defended my PhD thesis — June 2025

{% include figure image_path="./images/adityaphd.jpeg" url="https://www.linkedin.com/posts/uwaeroastro_check-out-aditya-deoles-research-and-phd-activity-7336542345682698240-2bHG?utm_source=share&utm_medium=member_desktop&rcm=ACoAABn4GLIBIY-l8NiSMJXGW03Ryx5HSTMDBKc" alt="Aditya in doctoral regalia after his PhD defense" caption="PhD defense, June 2025 — click for the UW Aero & Astro post." %}

### UW Graduate Showcase 2025

{% include figure image_path="./images/adityasharc.jpeg" url="https://www.linkedin.com/posts/uwaeroastro_spotlight-on-aditya-deoles-research-presented-activity-7345511465841266688-uCPS?utm_source=share&utm_medium=member_desktop&rcm=ACoAABn4GLIBIY-l8NiSMJXGW03Ryx5HSTMDBKc" alt="Aditya presenting research at the UW Graduate Showcase 2025" caption="Presenting at the UW Graduate Showcase 2025 — click for the UW Aero & Astro post." %}
