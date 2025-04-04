# Simulation of Thieves

_Jeremy Fischer, Nicholas Jean, Stephen Lee, Shiran Yuan_

_UC Berkeley_

## Project Summary

Our project aims to create a realistic, real-time water simulation in Unity by leveraging common heuristic techniques. We aim to implement a set of features including lighting effects like caustics, buoyancy and destruction physics for ships, and level of detail optimizations to really bring the simulation to life.

## Problem Description

Water simulation is an important problem that has been extensively researched for tasks such as CGI film, video game design, and simulation environments. However, for cases such as video game design, making it real-time is crucial, and there is currently no standardized way of optimizing it (so different implementations use wildly different techniques based on artistic preference and requirements). We aim to produce a real-time water simulation that contains most of the features which will be widely wanted, including a realistic surface, caustics for visual effect, buoyancy for physics, destruction physics for gameplay, and LOD optimization to make sure that it is still real-time.

The simulation can be broken up into 3 main parts: mesh manipulation, lighting, and buoyancy. The water mesh will be manipulated to follow a sum of sine waves with various frequency modifications in the frequency domain by using FFT. To achieve real-time performance, the wave calculations will be parallelized by unity compute shaders so the GPU can be utilized. Custom shaders will be written to handle the lighting of the water mesh, potentially caustics if time allows. Buoyancy will be implemented by devising a sampling strategy to approximate volume of an object under the water mesh and apply appropriate physics to push the object up.
We expect the initial task of mesh manipulation in real-time to be hard as it requires GPU programming. 

## Goals and Deliverables

### Planned to Deliver

The following are the objectives required for a successful project. We are confident that these objectives can be achieved with Jeremy’s expertise in Unity and plenty of resources available to follow.

__Water Mesh__. Given a mesh, the vertices can be displaced following an artistic choice of sum of sine waves to provide a convincing water mesh. This is the foundation of the water simulation as it provides the surface geometry to apply lighting, buoyancy, and physics. The math is straightforward, but as the resolution of the mesh increases, the number of calculations is too burdensome for a CPU to handle, so parallelism must be employed. Unity has a built-in method to access GPU resources via compute shaders which is what we will use to speed up the simulation to ensure real-time (defined by 60 fps) can be achieved.

__Basic Lighting__. To shade our water mesh, we will implement Blinn-Phong shading similar to the shaders implemented in HW4 with cloth. We will tune the model parameters so that we get reasonable looking water.

__Quality and Performance__. We aim for 60 fps on a minimum 100x100 unit mesh. The frames per seconds should be stable and have no significant frame drops as the camera moves around and lighting changes.

__Demo__. We will showcase the core water simulation features through images and videos highlighting the dynamic water mesh, real-time lighting using Blinn-Phong shading, and buoyancy interactions. Various environments and scenarios (ex. Island in middle of ocean, pirate ships shooting cannons at one another, etc) will be used to demonstrate these features. The videos will be relatively short, 1 minute long at most. 

### Hope to Deliver

These are the objectives that will make this project stand out from the rest if able to complete. Once the initial water mesh logic is complete the following tasks can be worked on in parallel and provide supplemental polish to the simulation.

__Buoyancy__. Buoyancy is the upward force a fluid exerts on an object, arising from pressure differences. This force increases as more of the object is submerged, helping it float. The calculations of this force is not straightforward, models can be of complex geometry and partially submerged at weird angles. Thus a sampling strategy will need to be developed to estimate the volume submerged under our mesh so a proper force can be applied to Unity’s built-in physics system. We will need to balance anti-aliasing techniques making the buoyancy more accurate with our real-time goal.

__Advanced Lighting and Caustics__. We aim to improve the visuals of the scenes we render by implementing some more advanced lighting effects such as caustics. Depending on the performance impact, we may aim to do this in a couple different ways such as photon mapping ideally or more approximate approaches such as fourier-based methods.

__Innovative Anti-Aliasing and Optimization__. The standard baseline we are implementing is based on the classic GPU Gems method using uniform lattice meshes. However, this causes aliasing and waste of computation at large distances because perspective transformation causes the frequency of that part of the mesh to be very high (causing aliasing) while its amplitude is very low (waste of computation). We propose decreasing the mesh resolution by removing vertices such that the frequency of the underlying mesh will always be lower than the Nyquist frequency, thus offering antialiasing. One potential way of implementing this would be, inspired by the quadtree LOD (level of detail) method in terrain generation, pre-generate mesh patches at predefined resolutions and then place them in chunks, and dynamically shift the patch locations whenever the camera changes chunks.

__Supplemental Demo__. One of our videos will feature destruction physics, showcasing pirate ships firing at each other, where damaged ship parts dynamically interact with the water surface to visually demonstrate our buoyancy physics. We will also create an island environment that’s in the middle of an ocean to demonstrate water interacting with the edges of the island and potentially waves crashing onto the island. Additionally, we will showcase the caustic effects through brief videos/animations.

__Quality and Performance__. We aim for 144 fps on a minimum 1000x1000 unit mesh. The frames per second should be stable and have no significant frame drops as the camera moves around, lighting changes, or as objects receive buoyancy physics.

## Schedule

- Week 1
  - Project Setup (Jeremy)
  - Initial Water Mesh (All)
- Week 2
  - Milestone Video Slideshow (All)
  - Lighting Part 1: Basic Shading (Stephen)
  - Buoyancy Part 1 (Jeremy / Nick)
  - Destruction Physics (Nick)
  - AA & Optim Part 1 (Shiran)
  - Plan Showcase Videos (Nick)
- Week 3
  - Lighting Part 2: Caustics (Stephen)
  - Buoyancy Part 2 (Jeremy / Nick)
  - AA & Optim Part 2 (Shiran)
- Week 4
  - Display Scene (All)
  - Final Report Writing (All)
  - Showcase Videos (Nick)

## Resources

All group members have access to high performing machines with graphics cards.

[https://www.youtube.com/watch?v=vzqoLJmpUqU](https://www.youtube.com/watch?v=vzqoLJmpUqU)

[https://www.youtube.com/watch?v=PH9q0HNBjT4](https://www.youtube.com/watch?v=PH9q0HNBjT4)

[https://www.youtube.com/watch?v=yPfagLeUa7k](https://www.youtube.com/watch?v=yPfagLeUa7k)

[https://www.youtube.com/watch?v=ja8yCvXzw2c](https://www.youtube.com/watch?v=ja8yCvXzw2c)

[https://gpuopen.com/gdc-presentations/2019/gdc-2019-agtd6-interactive-water-simulation-in-atlas.pdf](https://gpuopen.com/gdc-presentations/2019/gdc-2019-agtd6-interactive-water-simulation-in-atlas.pdf)

[https://www.researchgate.net/publication/264839743_Simulating_Ocean_Water](https://www.researchgate.net/publication/264839743_Simulating_Ocean_Water)

[https://developer.nvidia.com/gpugems/gpugems/part-i-natural-effects/chapter-1-effective-water-simulation-physical-models](https://developer.nvidia.com/gpugems/gpugems/part-i-natural-effects/chapter-1-effective-water-simulation-physical-models)

