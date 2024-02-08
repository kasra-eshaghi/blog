---
title: "Swarm Localization Using Partial Location Data"
excerpt: "Swarm localization can be challenging due to the scalability issues associated with a large number of robots. In this project, I worked on the development of a swarm localization methodology that was both effective and scalable"
---
<style>
p {
  text-align: justify;
}
</style>
# Introduction
Swarm localization deals with the problem of estimating the position of all robots with respect to a global reference frame. This must be achieved using the inter-robot and outer-robot proximity measurements obtained by the member robots which, respectively, describe the relative distance and bearing to neighboring robots and landmarks. Due to the absence of odometry, the robot’s executed motion commands must be used to globally position the swarm.
Swarm localization is particularly challenging due to the severe computational limitations of the robots in a swarm. Consequently, the swarm localization methodology to be developed must be computationally efficient by (1) spreading the localization process over multiple sequential steps, and (2) using a simplified approach to consider uncertainty. 

The swarm localization methodology developed in this project, Figure 1, estimates the configuration of the swarm (i.e., position of all robots with respect to the global reference frame), over three sequential steps. The two steps, respectively, obtained a preliminary estimate of the swarm’s configuration based on motion commands, and a secondary estimate of the swarm’s topology based on proximity measurements. These two estimates are, then, combined in the third step of localization through superimposition. 

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/localization/methodology.png" alt="Image 1" style="width: 100%; align: middle;" >
</div>
<p style="text-align: center;">Figure 1: Localization methodology.</p>

# Preliminary Configuration Estimate
A preliminary estimate of the swarm’s configuration after the execution of motion commands can be determined by assuming these commands were executed with no uncertainty.  Figure 2 below illustrates an example preliminary estimate obtained for a swarm of three robots that move to their new configuration (filled blue dots) located near a landmark (purple square).

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/localization/preliminary_estimate.png" alt="Image 1" style="width: 40%; align: middle;" >
</div>
<p style="text-align: center;">Figure 2: Preliminary configuration estimate.</p>

# Secondary Topology Estimate
The swarm’s topology represents the position of all robots with respect to a local swarm frame. This topology, as well as that of the surrounding landmarks, can be acquired by clustering the inter-robot and outer-robot proximity measurements obtained by the member robots through a custom objective function. Figure 3 below illustrates the post-motion estimated topology of the swarm.

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/localization/secondary_estimate.png" alt="Image 1" style="width: 40%; align: middle;" >
</div>
<p style="text-align: center;">Figure 3: Secondary topology estimate.</p>

# Superimposition
The swarm’s configuration is estimated by combining the preliminary swarm configuration estimate and the secondary swarm topology estimate. This is achieved through a weighted superimposition process that seeks to position the swarm topology to minimize the distances between corresponding robot positions. The weights associated with the robots in the superimposition step are selected to reflect the uncertainty in the estimated positions in the first two steps. This typically results in robots whose positions are known with higher certainty to be weighted higher, and to have a higher impact on the global position of the swarm. 

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/localization/superimposition.png" alt="Image 1" style="width: 40%; align: middle;" >
</div>
<p style="text-align: center;">Figure 4: Superimposition.</p>

# Publication
This work was published in:
<p style="padding-left: 40px;"> 
	K. Eshaghi, Z. Kashino, H. J. Yoon, G. Nejat, and B. Benhabib, “<i>An inchworm-inspired motion strategy for robotic swarms</i>,” Robotica, vol. 39, no. 12, pp. 2283–2305, Apr. 2021. 
</p>
