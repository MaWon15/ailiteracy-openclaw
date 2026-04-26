# Chapter 26: Robotics
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is Robotics?

**Robotics** is the field of creating physical agents that sense and act in the physical world.

A **robot** is a physical agent that:
- **Senses** the environment via sensors (cameras, LIDAR, sonar, proprioception, force/torque).
- **Actuates** the environment via effectors (wheels, joints, grippers).
- **Computes** actions to achieve goals.

**Challenge:** Unlike virtual agents, robots must deal with the physical world — continuous spaces, sensor noise, actuation uncertainty, real-time constraints, and safety.

## Robot Hardware

### Sensors
- **Cameras:** RGB, stereo, depth (RGBD), event cameras.
- **LIDAR:** Laser range finder; provides 2D or 3D point clouds.
- **Sonar/Ultrasound:** Short-range proximity sensing.
- **IMU (Inertial Measurement Unit):** Accelerometer + gyroscope; measures acceleration and angular velocity.
- **GPS:** Outdoor localization (low frequency, meter-level accuracy).
- **Encoders:** Measure wheel rotation and joint angles (odometry).
- **Force/Torque sensors:** Measure contact forces.
- **Tactile sensors:** Sense contact and pressure.

### Actuators
- **Wheels/Tracks:** Mobile platforms.
- **Joints (revolute, prismatic):** Robot arms.
- **End-effectors:** Grippers, tools.
- **Drones (UAVs):** Rotors for aerial locomotion.
- **Soft robots:** Compliant, deformable bodies.

## Kinematics

**Kinematics:** Relationship between joint configurations and robot pose.

### Forward Kinematics
Given joint angles θ = (θ₁, ..., θₙ), compute end-effector position/orientation.
- **Denavit-Hartenberg (DH) parameters:** Standard convention for parameterizing robot arms.
- Result: A transformation matrix describing end-effector pose.

### Inverse Kinematics (IK)
Given a desired end-effector pose, find joint angles θ that achieve it.
- May have 0, 1, or infinitely many solutions.
- **Analytical IK:** Closed-form for simple robots.
- **Numerical IK:** Iterative optimization (Jacobian pseudoinverse).
- **Jacobian J:** Maps joint velocity θ̇ to end-effector velocity ẋ = Jθ̇.
- **Pseudoinverse:** θ̇ = J⁺ẋ (minimizes joint velocity).

## Configuration Space (C-Space)

**Configuration space (C-space):** The space of all possible robot configurations.
- For a 6-DOF arm: 6-dimensional space.
- **C-free:** Configurations with no collision.
- **C-obstacle:** Configurations where the robot is in collision.

Reduce motion planning to path-finding in C-space.

## Motion Planning

Find a collision-free path in C-space from start to goal.

### Grid-Based Planning
- Discretize C-space into a grid; apply A*.
- Works for low-dimensional spaces (2D/3D); scales poorly.

### Probabilistic Roadmap (PRM)
1. Randomly sample configurations in C-free.
2. Connect nearby configurations with local planners.
3. Build a roadmap; query it with A*.
- **Probabilistically complete:** Finds a path (if one exists) as samples → ∞.

### Rapidly Exploring Random Trees (RRT)
1. Start with a tree rooted at the start configuration.
2. Randomly sample a configuration; extend the nearest tree node toward it.
3. Terminate when the goal is reached.
- **RRT*:** Asymptotically optimal variant that rewires the tree.
- Efficient for high-dimensional spaces; widely used.

## Localization

**Where am I?** — Estimate robot position given a map and sensor readings.

### Kalman Filter Localization
- State: (x, y, θ) position and heading.
- Prediction: Propagate state using motion model.
- Update: Incorporate sensor readings.
- Assumes Gaussian distributions; linear Gaussian dynamics.

### Particle Filter Localization (Monte Carlo Localization)
- Represent belief as a set of particles (x, y, θ) with weights.
- Prediction: Sample new particles from motion model.
- Update: Weight by sensor model likelihood.
- Resample.
- Handles non-Gaussian, multimodal beliefs.
- **Gold standard for mobile robot localization.**

### Global Localization
- Robot doesn't know its initial position.
- Particle filter starts with uniform distribution over entire map.
- **Kidnapped robot problem:** Handle sudden large changes in position.

## Mapping

**Where are obstacles?** — Build a map of the environment.

- **Occupancy grid:** Discretize environment; each cell is occupied/free/unknown.
- Update cells using laser scans and Bayes' Rule.
- Efficient for 2D navigation.

## Simultaneous Localization and Mapping (SLAM)

**SLAM:** Build a map while simultaneously localizing within it.

This is a chicken-and-egg problem: need a map to localize, need location to build map.

### Graph-Based SLAM
- Represent poses as nodes; relative transformations as edges.
- Optimize node positions to minimize constraint errors (bundle adjustment).

### EKF-SLAM
- State = robot pose + all landmark positions.
- Updates using EKF as robot moves and observes landmarks.
- O(n²) per step — scales poorly.

### Particle Filter SLAM (FastSLAM)
- Each particle maintains a robot trajectory AND a map.
- Uses Rao-Blackwellization — landmark positions are estimated analytically per particle.
- O(n log n) per step.

### Modern SLAM Systems
- **ORB-SLAM3:** Visual SLAM using ORB features.
- **LIO-SAM:** LiDAR + IMU; popular for outdoor mobile robots.
- **Neural SLAM / NeRF-based SLAM:** Emerging approaches using implicit neural representations.

## Planning Under Uncertainty

### Probabilistic Roadmaps with Uncertainty
- Paths that avoid obstacles even considering position uncertainty.

### MDPs and POMDPs for Robotics
- **Navigation MDPs:** Reward for reaching goal; penalty for collisions.
- **POMDPs for manipulation:** Handle uncertain object positions and grasps.

## Robot Manipulation

- **Grasping:** Detect objects (6-DOF pose estimation); plan stable grasps.
  - **GraspNet / GIGA:** Learning-based grasp planning.
  - **Force closure:** Grasp that can resist any external wrench.
- **Task and motion planning (TAMP):** Combine symbolic task planning (PDDL) with motion planning (RRT).

## Modern Robotics

### Learning for Robotics
- **Imitation learning:** Learn from human demonstrations.
- **RL for robotics:** Sim-to-real transfer; PPO/SAC agents for locomotion and manipulation.
- **Foundation models for robotics:** RT-2, RT-X — generalist robots using vision-language models.

### Autonomous Vehicles
- **Perception:** LIDAR + camera fusion; 3D object detection.
- **Prediction:** Forecast trajectories of pedestrians and vehicles.
- **Planning:** Behavior planning + motion planning + control.
- Key challenges: edge cases, adverse weather, regulatory approval.

## Key Terms

- **Configuration space (C-space):** Space of all robot configurations; motion planning operates here.
- **Forward/Inverse kinematics:** Compute end-effector pose from joints / joints from target pose.
- **PRM / RRT:** Sampling-based motion planners for high-dimensional C-spaces.
- **Particle filter localization:** Monte Carlo method for non-Gaussian robot localization.
- **SLAM:** Simultaneous Localization and Mapping.
- **Occupancy grid:** Probabilistic map of free and occupied space.
- **TAMP:** Task and Motion Planning — combines symbolic and geometric planning.
