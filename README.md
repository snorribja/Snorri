# Snorri's Project Repository

Welcome to my GitHub repository! This repository contains a collection of projects I've been working on, exploring various areas such as reinforcement learning, game development, and system integration. Below, you'll find a brief overview of each project included in this repository.

## Projects

### 1. Flappy Bird Reinforcement Learning Agent
This project explores using reinforcement learning (Q-Learning and Deep Q-Learning) to train an agent to play the game Flappy Bird. The goal is to develop an agent that can navigate obstacles to achieve high scores by balancing exploration and exploitation strategies. The project includes:
- Implementation of Q-Learning with state discretization and epsilon-greedy policy.
- Deep Q-Learning using neural networks for approximating Q-values in a continuous state space.
- Comparison of performance and stability between Q-Learning and DQN in the Flappy Bird environment.

### 2. Careeon (Submodule)
The **Careeon** project is included as a submodule within this repository. It is a separate Git repository that can be tracked independently. Please go ahead and watch the video in the reop. If you clone this repository, make sure to initialize the submodules to get the latest content of **Careeon**:
```bash
git submodule update --init --recursive
```
The Careeon project details are available within its own repository.

# Cloning This Repository

To clone this repository along with its submodules, use the following command:

```bash
git clone --recurse-submodules https://github.com/snorribja/Snorri.git
```

If you have already cloned the repository without the --recurse-submodules flag, you can initialize the submodules afterward with:

```bash
git submodule update --init --recursive
```


