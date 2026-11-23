# M1 EDU

[中文说明](README_zh.md)

M1 EDU is the public entry point for learning, training, and deploying reinforcement-learning policies on the Zeroth M1 humanoid robot. This repository organizes the workflow and points to the maintained training and deployment repositories.

## Start here

| Goal | Repository |
| --- | --- |
| Train and evaluate policies in simulation | [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train) |
| Deploy an exported ONNX policy on the robot | [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy) |

<div align="center">
  <img src="assets/m1-edu-lab.png" alt="M1 EDU development workspace" width="760">
  <br>
</div>

<div align="center">
  <img src="assets/m1-edu-xray.png" alt="M1 EDU internal structure reference" width="420">
  <br>
</div>

## Workflow

```text
M1 EDU hardware
      │
      ├── simulation and policy training
      │       └── M1_EDU_Train
      │
      ├── policy export to ONNX
      │
      └── robot-side policy deployment
              └── M1_EDU_Deploy
```

The two code repositories are intentionally maintained separately. Training dependencies, simulation assets, checkpoints, and experiment logs belong in the training repository. Robot connection code, deployment configuration, ONNX models, and runtime examples belong in the deployment repository. This repository provides the shared entry point and workflow documentation.

## Training

Open [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train) for the supported environment setup and commands.

The current training repository documents the following stack:

- Ubuntu 20.04 or Ubuntu 22.04
- Python 3.8 in a Conda environment
- NVIDIA Isaac Gym Preview 4
- `rsl_rl`
- `JOYIn_gym`

The documented training entry point is:

```bash
python JOYIn_gym/legged_gym/scripts/train.py --task=mini1_18dof_walk --num_envs=40
```

Use the training repository README as the source of truth for installation details, task configuration, checkpoints, and simulation troubleshooting.

## Export and deployment

After a policy has been validated in simulation, export it in the format expected by the deployment runtime and follow the instructions in [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy).

The deployment repository currently documents:

- connecting the development computer and robot on the same local network
- connecting to the robot through SSH
- placing an ONNX policy in the deployment model directory
- configuring observation dimensions, history stacking, joint parameters, and scaling factors
- starting the walking demo with the selected policy

The example deployment command is:

```bash
python demo_walk.py --model=model/your_model_name.onnx
```

The policy configuration used during deployment must match the configuration used during training. Check the deployment repository before changing observation layout, history length, action dimensions, joint defaults, or control parameters.

## Repository roles

### This repository

- provides the M1 EDU project entry point
- documents the simulation-to-robot workflow
- links the maintained public repositories
- records project-level guidance that applies across the workflow

### [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train)

- contains the Isaac Gym training environment
- contains the M1 task configuration and training scripts
- contains the bundled `JOYIn_gym` and `rsl_rl` source trees
- contains simulation resources and experiment outputs tracked by that repository

### [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy)

- contains the ROS 2 deployment examples
- contains robot communication and control code
- contains deployment configuration and example ONNX policies
- contains robot API and setup references under `api/`

## Getting help

For training failures, task configuration, or simulation behavior, open an issue in [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train). For robot connectivity, ROS 2 runtime behavior, policy loading, or deployment failures, open an issue in [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy). Use this repository for project-level documentation and navigation issues.