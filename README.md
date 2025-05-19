# Chemical Reactor Temperature Control with TASAC Reinforcement Learning

## Project Overview
This project implements a reinforcement learning approach for controlling the temperature of a batch chemical reactor. Using a **Twin Actor Soft Actor-Critic (TASAC)** architecture, the system learns to follow temperature trajectories by manipulating coolant flow rates — crucial for ensuring product quality and process safety in chemical manufacturing.

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
Temperature control in batch reactors presents significant challenges due to the **nonlinear dynamics**, **exothermic reactions**, and **time-varying behavior** of chemical processes. Traditional PID controllers often struggle with these complexities, especially when following specific temperature trajectories. This project demonstrates how **reinforcement learning** can address these challenges by learning optimal control policies directly from process data.

---

## Features
- Reinforcement learning-based temperature controller using **TASAC**
- **Multiple-Input Single-Output (MISO)** control strategy
- Custom **OpenAI Gym** environment for reactor simulation
- Realistic **batch reactor model** with exothermic reaction dynamics
- **Experience replay buffer** for stable training
- **Visualization tools** for performance analysis

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
```bash
# Clone the repository
git clone https://github.com/yourusername/reactor-control-rl.git
cd reactor-control-rl

# Install dependencies
pip install -r requirements.txt
