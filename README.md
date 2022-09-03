# DFO visualization

This is a simple demo of *Dispersive Flies Optimization* (DFO), inspired by [this video](https://youtu.be/VZGp0Dv01rE).
You can try it [here](https://gijs-pennings.github.io/dispersive-flies). It visualizes how flies (circles) follow your mouse (crosshair).
This project is licensed under the [ISC license](LICENSE.txt).

DFO is a swarm intelligence metaheuristic. In other words, it is a high-level algorithm designed to find "good" solutions to optimization problems. In particular, it maintains a population of agents (here: flies) that each represent a solution. Each iteration of the algorithm, these agents are updated and hopefully "moved closer" to the optimal solution.
Compared to other metaheuristics, DFO has the advantage that it only uses one parameter (i.e., the disturbance threshold).

DFO was first introduced in [1]. However, the original paper is imprecise in some aspects.[^1]
Therefore, this implementation is based on [2], which includes a more detailed description.
Furthermore, I made two minor changes, which are discussed [below](#changes-to-base-algorithm).

[^1]: For example, the usage of ring topology is not described rigorously, it is not specified what happens in case of out-of-bounds coordinates, the pseudocode is inefficient, etc.

The optimization problem used for this demo is defined as follows.
The solution space is the set of all positions on the screen.
The cost of a solution is simply the distance to the mouse, and the objective is to minimize this cost.
Obviously, this optimization problem has no actual applications, but it makes for a nice demo.


## Changes to base algorithm

- When selecting the best neighbor, the current fly is also considered as a candidate, not only its (strict) neighbors. Without this change, the majority of flies do not seem to converge.
- When a coordinate of a fly is out-of-bounds, it is [clamped](https://en.wikipedia.org/wiki/Clamping_(graphics)) to the search space, instead of assigned a random value as described in [2]. Without this change, there is a disproportionate amount of exploration near the boundary of the search space.


## References

[1] M. M. al-Rifaie. Dispersive Flies Optimisation. In *2014 Federated Conference on Computer Science and Information Systems*, pages 529–538. IEEE, 2014.

[2] M. M. al-Rifaie. Dispersive Flies Optimisation: A Tutorial. In A. Slowik, editor, *Swarm Intelligence Algorithms: A Tutorial*, pages 135–147. CRC Press, 2020.
