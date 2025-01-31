---
title: "mROBerTO 2.0: A Millirobot for Swarm Studies"
excerpt: "Swarm algorithms are typically verified using millimeter-scale robots. I worked on the development of one such millirobot in this project."
---
<style>
p {
  text-align: justify;
}
</style>

# Introduction
Swarm robotic systems typically consist of simple and small-scale robots that collaborate with each other to compensate for their individual limitations. In research, such systems are typically verified using millimeter-scale robots (called millirobots) which allow for the deployment of large-scale swarms in constrained laboratory settings. I had the opportunity to develop one such millirobot during my PhD, where, in addition to robot design, I worked on developing motion-control and planning methodologies for swarms, as detailed <a href="{{ site.baseurl }}/software/collaborative-motion-control">here</a> and <a href="{{ site.baseurl }}/software/constrained-motion-planning">here</a>.

The mROBerTO (milli-ROBot-TOronto) 2.0 millirobot that was developed, Figure 1, sought to improve the already existing <a href="https://ieeexplore.ieee.org/document/7759331">mROBerTO 1.0</a> in terms of its modularity and locomotive capabilities. The mROBerTO 2.0 has a footprint of 22x20 mm, and comprises four modules: (1) the processing and communication module (mainboard), (2) the locomotion module, (3) the swarm sensing module, and (4) the proximity sensing module. It costs approximately $140 USD in components and boards. In designing this robot, I was responsible for schematic design, PCB design, assembly, coding, and testing. The modules of this robot are further detailed below, followed by videos of some of the experiments completed with this robot.

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
	<img src="{{ site.baseurl }}/assets/images/mroberto_2/all.png" alt="Image 1" style="width: 100%; align: middle;" >
</div>
<p style="text-align: center;">Figure 1: mROBerTO 2.0 and its modules.</p>

# Processing and Communication Module
Processing and communication capabilities are provided through an SoC that includes an ARM Cortex-M0 processor and built-in Bluetooth Low Energy (BLE) and ANT capabilities, Figure 2. The processing capabilities of the robot at this scale are, naturally, limited. This prevents the implementation of sophisticated control architectures on the robot, and typically limits it to simple behavior-based solutions. Furthermore, the robot has a limited communication range due to restrictions on power and antenna design. Thus, to communicate with its neighbors or an external computer, it must form a mesh communication network, and use a communication protocol such as flooding.
<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
	<img src="{{ site.baseurl }}/assets/images/mroberto_2/mainboard.png" alt="Image 1" style="width: 50%; align: middle;" >
</div>
<p style="text-align: center;">Figure 2: Processing and communication module.</p>

# Locomotion Module
The locomotion module provides mobility to the robot through a front-wheel differential drive configuration, Figure 3. The wheels are driven by stepper motors, and the third support is provided through a PTFE ball castor. Wheels at such small scales are not readily available. In response, an innovative solution was adopted by using circular PCBs as the rims, and heat shrink as the tires. 
<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
	<img src="{{ site.baseurl }}/assets/images/mroberto_2/locomotion.png" alt="Image 1" style="width: 50%; align: middle;" >
</div>
<p style="text-align: center;">Figure 3: Locomotion module.</p>
# Swarm Sensing Module
The swarm sensing modules allows the robot to measure the proximity to its neighbors. This is achieved through infrared (IR) emitters and detectors; each robot emits a unique frequency IR signal which is measured by its neighbors. Due to power limitations, the robot has a limited sensing range. Consequently, it must remain in close proximity to its neighbors during task execution. This short-range sensing limitation, which is encountered by many swarm platforms and applications, poses a challenge to localization, and must be addressed through collaborative-motion control and planning methodologies, such as those that I developed during my PhD, as detailed <a href="{{ site.baseurl }}/software/collaborative-motion-control">here</a> and <a href="{{ site.baseurl }}/software/constrained-motion-planning/">here</a>.
<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
	<img src="{{ site.baseurl }}/assets/images/mroberto_2/swarm_sensing.png" alt="Image 1" style="width: 50%; align: middle;" >
</div>
<p style="text-align: center;">Figure 4: Swarm sensing module.</p>
# Swarm Proximity Module
Finally, the proximity sensing module is equipped with a time-of-flight (ToF) sensor that allows the robot to measure the distance to the environment directly situated in front of it. Imagine a Lidar that only gives you ONE point! This presents a significant challenge to perception and mapping, a problem that I also investigated during my PhD.

# Experiments
mROBerTO 2.0 and mROBerTO 1.0 were used in various experiments throughout my PhD. Videos of two such experiments for chain formation and motion control are shown in Video 1 and Video 2, respectively.

<div style="display: flex; justify-content: center;">
	<video width="100%" controls>
	  <source src="{{ site.baseurl }}/assets/images/mroberto_2/Chain_Formation_Experiments.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 10px; text-align: center;">Video 1: Chain formation.</p>

<div style="display: flex; justify-content: center;">
	<video width="100%" controls>
	  <source src="{{ site.baseurl }}/assets/images/mroberto_2/Tether_Based_Motion_Video.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 10px; text-align: center;">Video 2: Tether-based motion control.</p>