# Reinforcement Learning Playground for Beginners

Author: Ran Zhu @ Southeast University, China; State Grid NARI Group Corporation, China

Email: gemina_cat@163.com

--------------------------------------------------
This repository is still under construction. Till now, the following algorithms are included:
- [x] Classical Value-based Algorithms: [Sarsa], [Q-Learning]
- [x] Value Function Approximation Algorithms: [Naive Q-Learning with neural network (Naive Q_nn)], [Naive Q_nn with replay buffer],[Vanilla DQN]
- [x] Classical Policy-based Algorithms: [REINFORCE] [QAC]

Besides, this repository is created to relax myself (and to learn something interesting) because of the pressure of my PhD study. I will update it sporadically. If you have any questions, please contact me via email.

In the future, I will add more algorithms, such as policy-based algorithms, actor-critic algorithms, offline RL algorithms including several applications of RL in power distribution systems.

## 1. Introduction
This repository is a playground for beginners to learn reinforcement learning. It is a collection of simple environments and agents to get you started with reinforcement learning. Each algorithm is implemented in a single ipynb file with less than 500 lines of code, which written in pytorch and based on the latest gymnasium. The goal of this project is to provide a simple and clear implementation for each algorithm.

If you have already known basic concepts and mathematical notations of reinforcement learning but have no idea how to implement them, this repository is for you. If you are a beginner of reinforcement learning, I recommend you to learn the basic concepts and mathematical notations first. 

## 2. Features
- **Smoothly from Maths to Codes:** The names of variables and functions are consistent with the core sprits of each RL algorithm. The main sloop of each algorithm is also consistent with the pseudo code in the textbook.
- **No Programming Tricks But Just Algorithms:** There is no programming tricks (at least I think so) in the codes. Everything is simplified as much as possible to help you understand the core idea of each algorithm.
- **Clear Implementation:** The coding style and core architecture refer to the pfrl library which has a clear structure. I think the "pfrl-style" is a good choice for beginners to learn reinforcement learning. 
- **Modular Unified Architecture:** Each code file has a similar structure. You can easily modify the code to implement your own algorithm.

## 3. Requirements
All the dependencies are the current stable versions, so you don't need to worry about the compatibility. 
All the codes are tested on the following environment:
- python == 3.8
- pytorch == 2.0
- gymnasium == 0.28
- numpy == 1.24
- matplotlib == 3.2
- pandas == 2.0

## 4. Thanks
I would like to thank Dr.Zhao for his unselfish sharing of the course materials (https://www.bilibili.com/video/BV1sd4y167NS/). 
I would also like to thank the authors of the following repositories:
- [A clear RL tutorial for beginners using pure pytorch] https://github.com/rexrex9/reinforcement_torch_pfrl
- [A powerful DRL library based on pytorch] https://github.com/pfnet/pfrl
- [Codes of David Silver's RL Course] https://github.com/dennybritz/reinforcement-learning
