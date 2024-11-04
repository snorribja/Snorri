# Flappy Bird Reinforcement Learning Project

This project explores the use of reinforcement learning methods, specifically Q-Learning and Deep Q-Learning (DQN), to train an agent to play the game Flappy Bird. The aim is to enable the agent to learn policies that maximize survival and score, navigating through obstacles without crashing.

## Table of Contents
- [Flappy Bird Reinforcement Learning Project](#flappy-bird-reinforcement-learning-project)
  - [Table of Contents](#table-of-contents)
  - [Environment](#environment)
  - [Methodology](#methodology)
    - [Q-Learning Implementation](#q-learning-implementation)
    - [DQN Implementation](#dqn-implementation)
    - [Experiments to Improve the Agent](#experiments-to-improve-the-agent)
  - [Training Process and Results](#training-process-and-results)
  - [Conclusion and Recommendations](#conclusion-and-recommendations)
  - [License](#license)

## Environment

Flappy Bird presents a continuous, episodic, and finite environment. Each episode begins with the bird starting at a fixed position and ends when it crashes into a pipe or the ground. The continuous state space, including variables such as bird position and velocity, is discretized for Q-Learning to make learning manageable. Both methods rely on the Markov Property, assuming each state provides sufficient information for optimal decision-making without requiring past states.

## Methodology

### Q-Learning Implementation

**State Space Discretization**: 
- The agent’s state includes the bird’s vertical position, next pipe’s y-position, distance to the pipe, and vertical velocity, discretized into 64,125 states.

**Policy and Learning Mechanism**:
- The agent uses an epsilon-greedy policy (𝜀 = 0.1) to balance exploration and exploitation.
- The Q-value update formula: `Q(s, a) ← Q(s, a) + α(r + γ max Q(s', a') − Q(s, a))`
  - Learning rate (α) = 0.1, Discount factor (γ) = 1.0.
- Terminal state handling assigns a negative reward (-5) on crashes, helping the agent avoid such outcomes.

### DQN Implementation

**Neural Network**:
- A neural network with two hidden layers approximates Q-values, trained with the MLPRegressor.
- Input features include normalized state values: bird’s y-position, y-coordinate of the next pipe gap, distance to the nearest pipe, and bird’s velocity.

**Training Techniques**:
- Experience replay (buffer of 1000 experiences, batch of 100) reduces correlation between training samples.
- Target network updated every 100 steps improves learning stability.

### Experiments to Improve the Agent

Several experiments tested variations in epsilon, learning rate, and reward structure:
- **Epsilon**: Lower epsilon (0.01) improved stability, while higher epsilon (0.3) promoted rapid but unstable learning.
- **Learning Rate**: A higher rate (α = 0.2) enhanced learning speed but increased variability.
- **Reward Structure**: A balanced reward of +1 for passing pipes and -5 for crashes promoted both scoring and survival, while harsher penalties encouraged more cautious behavior.

## Training Process and Results

Q-Learning achieved impressive performance, converging on a stable policy after about 60,000 episodes. DQN, however, faced challenges in stabilizing due to the dynamic nature of the game and required more samples and careful hyperparameter tuning to reach effective policies.

- **Q-Learning** outperformed DQN in both stability and reward accumulation.
- **Performance**: Q-Learning achieved an average score of 52,000 across simulations, while DQN showed less reliable results.

## Conclusion and Recommendations

Q-Learning proved effective for the Flappy Bird environment, balancing sample efficiency and ease of implementation. While DQN has advantages in complex environments, its stability challenges in this project underscore the utility of simpler tabular methods when state discretization is feasible.

## License

This project is open-source and available for modification and reuse.
