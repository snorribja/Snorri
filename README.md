# Snorri's Project Repository

Welcome to my GitHub repository! This repository contains a collection of projects I've been working on, exploring various areas such as reinforcement learning, game development, and system integration. Below, you'll find a brief overview of each project included in this repository.

## Projects

### 1. Flappy Bird Reinforcement Learning Agent
This project explores using reinforcement learning (Q-Learning and Deep Q-Learning) to train an agent to play the game Flappy Bird. The goal is to develop an agent that can navigate obstacles to achieve high scores by balancing exploration and exploitation strategies. The project includes:
- Implementation of Q-Learning with state discretization and epsilon-greedy policy.
- Deep Q-Learning using neural networks for approximating Q-values in a continuous state space.
- Comparison of performance and stability between Q-Learning and DQN in the Flappy Bird environment.

### 2. FIFA Classification Analysis
This project provides an analysis and classification of FIFA player data, focusing on player attributes across different positions. The goal is to categorize player positions and compare their performance across various skill areas like shooting, passing, defending, and more.

### 3. Raft-Based Distributed Consensus System  
This project implements a distributed consensus algorithm based on Raft, enabling multiple servers to agree on a sequence of client commands in the presence of failures. The goal is to maintain consistency across a replicated log using UDP and Protobuf. The project includes:
- Leader election with randomized timeouts and majority voting.
- Log replication and commitment through quorum-based agreement.
- Simulation of fault tolerance via suspend/resume commands and in-memory state handling.

### 4. Careeon (Submodule)  
The **Careeon** project is included in this repository as a Git submodule. You can visit the live website here (can take 20 seconds to start):[https://careeon.onrender.com](https://careeon.onrender.com)
Careeon is maintained in a separate repository, which allows it to be tracked independently. A demo video is available in the Careeon repository—feel free to check it out.
If you clone this repository, make sure to initialize the submodules to pull in the latest version of **Careeon**:

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




