# Autonomous Production Optimization via Deep Reinforcement Learning 🤖🏭

This project implements a discrete-event production system simulation to evaluate and compare classical control policies against state-of-the-art **Deep Reinforcement Learning (DRL)** agents. By wrapping a **SimPy** discrete-event simulation into a **Gymnasium** environment, the agents optimize job release strategies from a Pre-Shop Pool (PSP) to minimize Work-In-Process (WIP) and tardiness.

## 🔬 Project Overview
This system models a multi-machine manufacturing floor with stochastic job arrivals and complex routing. The goal is to move beyond static "PUSH" policies by using intelligent agents that decide the optimal timing and quantity of job releases based on real-time shop floor state.

## 🛠 Core Engineering

* **Discrete-Event Simulation (SimPy):** Models 6 machines, 3 job families with Gamma-distributed processing times, and Poisson arrival rates.
* **Custom Gymnasium Environment:** Features a 7-dimensional normalized observation space and a multi-objective reward function designed to balance throughput vs. lean operations.
* **Deep RL Framework:** Built using **Stable-Baselines3**, comparing **PPO** (Proximal Policy Optimization) with vectorized environments and **DQN** (Deep Q-Network).

## 📊 Performance Benchmarking

The agents were evaluated against a **PUSH Baseline** (immediate job release). The PPO agent, in particular, demonstrated superior capability in reducing system congestion while meeting production targets.

### Comparative Results
![Detailed Performance Results](media/graphical_results.png)

| Policy | Throughput | Avg WIP | Avg Tardiness | Performance |
| :--- | :---: | :---: | :---: | :--- |
| **PUSH** | 0.599 | 21.11 | 6.76 | Baseline |
| **DQN** | 0.600 | 21.56 | 7.13 | Stable |
| **PPO** | **0.603** | **16.85** | **3.02** | **Optimal** |

**Key Findings:**
* **55% Reduction in Tardiness:** The PPO agent learned to prioritize jobs effectively, drastically reducing late deliveries.
* **20% Reduction in WIP:** The system maintains a leaner shop floor, reducing holding costs without sacrificing throughput.
* **Production Stability:** Both RL agents maintained or slightly exceeded the target throughput of 0.60 jobs/time-unit.

## 📂 Project Structure
* `notebooks/`: Interactive Google Colab sessions with training logs and visualizations.
* `src/`: Clean Python implementation of the simulation engine and RL environment.
* `media/`: High-resolution performance plots and benchmarking graphics.

## 🛠 Tech Stack
* **Language:** Python
* **Libraries:** SimPy, Gymnasium, Stable-Baselines3, NumPy, Matplotlib
