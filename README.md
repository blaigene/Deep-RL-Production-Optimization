# Autonomous Production Optimization via Deep Reinforcement Learning 🤖🏭

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This project implements a discrete-event production system simulation to evaluate and compare classical control policies against state-of-the-art **Deep Reinforcement Learning (DRL)** agents. By wrapping a **SimPy** discrete-event simulation into a **Gymnasium** environment, the agents optimize job release strategies from a Pre-Shop Pool (PSP) to minimize Work-In-Process (WIP) and tardiness.

## 🧠 AI & Reinforcement Learning Implementation
To solve the stochastic job-shop scheduling challenge, the system was modeled as a Markov Decision Process (MDP) with the following technical specifications:

* **State Space (7D Observation Vector):** Normalized metrics including current WIP levels, PSP backlog size, machine utilization rates, real-time throughput, and episode time progress.
* **Action Space:** Discrete control allowing the agent to decide the exact number of jobs (0 to $K$) to release from the pool at each decision point.
* **Reward Engineering:** A multi-objective function designed to balance competing KPIs:
    * **Incentives:** Positive rewards for job completion.
    * **Penalties:** Weighted penalties for WIP accumulation, PSP overflow, and system lateness.
    * **Advanced Shaping:** Implementation of terminal shortfall penalties to provide a strong episode-level signal for PPO stability.
* **Algorithms:** Comparative study between **PPO** (On-policy) using vectorized environments and **DQN** (Off-policy) with experience replay. 



## 🔬 Project Overview
This system models a multi-machine manufacturing floor with stochastic job arrivals and complex routing. The goal is to move beyond static "PUSH" policies by using intelligent agents that decide the optimal timing and quantity of job releases based on real-time shop floor state.

## 🛠 Core Engineering
* **Discrete-Event Simulation (SimPy):** Models 6 machines, 3 job families with Gamma-distributed processing times, and Poisson arrival rates.
* **Architecture:** Built using **Stable-Baselines3**, utilizing `VecNormalize` for observation and reward scaling to ensure gradient stability.

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

---
**Author:** Blai Gené Mora  
**Institution:** Universitat de Lleida (UdL) / Università degli Studi di Modena e Reggio Emilia (UNIMORE)
