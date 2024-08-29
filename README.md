# Collaborative-Maze-Solver-using-Reinforcement-Learning



## Reinforcement Learning

This project utilizes reinforcement learning, specifically Deep Q-Learning, to train the robots to navigate through the maze efficiently.

### Key Concepts

1. **Agent**: In our case, the e-Puck robots that learn to navigate the maze.
2. **Environment**: The maze in which the robots operate.
3. **State**: The current position of the robot in the maze, represented by sensor readings.
4. **Action**: The movement decisions made by the robot (e.g., move forward, turn left, turn right).
5. **Reward**: A numerical value given to the agent based on its actions. In our implementation:
   - Reaching the target: High positive reward
   - Collision: High negative reward
   - Empty space: Small negative reward (to encourage efficient pathfinding)
6. **Policy**: The strategy that the agent follows to determine the next action based on the current state.

### Neural Networks in RL

In this project, we use a neural network to approximate the Q-function, which predicts the expected cumulative reward for each action in a given state. Our network architecture consists of:

- Input layer: Corresponds to the state representation
- Hidden layers: Two fully connected layers with ReLU activation
- Output layer: Corresponds to the Q-values for each possible action

### Deep Q-Network (DQN)

DQN is an advanced RL algorithm that combines Q-learning with deep neural networks. Key components of our DQN implementation include:

1. **Q-Network**: A neural network that approximates the Q-function, mapping states to action values.
2. **Target Network**: A separate network used to compute target Q-values, updated periodically to stabilize training.
3. **Experience Replay**: A buffer that stores and randomly samples past experiences (state, action, reward, next state) to break correlations between consecutive samples and improve learning stability.
4. **Epsilon-Greedy Exploration**: A strategy that balances exploration and exploitation by sometimes taking random actions (controlled by an epsilon value that decays over time).

### Training Process

The training process for our maze-solving robots involves the following steps:

1. **Initialization**: The robots start with random policies, and the replay buffer is empty.
2. **Exploration and Data Collection**: 
   - The robots explore the maze using an epsilon-greedy strategy.
   - Experiences (state, action, reward, next state) are collected and stored in the replay buffer.
3. **Training**:
   - Batches of experiences are randomly sampled from the replay buffer.
   - The Q-network is updated using these experiences:
     - Compute the current Q-values
     - Compute the target Q-values using the target network
     - Calculate the loss (mean squared error between current and target Q-values)
     - Update the Q-network weights using backpropagation
4. **Target Network Update**: Periodically, the target network weights are updated to match the Q-network.
5. **Epsilon Decay**: The exploration rate (epsilon) is gradually reduced to shift from exploration to exploitation.
6. **Iteration**: Steps 2-5 are repeated for many episodes to refine the policy.

This implementation uses PyTorch for building and training the neural network, allowing for efficient GPU acceleration if available.
