# Deep Reinforcement Learning
In many practical decision-making problems, the states $s$ of the MDP are **high-dimensional** and cannot be solved by traditional RL algorithms. Deep reinforcement learning algorithms incorporate deep learning to solve such MDPs, often representing the policy $\pi(a|s)$ or other learned functions as a neural network and developing specialized algorithms that perform well in this setting.
## Acrobot Environment
### Description
The [acrobot environment](https://www.gymlibrary.dev/environments/classic_control/acrobot/) is a system consisting of two links connected linearly to form a chain, with one end of the chain fixed. The joint between the two links is actuated. The goal is to apply torques on the actuated joint to swing the free end of the linear chain above a given height while starting from the initial state of hanging downwards.

**Action Space**

The action is **discrete**, **deterministic**, and represents the torque applied on the actuated joint between the two links.
| Num | Action | Unit |
| --- | --- | --- |
| 0 | apply -1 torque to the actuated joint | torque (N.m) |
| 1 | apply 0 torque to the actuated joint | torque (N.m) |
| 2 | apply 1 torque to the actuated joint | torque (N.m) |

**Observation Space**

The observation provides information about the two rotational joint angles as well as their angular velocities:
| Num | Observation | Min | Max|
| --- | --- | --- | --- |
| 0 | $$cos(\theta_1)$$ | -1 | 1 |
| 1 | $$sin(\theta_1)$$ | -1 | 1 |
| 2 | $$cos(\theta_2)$$ | -1 | 1 |
| 3 | $$sin(\theta_2)$$ | -1 | 1 |
| 4 | Angular velocity of $\theta_1$ | $$~ -12.567(4 \times \pi)$$ | $$~ 12.567(4 \times \pi)$$ |
| 5 | Angular velocity of $\theta_2$ | $$~ -28.274 (9 \times \pi)$$ | $$~ 28.274 (9 \times \pi)$$ |

_where_
* $\theta_1$ is the angle of the first joint, where an angle of 0 indicates the first link is pointing directly downwards.
* $\theta_2$ is relative to the angle of the first link. An angle of 0 corresponds to having the same angle between the two links.

**Rewards**

The goal is to have the free end reach a designated **target height** in as few steps as possible, and as such all steps that do not reach the goal incur a reward of -1. Achieving the target height results in termination with a reward of 0.
## Deep Q-Learning (DQN)
The problem with traditional Q-learning is that the size of the Q-table grows exponentially with the number of states and actions, making it impractical for many problems. To address this, deep Q-learning (DQN) was introduced, which uses a **neural network** to approximate the Q-values. As a universal function approximator, the neural network is able to capture the relationships between states and actions more efficiently than the Q-table.
<img src="/readme_images/DQL.png" width="1293" height="586">

However, one issue with using a neural network to learn the Q-values is that the **update rule depends on the values produced by the network itself**, which can make **convergence difficult**. To address this, the DQN algorithm introduces the use of a **replay buffer** and **target networks**. The replay buffer stores past interactions as a list of tuples, which can be sampled to update the value and policy networks. This allows the network to learn from individual tuples multiple times and reduces dependence on the current experience. The target network is a **time-delayed copy** of the Q-network, and its parameters are updated according to the following equation:
$$\theta_\hat{Q} = \tau \times \theta_Q + (1-\tau)\theta_\hat{Q}$$
The pseudocode of the DQN algorithm is written as follows:

<img src="/readme_images/DQN_pseudocode.png" width="1131" height="742">
The trainig results for the DQN agent are depicted below.

| Reward Plot | Video |
| --- | --- |
| <img src="/readme_images/DQN_r.png"> | <img src="/readme_images/DQN.gif"> |
## Dueling Deep Q-Learning (Dueling DQN)
The dueling DQN algorithm seeks to improve upon traditional DQN by decomposing the Q-values into two separate components: the **value function**, $V(s)$, and the **advantage function**, $A(s,a)$. The value function represents the expected reward for a given state, s, while the advantage function reflects the relative advantage of taking a particular action, a, compared to other actions. By combining these two functions, it is possible to compute the full Q-values for each state-action pair.

<img src="/readme_images/Duel_arch.png">
To implement this decomposition, the dueling DQN algorithm introduces a neural network with two separate output layers, one for the value function and one for the advantage function. These outputs are then combined to produce the final Q-values. This modification allows the network to learn more efficiently in situations where the exact values of individual actions are not as important, as it can focus on learning the value function for the state.

$$Q(s,a) = V(s) +(A(s,a)- \frac{1}{|A|}\sum_a A(s,a))$$
The trainig results for the Dueling DQN agent are depicted below.

| Reward Plot | Video |
| --- | --- |
| <img src="/readme_images/Duel_r.png"> | <img src="/readme_images/Dueling-DQN.gif"> |
# References
* Sutton, R. S., & Barto, A. G. (2018). Reinforcement Learning, second edition: An Introduction. MIT Press.
* [Dueling DQN](https://wikidocs.net/174647) - EN. (n.d.-b). 위키독스.
* ChienTeLee. (n.d.-b). GitHub - ChienTeLee/dueling_dqn_lunar_lander. [GitHub](https://github.com/ChienTeLee/dueling_dqn_lunar_lander).
* Cyoon. (n.d.-d). GitHub - cyoon1729/deep-Q-networks: Implementations of algorithms from the Q-learning family. Implementations inlcude: DQN, DDQN, Dueling DQN, PER+DQN, Noisy DQN, C51. [GitHub](https://github.com/cyoon1729/deep-Q-networks).
* Tutorial: [From Tabular Q-Learning to DQN](https://araffin.github.io/slides/dqn-tutorial/). (n.d.).
* Acrobot - [Gym Documentation](https://www.gymlibrary.dev/environments/classic_control/acrobot/). (n.d.).
