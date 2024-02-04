---
title: "Collaborative-Motion Control Strategies for Robotic Swarms"
---

# Introduction
Swarm robotic systems, typically consisting of high numbers of collaborative robots, may be burdened with onboard sensing limitations due to hardware miniaturization. Such sensing limitations present a challenge for sensing-based robotic tasks, such as localization, perception, and mapping.

The work completed in this project specifically dealt with swarms that are only equipped with short-range proximity sensors. Members of such swarms are unable to to accurately localize individually and, thus, control their motion. This results in the accumulation of motion errors, and the divergence of the swarm from its desired motion.

Herein, these sensing limitations are addressed by leveraging the collaborative nature of robotic swarms. Namely, through the development of collaborative-motion control strategies that allow the robots to simultaneously execute their desired motion while helping each other compensate for their individual sensing limitations. Two such strategies were developed: the inchworm-inspired and tether-based strategies, as described below.

# Inchworm-Inspired Strategy
## Overview
The inchworm-inspired strategy seeks to address the sensing limitations of the swarm by allowing the robots to use each other as temporary reference frames during their motion. Namely, using this strategy, the swarm moves from one *configuration* to another over multiple incremental steps. In each step, a subset of the swarm operates as *anchor* robots that remain stationary while the remaining *mobile* robots move to their destinations. These anchors act as temporary reference frames for improved localization of the mobile robots. Once the mobile robots reach their destinations, they obtain proximity measurements to their anchor neighbors, and use these measurements to accurately estimate their positions. They, then, switch roles and act as anchors for another subset of the swarm that becomes mobile, allowing the swarm to incrementally move along its desired path.

The inchworm strategy is illustrated through Video 1 below for a swarm of six robots that moves to its destination three robots at a time. 
<div style="display: flex; justify-content: center;">
	<video width="300" controls>
	  <source src="/assets/files_collaborative_motion/inchworm_1.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 0px; text-align: center;">Video 1: Inchworm motion.</p>

Video 2 illustrates a swarm of ten robots that follow a sinusoidal path using the inchworm-inspired strategy. One may note that the swarm eventually diverges from its desired path, though this would occur at a slower rate than if anchors were not used.

<div style="display: flex; justify-content: center;">
	<video width="700" controls>
	  <source src="/assets/files_collaborative_motion/inchworm_2.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 0px; text-align: center;">Video 2: Inchworm motion for path following.</p>

## Optimization
A key variable of the inchworm-inspired strategy is the selection of the number and choice of anchor robots for every incremental step of motion. This selection would have a tangible impact on the path following performance of the swarm as it affects two competing sub-objectives: (1) swarm localization and (2) swarm speed. These sub-objectives are competing as a higher number of anchor robots typically results in lower localization errors, though requiring the swarm to move to its destination slowly. In contrast, less anchors would allow the swarm to move to its destination quickly, but at the cost of an increase in the accumulated localization errors.

In this regard, a nested optimization algorithm was developed to optimize the number and choice anchor robots, Figure 1. The outer optimization loop seeks the optimal number of anchor robots using a simple (single, discrete-variabel) search engine. The inner optimization loop, in turn, seeks the optimal choice of anchor robots for a specific number of anchors considered. The combinatoric nature of anchor-choice selection requires the adoption of a suitable search engine, such as a variation of the Genetic Algorithm. Furthermore, optimization is achieved through a simulation-based approach, where the motion of the swarm for an anchor choice is simulated numerous times, and the expected localization error calculated.
<div style="display: flex; justify-content: center;">
	<figure>
	  <img src="/assets/files_collaborative_motion/inchworm_nested_optimization.png" alt="Nature Image" style="height: 500px; width: auto;">
	</figure>
</div>
<p style="margin-top: 0px; text-align: center;"> Figure 1: Anchor optimization algorithm.</p>

## Reference
This work was published in:
<p style="padding-left: 40px;"> 
	K. Eshaghi, Z. Kashino, H. J. Yoon, G. Nejat, and B. Benhabib, “<i>An inchworm-inspired motion strategy for robotic swarms</i>,” Robotica, vol. 39, no. 12, pp. 2283–2305, Apr. 2021. 
</p>

# Tether-Based Strategy
## Overview
The tether-based strategy seeks to address the accumulation of localization and motion errors by allowing the swarm to maintain sensing connectivity to stationary landmarks in the environment. Namely, this strategy uses a secondary team of tether robots that collaborate with the swarm as it executes its motion. The tether robots form a wireless tether that dynamically changes its shape and length to extend the sensing range of the swarm, and to maintain continuous connectivity between the swarm and a landmark in its operating environment. By maintaining connectivity with and indirectly sensing the environment through this wireless tether, the swarm can localize through proximity measurements that are subject to noise that is independent of its traveled distance. This allows it to compensate for accumulated localization and motion errors.

The tether-based strategy is illustrated through Video 3 below for a swarm of six robots, equipped with a secondary team of five tether robots. The swarm moves to its destination using the inchworm-inspired strategy, while maintaining connectivity to a landmark through the wireless tether. Upon arrival, sensor measurements to the landmark are obtained and used to accurately localize the swarm and corrects its position.

<div style="display: flex; justify-content: center;">
	<video width="560" height="315" controls>
	  <source src="/assets/files_collaborative_motion/tether_1.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 0px; text-align: center;">Video 3: Tether motion to next destination</p>

Video 4 below illustrates a swarm of ten robots, equipped with a secondary team of fifteen tether robots, that follow a sinusoidal path using the tether-based strategy. One may note that the swarm may change its connectivity from one landmark to another during its motion. By maintaining connectivity to the environment through the tether, the swarm can compensate for accumulated localization errors and execute corrective motion commands.

<div style="display: flex; justify-content: center;">
	<video width="560" height="315" controls>
	  <source src="/assets/files_collaborative_motion/tether_2.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 0px; text-align: center;">Video 4: Tether motion for path tracking</p>

## Optimization
The motion of the tether robots is planned to through three sequential steps, Figure 2:
1. <i>Tether formation</i>: The tether formation step seeks to determine the connectivity point of the swarm and the position of the nodes that must be achieved by the tether robots to provide connectivity to this point. This step is completed with the objective of minimizing the localization errors of the swarm that depend on the above variables through an empirically derived function.
2. <i>Tether robot allocation</i>: For each tether, the tether robots need to be specifically assigned to the nodes at hand. This is completed with the objective of minimizing the distance travelled by the tether robots, allowing them to achieve the planned tethers quickly and accurately. A combinatoric search engine, such as a variation of Genetic Algorithms, must be adopted.
3. <i>Tether robot motion planning</i>: as the last step, based on the formed tethers and corresponding tether robot allocations, the collision-free paths of the robots from one tether to another would be determined. For example, using classical methods such as prioritized RRT.

<div style="display: flex; justify-content: center;">
	<figure>
	  <img src="/assets/files_collaborative_motion/tether_optimization.png" alt="Nature Image">
	</figure>
</div>
<p style="margin-top: 0px; text-align: center;"> Figure 2: Tether optimization.</p>

## Reference
This work was published in:
<p style="padding-left: 40px;"> 
	K. Eshaghi, A. Rogers, G. Nejat, and B. Benhabib, “<i>losed-loop motion control of robotic swarms – A tether-based strategy</i>,” IEEE Trans. Robot., vol. 38, no. 6, pp. 3564-3581, Dec. 2022.
	* Also presented at ICRA 2023.
</p>