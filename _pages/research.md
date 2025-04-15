---
permalink: /research/
title: "Research"
author_profile: true
redirect_from: 
  - /re/
  - /research.html
---

## Photorealistic Simulation Design for Vision Based Navigation
For application of a ML based state estimator used for state feedback in navigation systems, a robust simulation environment needs to be designed. I have worked on robust control and trajectory design methods for such systems. To setup these problems, the simulation environment needs to encorporate realistic visuals and emulate realistic perception maps. The simulator needs to be modular enough to work with custom dynamic engines and ML algorithms that can process the image outputs. Finally a robust controller algorithm need to interact with the uncertain ML output and give the best course of action.

To facilitate this, I designed a modular sim in Unreal Engine which runs Python scripts to interact with a dynamics Engine usually written in MATLAB or python while a parallel script runs the ML perception algorithm. Ive tested this for space environments where satellite proximity operations are performed. The satellite is in a Low Earth orbit, trying to rendezvous with a uncontrolled spacecraft.

<img src="../images/sim/Screenshot%20(79).png" width="280" height="200"><img src="../images/sim/arch2.png" width="280" height="200">

Currently there are a few UE based sims available commercially, showing the importance of such a tool in research as well as in industry. Carla, Airsim etc are also built before this to solve similar problems. For research specific scenarios with custom enviroments, a custom sim needs to be built.

## Controller design for systems with ML based estimation : An Applied AI problem
I have been interested in investigating use of safe methods in satellite proximity applications where Ego spacecrafts use ML to identify their Targets. This was a problem setup investigated by my colleagues at Rain Lab and JPL. The main goal was to see which controller design would be robust in a scenario where uncertainty comes from ML-algorithms.

<img src="../images/funnel/state1.png" width="280" height="200">

### Funnel Synthesis
We investigated funnel synthesis methods developed by [Reynold et al](https://doi.org/10.2514/6.2021-0504) for the problem of following a nominal trajectory under the uncertain estimation. The uncertainties can be modelled with respect to the nominal trajectory. Using the simulation platform, I modelled the uncertainties with slope bounds around a pre defined trajectory. We used a [Key-point CNN model developed at JPL, Becktor, **Deole** et al](https://doi.org/10.1109/AERO53065.2022.9843396).  Then an exhaustive search of uncertainties was used to compute slope bounds. Then in our paper at Scitech by [Newsha,**Deole** et al](https://arc.aiaa.org/doi/abs/10.2514/6.2022-2213), we showed that modified funnel synthesis can handle types of uncertainties.

<!--<img src="../images/sim/Sat%20diagram.png" width="280" height="200"><img src="../images/sim/error3d.png" width="280" height="200">-->
<img src="../images/funnel/Picture3.png" width="280" height="200"><img src="../images/funnel/state2.png" width="280" height="200"><img src="../images/funnel/state3.png" width="280" height="200">

### Passivity based control
[Link to my paper](https://arc.aiaa.org/doi/abs/10.2514/6.2023-2156)

A more general approach not involving nominal trajectories to model ML uncertainty, is to use passivity based models. We use the principle that "a good ML estimator must be passive" ie it should not add extra energy to the outputs. Therefore we model the input-output characteristics of this ML map and use sector bounded non linearities to demonstrate that ML maps can be passive. Then a linear feedback controller can be designed by defining constraints, uncertainties and stability criterions as LMIs and solving for feasibility.

<img src="../images/passivity/passivity4.png" width="280" height="200"><img src="../images/passivity/Picture1%20(1).png" width="280" height="200">
<!--<img src="../images/passivity/trajerror%20(1).png" width="280" height="200">-->

The controller makes the entire system passive, which allows us to connect multiple such systems by exploiting the passivity interconnection theorems. We show that consensus algorithms like max consensus and dynamic-average consensus can improve tracking in a network.

<img src="../images/passivity/consensus_system.png" width="280" height="200"><img src="../images/passivity/multi.png" width="280" height="200">
<!--<img src="../images/passivity/consensus_results.png" width="280" height="200">-->

Passivity certificates have shown to be important tools to classify quality of NN outputs.



## Estimation-aware trajectory planning for set-valued uncertainty
[Project Page(Videos + Code)](https://github.com/Rainlabuw/Obs_aware_opt)

One of my favorite research topics has been investigating perception-aware trajectory planning. We observe that certain NNs that are usually deployed in Physical environments can be modelled as state depdendent sensors. We observed that Keypoint networks behaved in this fashion under illumination states. So if uncertainty depends on state of the system then a trajectory planning problem can be designed such that the planned trajectory exhibits optimized state estimation. This makes following the trajectory easy. 

This is my current work in estimation-aware planning. Paper under review at [Journal of Guidance navigation and Control. ](https://arxiv.org/abs/2501.09192).

We use Sequential Convex Programming to solve Estimation-aware Optimal control problem. [Code shared here](https://github.com/Rainlabuw/Obs_aware_opt).

Here, we modelled the ML uncertainty as bounded sets, and defined observability condition on output tubes. Then, leverage concepts of set-based observability to design the trajectories which improve estimation alongside task completion.

<img src="../images/observability/distinguish.png" width="280" height="200">

Here we use keypoint-based CNN which has least uncertainty when illumination is optimized, we model this behavior using our UE-based sim and design the trajectory to optize estimation alongside estimation.

### single agent
For single agent case we show an example of Target tracking problem where an Ego spacecraft chases a Target by exploiting illumination as it improves its sensor performance. We show that overall state variance is reduced. [See paper](https://arxiv.org/abs/2501.09192).

![obsgif1](https://github.com/user-attachments/assets/e39cee1a-5bff-4ee3-a62f-dea134f56879)

We also presented an MPC approach to solving this problem to design optimized observability based trajectories on the fly. [See the paper.](https://arc.aiaa.org/doi/abs/10.2514/6.2024-0947) 

### Multiagent
The same setup can be optimized even further with a network of sensors, by quantifing the dimenisons where information is missing. The SCP alrogithm is implemented here for multi-agent scenario in a sequential approach.

![obsgif2](https://github.com/user-attachments/assets/e8c5a74d-4c4b-4410-9cfe-2035541c15e8)





## Neuronal Dynamics
Exciting Update incoming!!!
<!--
<img src="" width="280" height="200">
-->
## Hardware Projects

I am a big hardware/electronics/robotics nut. I have been working on and supervising some cool educational hardware projects at Rain lab. Take a look:::

- [Visit the Page for ROS2 enabled ground-robot platform for testing trajectory optimization](https://github.com/Rainlabuw/Johnny_demos)
- PNT project with mobile robots where we built our own positioning system for mobile robots. 
- Crafyflie 2 for trajectory optimization



I also helped build an inhouse drone for trajectory planning at Rain Lab :smiley:

![q1gif](https://github.com/user-attachments/assets/a80c08b7-b06f-4fdf-9923-0f4bc7cce097)

![q2gif](https://github.com/user-attachments/assets/4383cf36-f847-4339-88a6-fba42f1a3142)





