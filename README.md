**Introduction**

This project focuses on solving the Taxi-v3 environment using Proximal Policy Optimization (PPO) from the Stable-Baselines3 library along with the Gymnasium API. Taxi-v3 is a discrete reinforcement learning task where an agent controls a taxi in a grid world.

**Why PPO Instead of DQN?**

We use PPO instead of DQN because PPO is a more stable and reliable policy-gradient method, especially in environments like Taxi-v3 where rewards are sparse and exploration is crucial.

PPO updates its policy using a clipped objective, preventing overly large and unstable updates and making learning more consistent. It also learns a stochastic policy, which naturally encourages exploration.

DQN, on the other hand, is a value-based method that depends heavily on replay buffers, target networks, and careful hyperparameter tuning. It can struggle in sparse-reward environments and tends to be less stable without extensive tuning.

Overall, PPO offers better stability, simpler training, and more reliable convergence, making it the preferred choice for this task.

**Learning Rate Analysis**

I compared two PPO learning rates on the Taxi-v3 environment: a standard value of 3e-4 and a more aggressive value of 3e-3, keeping all other hyperparameters constant (n_steps = 2048, batch_size = 256, 8 parallel environments, and 1,000,000 timesteps).

With the standard learning rate (3e-4), the agent failed to learn entirely—every evaluation episode returned a total reward of −200, the worst possible score. This shows that the updates were too small to meaningfully change the policy within the training budget.

In contrast, the aggressive learning rate (3e-3) produced a successful policy. The evaluation rewards were- 6, 6, 6, 9, 9, 7, 11, 8, 8, 6

with a mean reward of 7.60 ± 1.62, and episode lengths of 10–15 steps, demonstrating consistent successful pickups and dropoffs.

Overall, increasing the learning rate significantly improved convergence. The standard LR was too conservative to escape poor initial behavior, while the aggressive LR allowed PPO to learn an effective policy much faster without causing instability.
