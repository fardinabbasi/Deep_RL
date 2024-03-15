# Deep RL
## Acrobot Environment
### Description
The [acrobot environment](https://www.gymlibrary.dev/environments/classic_control/acrobot/) is a system consisting of two links connected linearly to form a chain, with one end of the chain fixed. The joint between the two links is actuated. The goal is to apply torques on the actuated joint to swing the free end of the linear chain above a given height while starting from the initial state of hanging downwards.

**Action Space**

The action is discrete, deterministic, and represents the torque applied on the actuated joint between the two links.
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
| 4 | Angular velocity of $\theta_1$ | $$~ -12.567(4 \times \pi)$$ | $$~ 12.567(-4 \times \pi)$$ |
| 5 | Angular velocity of $\theta_2$ | $$~ -28.274 (9 \times \pi)$$ | $$~ 28.274 (9 \times \pi)$$ |

_where_
* $\theta_1$ is the angle of the first joint, where an angle of 0 indicates the first link is pointing directly downwards.
* $\theta_2$ is relative to the angle of the first link. An angle of 0 corresponds to having the same angle between the two links.

**Rewards**

The goal is to have the free end reach a designated target height in as few steps as possible, and as such all steps that do not reach the goal incur a reward of -1. Achieving the target height results in termination with a reward of 0. The reward threshold is -100.

# References
* Sutton, R. S., & Barto, A. G. (2018). Reinforcement Learning, second edition: An Introduction. MIT Press.
* [Dueling DQN](https://wikidocs.net/174647) - EN. (n.d.-b). 위키독스.
* ChienTeLee. (n.d.-b). GitHub - ChienTeLee/dueling_dqn_lunar_lander. [GitHub](https://github.com/ChienTeLee/dueling_dqn_lunar_lander).
* Cyoon. (n.d.-d). GitHub - cyoon1729/deep-Q-networks: Implementations of algorithms from the Q-learning family. Implementations inlcude: DQN, DDQN, Dueling DQN, PER+DQN, Noisy DQN, C51. [GitHub](https://github.com/cyoon1729/deep-Q-networks).
