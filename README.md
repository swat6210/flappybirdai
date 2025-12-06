Flappy Bird Reinforcement Learning (DQN)
Region-Based Reward System | PyTorch | Pygame

This project implements a Deep Q-Learning (DQN) agent that learns to play Flappy Bird using a region-based adaptive reward system. The environment is built with Pygame, and the neural network agent is trained using PyTorch.

🚀 Features
✔ Deep Q-Network (DQN) Agent
Two-model system: policy network + target network
Soft update of target network (τ = 0.01)
Experience Replay Memory (100k capacity)
Epsilon-greedy action policy

✔ Region-Based Reward System (Custom)
Unlike standard Flappy Bird RL, this project uses:
Positive reward for flying inside the pipe gap region
Penalty for entering danger zones near the pipes
Alignment bonus based on distance from gap center
Survival reward every frame
Big penalty upon collision
This helps stabilize early learning and reduces random crashing.

✔ Exploration → Exploitation Training
First 100 episodes use higher randomness
After that, agent switches to low-epsilon exploitation
Decision frequency reduced (action taken every few frames)

✔ Real-Time Pygame Rendering
Shows bird movement, pipes, and gap boundaries
FPS-controlled environment


📂 Project Structure
FlappyBird-RL/
│
├── main.py               # Full game + training loop
├── README.md             # Project documentation
└── requirements.txt      # Dependencies


🧠 How the Agent Learns (DQN Overview)
State Representation
The agent observes a 4-dimensional state:

  bird_y_normalized,
  bird_vertical_velocity,
  pipe_x_normalized,
  pipe_gap_center_normalized

Actions
0 → Do nothing  
1 → Jump  

Rewards (Region-Based)
Scenario	Reward
Staying alive	+0.1
Passing a pipe	+3.0
Inside gap region	+2.0
Outside safe region	-3.0
Near screen edges	-2.5
Collision	-10


Q-Learning Target
Q_target = r + γ * max(Q_next) * (1 - done)

Memory Replay
Random samples of size 2000 from a buffer of 100k transitions are used for stable learning.

🛠 Installation
1. Install Requirements
pip install pygame torch numpy

2. Run the Trainer
python main.py

🏆 Training Behavior
Episodes 1–100 → Exploration
epsilon = 0.5
Agent tries random actions to learn environment dynamics.
Episodes 101–300 → Exploitation
epsilon = 0.05
Agent uses its trained policy.
The best score is printed after each episode.

📈 Why Region-Based Rewards?
Traditional Flappy Bird RL fails early because:
Bird dies too quickly
No consistent positive signal
High randomness in first episodes
Your region-based reward system solves this by:
Rewarding correct alignment early
Penalizing dangerous positions
Encouraging smooth flying rather than binary success/failure
This leads to faster and more stable learning.

🔮 Future Improvements
Add Double DQN for more stable Q-updates
Add prioritized replay instead of random sampling
Save and load model weights
Graph training curves (reward/score over time)
Add GUI to toggle training/exploitation modes

👤 Author
Swat Shiro
Flappy Bird RL (DQN) using region-based adaptive reward shaping.
