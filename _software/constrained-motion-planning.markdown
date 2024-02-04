---
title: "Constrained Swarm Motion Planning"
---
<style>
p {
  text-align: justify;
}
</style>
# Introduction
Swarm robotic systems with sensing limitations typically rely on adopting collaborative-motion control strategies, such as those described <a href="{{ site.baseurl }}/software/collaborative-motion-control">here</a>. While such strategies allow the swarm to compensate for its sensing limitations and achieve accurate localization and motion control, they also impose constraints on the trajectories of the member robots. 

These constraints must be considered when planning the motion of the swarm for a multi-task mission, where each task in a mission must be completed by a subset of a swarm at hand (referred to as a <i>coalition</i> of robots). In the context of multi-task mission execution, collaborative-motion control strategies typically require:
1. The swarm to be divided into worker robots that accomplish the tasks at hand and support robots that facilitate the movement of the worker robots, and 
2. For the worker and support robots to synchronize their motion. 

The following Sections detail a constrained planning methodology that was developed to address this problem.

# Constrained Planning Methodology
A constrained swarm motion planning methodology was developed to optimize the motion of the swarm while considering the constraints imposed by collaborative-motion control strategies, Figure 1. The methodology utilizes five mechanisms to optimize the mission completion time: 
1. The division-of-labor of the swarm into worker and support robots, 
2. Task allocation of the worker robots, 
3. Worker robot path planning, 
4. Movement concurrency, and 
5. Movement allocation to the support robots. 

The interdependence of these mechanisms requires the methodology to seek their optimal combination by varying them concurrently. Once the optimal solutions of all mechanisms are found, the corresponding support robot paths and swarm trajectories can be determined. 

<div style="display: flex; justify-content: center;">
	<figure>
	  <img src="{{ site.baseurl }}/assets/images/files_constrained_planning/constrained_planning_method.jpg" alt="Nature Image" style="width: 300px; height: auto;">
	</figure>
</div>
<p style="margin-top: 10px; text-align: center;"> Figure 1: Constrained planning methodology </p>

## Division-of-Labor
Robotic swarms typically consist of a high number of homogenous robots that can be programmed to operate in different roles. When a homogenous swarm is adopted, the division must strike an (optimal) balance between the number of worker and support robots. An increase in the number of worker robots, at the expense of support ones may at first appear as allowing for the faster parallel completion of more tasks by increasing the number of distinct coalitions. However, swarm constraints may lead to significant degradation in mission completion time due to the lack of sufficient number of support robots required to accomplish the desired parallelism. 

## Task Allocation
The task allocation stage focuses on the optimal grouping of worker robots into coalitions (i.e., teams of robots that collectively work on a task). Task-allocation can be formulated to indicate the number of robots that leave one task for another, without specifying the robots' identities. This approach can be used to enhance the scalability of optimization.

Figure 2 below illustrates a candidate task allocation solution generated for a swarm mission with three tasks.

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/files_constrained_planning/task_allocation.jpg" alt="Image 1" style="width: 50%; align: middle;" >
</div>
<p style="text-align: center;">Figure 2: Task allocation solution.</p>

## Worker Robot Path Planning
The goal of path planning is to find a balance between (i) aiming for each sub-coalition to get to its next task as quickly as possible and (ii) allowing the support robots to facilitate these paths efficiently. For example, if each sub-coalition were to operate without collaborating with support robots, it would move along the shortest possible path. However, due to the need for collaboration, sub-coalition paths must be planned to also consider the support robots which may, potentially, be facilitating multiple paths concurrently for enhanced efficiency in mission execution. 
Herein, this goal is achieved by allowing the temporary/intermediate relocation of sub-coalitions to task-stops that represent tasks that they are not allocated to, enroute to their allocated task. At these intermediate task-stops they remain as visitors, not participating in the work carried out by other worker robots allocated to this task. 

Figure 3 below illustrates a candidate worker robot path planning solution generated for the task allocation solution in Figure 2.

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/files_constrained_planning/worker_paths.jpg" alt="Image 1" style="width: 50%; align: middle;" >
</div>
<p style="text-align: center;">Figure 3: Worker robot path planning solution.</p>

## Movement Concurrency
The motion of a group of robots from one task to another can be divided into multiple movements that must be facilitated by support robots. Once divided, multiple movements may start and end at the same task-location. Such movements can be planned to be facilitated concurrently by the support robots. Multiple movements that are facilitated concurrently would start and end at the same time and would be facilitated by the same set of support robots. This allows the efficiency of the support robots to be enhanced.

## Movement Allocation
Movement allocation is synonymous to task allocation. Namely, this mechanism aims to optimize the allocation of the support robots to the movements that must be facilitated. 

Figure 4 illustrates candidate movement concurrency and movement allocation solution generated for the worker robot path planning solution in Figure 3.

<div style="display: flex; flex-wrap: wrap; justify-content: space-around;">
<img src="{{ site.baseurl }}/assets/images/files_constrained_planning/movement_conc_alloc.jpg" alt="Image 1" style="width: 50%; align: middle;" >
</div>
<p style="text-align: center;">Figure 3: Worker robot path planning solution.</p>

# Examples
Video 1 illustrates the execution of a 5-task mission with a 50-robot swarm, with motion plans found through the developed methodology. Performance is compared to the mission planning with a competing sub-optimal methodology.
Video 2 illustrates the execution of a 10-task mission with a 100-robot swarm.

<div style="display: flex; justify-content: center;">
	<video width="560" height="315" controls>
	  <source src="{{ site.baseurl }}/assets/images/files_constrained_planning/simple_example_video.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 10px; text-align: center;">Video 1: Multi-task mission execution with 50-robot swarm.</p>

<div style="display: flex; justify-content: center;">
	<video width="560" height="315" controls>
	  <source src="{{ site.baseurl }}/assets/images/files_constrained_planning/complex_example_video.mp4" type="video/mp4">
	  Sorry! Your browser does not support the video tag.
	</video>
</div>
<p style="margin-top: 10px; text-align: center;">Video 2: Multi-task mission execution with 100-robot swarm</p>

# Reference
This work was published in:
<p style="padding-left: 40px;"> 
	K. Eshaghi, G. Nejat, and B. Benhabib, “<i>A concurrent mission-planning methodology for robotic swarms using collaborative motion-control strategies</i>,” J. Int. Rob. Syst., vol. 108, no. 2, pp. 1-26, Apr. 2023.
</p>
