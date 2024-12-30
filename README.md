# Evolutionary Algorithm Application to Tensegrity Bot Structures and Controllers

## Project Overview

This project investigates the use of evolutionary robotics and algorithms to design both the physical configurations and controllers of tensegrity robots to perform tasks that are not immediately intuitive code or design.

A simple 2D physics simulator was developed using Taichi, where gravity and a floor environment are implemented. The robots in this simulation, referred to as tensegrity bots, consist of masses represented as circles connected by motorized springs depicted as lines. Tensegrity robots have practical applications, including potential use as resilient rover designs. Despite their robustness and stability, programming such machines for movement is inherently challenging. A promising solution involves leveraging evolutionary algorithms and neural networks.

In these simulations, a randomized neural network is initialized and updated after each simulation. The neural networks receive sensor input from the robot at every time step. The loss function is determined by how far the robot moves to the right within a fixed duration. Over successive simulations, the controller evolves, learning to maximize forward movement. Additionally, the robot’s physical structure (its "body") is also allowed to evolve over time through a nested optimization process. An inner loop focuses on training the controller, while an outer loop adjusts the robot's body configuration.

### Robot Design and Constraints

The robot’s body is initially generated using a 4x4 grid of mass points. Between 5 and 12 nodes (mass points) are selected, and a random subset of springs connecting those nodes is chosen. Constraints are applied to ensure stability and functionality:

- The nodes must form a connected structure (not disjoint).
- Each node must have at least 3 and no more than 7 spring connections.

To simplify implementation, all mass points in the grid are always present, but unused springs are assigned a stiffness of zero. This allows unselected masses to drop to the ground without affecting the robot's movement. In the simulation visualizations, unused masses and springs are depicted in gray.

Once the robot is configured, it undergoes a set of training epochs to optimize its controller. The best loss value achieved is recorded. The robot’s body is then mutated by adding or removing a node or spring. The mutated robot is re-evaluated with a reinitialized controller. If the new configuration outperforms its predecessor, it becomes the new parent for further mutations. If it underperforms, the mutation is discarded, and the process is repeated.

### Controller Training Improvements

During controller training, a modification was introduced to improve the convergence of the loss function. If a controller underperforms compared to its predecessor, it reverts to its previous state, and the learning rate is decreased. This adjustment reduces erratic behavior in the loss curve, promoting more monotonic fitness convergence.

### Context and Contributions

The physics simulation and the basic tensegrity bot with its neural controller were developed as part of the Advanced Evolutionary Robotics course taught by Dr. Josh Bongard at The University of Vermont. The extensions, including the learning rate adjustments and the body mutation process, were developed independently as a final project.

Code for this project is available in this repository, along with a link to the Google Colab notebook for further exploration.
