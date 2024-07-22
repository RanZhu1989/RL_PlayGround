# Offline Reinforcement Learning

## Intro
Offline reinforcement learning (RL) is also known as batch RL. The morden offline RL is first proposed by Fujimoto, as a pre-train method, to avoid the massive destructive failures during the initial interaction stage. Such deadly failures lead to high 'interaction cost' in many industrial applications (e.g, power systems). Thus, offline RL is deducted to learn from a historical Markov decision process (MDP) dataset ($\mathcal{D} = \{\mathbf{s}, \mathbf{a}, \mathbf{s}^{\prime}, \mathbf{r} \}_i$), without interacting with the environment.

The reason why we list offline RL as a separate category can be summarized as follows:
- *Compared to off-policy algorithms:* It is hard to implement offline RL via the conventional off-policy algorithms. These off-policy algorithms are online learning implementations, which can evaluate state values which are not encountered by interacting with the environment. However, the offline RL is a different story. The values of the unseen states should be **inferred** by the agent via its inherent mechanism (data-driven, knowledge-driven, or hybrid).
- *Compared to imitation learning:* Offline RL can 'pick' good actions from the data, and try to **improve** the policy behind the data ($\pi_{\beta}$). In the contract, imitation learning can only mimic the expert's behavior with respect to the supervised learning paradigm (the agent does not know **why** the expert takes such actions). Moreover, offline RL can learn from different data and combine the good actions from different experts to develop a new 'best' policy. In contrast, imitation learning can only regress according to different datasets.

The core challenge of the offline RL is *distribution shifting* mainly caused by 1) the limitation of the dataset, 2) complexity of the state transition of the environment, and 3) the difference between $\pi_{off}$ and $\pi_{\beta}$. The distribution shifting problem can be described from both policy optimization and value estimation aspects.

- *Policy Optimization*
The offline RL problem can be set to maximize the performance metric of average value
$$
V^\pi\left(s_t\right) \doteq \mathbb{E}_{\tau \sim p_\pi\left(\cdot \mid s_t\right)}\left[\sum_{t'=t}^{T} \gamma^{t-t'} r_t\right].
$$
$\pi$ is the policy to learnt offline. $\tau = \{s_0, a_0, s_1, a_1, \dots, s_{T-1}, a_{T-1}, s_T\}$ is the trajectory. $p_\pi\left(\cdot \mid s_t\right)$ is the trajectory distribution under policy $\pi$. This expectation is easy to be calculated when $\tau$ is constrained in the dataset $\mathcal{D}$. However, the agent may encounter the state out of the dataset, i.e., $s_t,a_t \rightarrow s_{t+1} \notin \mathcal{D}$. The distribution of $\tau$ is shifted from the dataset and called *distribution shifting*. This indicates one can constraint the state and action in the dataset.

- *Value Estimation*
Solving the bellman equation for estimating the Q function $Q_{\phi}$ is the core idea of the value-based RL algorithms. Consider the following SARSA-like temporal-difference (TD) to minimize the TD error 
$$
\mathbb{E}_{s, a, s^{\prime} \sim \mathcal{D}}\left[Q_{\phi}(s, a)-r(s, a)- \gamma \mathbb{E}_{a^{\prime} \sim \pi_{off}(\cdot \mid s)} Q_{\phi}\left(s^{\prime}, a^{\prime}\right)\right].
$$
The outer expectation is on the expected trajectory in the dataset, while the inner expectation is on the to-learnt offline policy. One can expect that $\pi_{off} = \pi_{\beta}$ so that the value can be accurately estimated. However, the learned policy can be never improved. In other words, this is not real offline RL. On the other hand, if $\pi_{off} \neq \pi_{\beta}$, the distribution shifting occurs. Directly using the stochastic gradient descent to minimize the TD error can lead to mis-estimate of the Q function. Even if we can accurately estimate the Q function, the trajectory may still be out of the dataset due to the difference of the two policies. It indicates that $\pi_{off}$ should be not too far from $\pi_{\beta}$ once executing the value estimation.