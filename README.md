# Chemical Reactor Temperature Control with TASAC Reinforcement Learning

## Project Overview
This project implements a reinforcement learning approach for controlling the temperature of a batch chemical reactor. Using a **Twin Actor Soft Actor-Critic (TASAC)** architecture, the system learns to follow temperature trajectories by manipulating coolant flow rates, crucial for ensuring product quality and process safety in chemical manufacturing.

![image alt](https://github.com/Kritika896/TASAC/blob/main/result.png?raw=true)

---

## Table of Contents
- [Background](#background)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [The Science Behind It](#the-science-behind-it)
  - [Batch Reactor Model](#batch-reactor-model)
  - [MISO Control Strategy](#miso-control-strategy)
  - [TASAC Reinforcement Learning](#tasac-reinforcement-learning)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

---

## Background
Temperature control in batch reactors presents significant challenges due to the nonlinear dynamics, exothermic reactions, and time-varying behavior of chemical processes. Traditional PID controllers often struggle with these complex dynamics, especially when following specific temperature trajectories. This project demonstrates how reinforcement learning can address these challenges by learning optimal control policies directly from process data.

---

## Features
- Reinforcement learning-based temperature controller using TASAC  
- Multiple-Input Single-Output (MISO) control strategy  
- Custom OpenAI Gym environment for reactor simulation  
- Realistic batch reactor model with exothermic reaction dynamics  
- Experience replay buffer for stable training  
- Visualization tools for performance analysis  

---

## Requirements
- Python 3.7+  
- PyTorch 1.7+  
- NumPy  
- Pandas  
- Matplotlib  
- SciPy  
- OpenAI Gym  
- scikit-learn  

---

## Installation 
# Clone the repository
git clone https://github.com/yourusername/reactor-control-rl.git
cd reactor-control-rl

# Install dependencies
pip install -r requirements.txt

## Usage
bash
Copy
Edit
# Train the TASAC controller
python train_controller.py

# Evaluate the controller performance
python evaluate_controller.py

# Run visualization
python visualize_results.py
The Science Behind It
Batch Reactor Model
The project uses a first-principles model of a batch reactor with an exothermic reaction. The model is described by a set of differential equations:

python
Copy
Edit
def br(x, t, u, Ad, heater):
    F = u * 16.667
    Ii, M, Tr, Tj = x
    Ri = Ad * Ii * (np.exp(-140.06e3 / (8.3145 * (Tr + 273.15))))
    Rp = (1.7e11 / 60) * (Ii ** 0.5) * (M ** 1.25) * np.exp(-16.9e3 / (0.239 * 8.3145 * (Tr + 273.15)))
    mrCpr = 450 * 4.184 + Ii * 187 * 0.5 + M * 110.58 * 0.5 + (0.7034 - M) * 84.95 * 0.5 + 220 * 0.49 + 7900 * 0.49
    Qpr = 1.212827 * (Tr - 27) ** 0.000267 + heater

    dy1_dt = -Ri  # Rate of initiator consumption
    dy2_dt = -Rp  # Rate of monomer consumption
    dy3_dt = (Rp * 0.5 * -82.2e3 - 33.3083 * (Tr - Tj) + 650 + 12.41e-2 - Qpr) / mrCpr  # Reactor temperature
    dy4_dt = (33.3083 * (Tr - Tj) - F * 4.184 * (Tj - 27)) / ((18 * 4.184) + (240 * 0.49))  # Jacket temperature

    return [dy1_dt, dy2_dt, dy3_dt, dy4_dt]
Variables:

Ii: Initiator concentration

M: Monomer concentration

Tr: Reactor temperature

Tj: Jacket (cooling) temperature

F: Coolant flow rate

Ri: Rate of initiator consumption

Rp: Rate of polymerization

Qpr: Heat generated by the reaction

MISO Control Strategy
The Multiple-Input Single-Output (MISO) approach simplifies the control problem while maintaining effectiveness:

Inputs: Reactor temperature (Tr), setpoint temperature, and temperature difference (error)

Output: Coolant flow rate (manipulated variable)

This strategy reduces the complexity of the control policy while still capturing the essential dynamics for effective temperature control.

TASAC Reinforcement Learning
Twin Actor Soft Actor-Critic (TASAC) is an advanced reinforcement learning algorithm particularly well-suited for continuous control problems:

Actor-Critic Architecture:
Actor: Determines the control action (coolant flow rate)

Critics: Two Q-networks that evaluate the quality of state-action pairs

Soft Policy Updates:
Entropy regularization encourages exploration

Provides robustness against environmental uncertainties

Twin Critic Approach:
Uses two critic networks to reduce overestimation bias

Takes the minimum Q-value for more conservative policy updates

Experience Replay:
Stores experiences in a buffer to break correlations between consecutive samples

Improves sample efficiency and learning stability
![image alt]()
Key Equations:
Policy Network: π(a|s) - Determines the probability of taking action a in state s

Q-Function: Q(s,a) - Estimates the expected return from taking action a in state s

Value Function: V(s) - Estimates the expected return from state s


## Results
# The TASAC controller successfully learns to follow temperature trajectories with high accuracy. Performance metrics include:
![image alt](https://github.com/Kritika896/TASAC/blob/main/result.png?raw=true)

Low mean squared error between actual and reference temperatures

Smooth control actions without excessive oscillations

Quick response to setpoint changes

Robustness to process disturbances

Visual results showing temperature tracking and control actions are available in the results/ directory.
