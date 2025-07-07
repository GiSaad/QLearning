# QLearning

## Reinforcement Learning in a Grid World: Q-Learning vs. DQN

This project provides Python implementations of two fundamental reinforcement learning algorithms, Q-Learning and Deep Q-Network (DQN), to solve a classic 4x4 Grid World environment. The goal is for an agent to learn the optimal path from a starting position (0,0) to a goal (3,3).

## Features
### 1. Q-Learning Experiments 
- Tabular Q-Learning: A classic implementation from scratch using NumPy.

- Systematic Experiments: Includes 10 pre-defined configurations to demonstrate how different hyperparameters affect learning.

- Hyperparameter Analysis: Compares agents with varying α (learning rate), γ (discount factor), and ε (exploration strategy).

- Comparative Visualization: Generates plots for Total Reward and Steps per Episode across all experiments, smoothed with a moving average for clarity.

- Policy Visualization: Prints the final learned policy for each configuration as an intuitive grid of arrows.

### 2. Deep Q-Network 
- DQN Implementation: Uses PyTorch to build a neural network that approximates the Q-function.

- Experience Replay: Implements a ReplayBuffer to store and sample transitions, stabilizing the training process.

- Best Model Selection & Early Stopping: The training loop monitors performance and saves the best-performing model. It also stops training early if performance stagnates, improving efficiency.

- Detailed Plotting: Visualizes the training progress (reward and steps) for the DQN agent.

# Disscusion of how parameters affect convergence and learning speed of the First part  (q_learning_experiments)

## The Impact of Learning Rate (α)
The learning rate (α) determines how much new information overrides old information.

- A high alpha (like A2. High Alpha and B3. The Aggressive Learner) leads to faster learning. The agent rapidly updates its Q-values based on recent experiences. This is visible in the steep initial improvement in both reward and steps. However, a high alpha can also cause instability, as the agent might constantly overshoot the optimal policy, leading to oscillations and preventing stable convergence, as seen in the slightly more erratic lines for these agents.

- A low alpha (like B4. The Cautious & Patient Learner) results in slower, more stable learning. The agent updates its Q-values more cautiously, leading to a smoother, more gradual convergence.

## The Impact of Discount Factor (γ)
The discount factor (γ) controls the importance of future rewards. It dictates whether the agent is "farsighted" or "shortsighted."

- A high gamma (like A3. High Gamma and B3. The Aggressive Learner) makes the agent prioritize long-term rewards. This encourages it to find the most efficient (shortest) path to the goal, even if it requires more initial exploration. These agents ultimately converge to a higher total reward and a lower number of steps, representing a more optimal policy.

- A low gamma (like B1. The Impatient Agent) makes the agent "shortsighted." It heavily values immediate rewards. In this grid world, where all non-goal steps have a -1 reward, the agent is simply focused on ending the episode quickly rather than finding the most efficient path. As a result, its performance is good but clearly suboptimal compared to agents with higher gamma values.

## The Impact of Exploration vs. Exploitation (ϵ)
The epsilon (ϵ) parameter manages the trade-off between exploring the environment to find new paths and exploiting known good paths.

- Constant Exploration (like B5. The Unstable Learner with ϵ=0.5): This agent never stops exploring randomly. Consequently, it fails to converge. Its performance remains erratic and poor because it cannot consistently exploit the optimal policy it may have discovered.

- Greedy Approach (like B2. The Greedy Agent with low ϵ): This agent does very little exploration and begins exploiting its knowledge early on. This leads to rapid initial improvement, as seen by its quick convergence to a stable reward and step count. However, it gets stuck in a suboptimal policy because it didn't explore enough to find the truly best path.

- Decaying Epsilon (like A1. Baseline and A5. More Final Exploitation): This is the most effective strategy. The agent explores heavily at the beginning to discover various paths and then gradually reduces exploration to exploit the best policy it has found. The A5 agent, which reduces epsilon to a very low value (0.01), achieves one of the most stable and optimal policies, demonstrating the benefit of shifting from exploration to exploitation over time.

