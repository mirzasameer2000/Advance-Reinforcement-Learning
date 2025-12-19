# Mouse & Cheese (Unity ML-Agents Reinforcement Learning)
Unity + AI Implementation

A Unity **Reinforcement Learning** project where a mouse agent learns to **avoid traps** and **collect cheese** using **Unity ML-Agents**.  
The environment resets when the mouse hits a trap, touches boundary walls, or finishes an episode. After every successful collection, the cheese **respawns at a random position**, encouraging robust exploration.

This project uses **PPO (Proximal Policy Optimization)** with a **Ray Perception Sensor 3D** for observations and **TensorBoard** for training analytics.

---

## Key Features

- 🐭 **RL Agent (PPO)** learns a movement policy to reach cheese while avoiding traps  
- 🧀 **Randomized cheese respawn** after each success / episode reset  
- 🪤 **Trap avoidance**: hitting a trap triggers reset (and can apply a penalty)  
- 🧱 **Boundary reset**: touching walls/boundaries resets the episode  
- ⚡ **16 parallel environments** to speed up training (faster experience collection)  
- 📊 **TensorBoard summaries** for rewards and training diagnostics  
- 🎮 Unity components used:
  - Box Collider, Rigidbody  
  - Behavior Parameters  
  - Decision Requester  
  - Animator  
  - Ray Perception Sensor 3D  

---

## Environment Logic (High Level)

### Episode Reset Conditions
- Mouse hits **Trap** ➜ reset episode  
- Mouse hits **Boundary/Wall** ➜ reset episode  
- Episode ends (time limit / max steps) ➜ reset episode  

### Success Condition
- Mouse touches **Cheese** ➜ reward + regenerate cheese at a random position  

---

## Project Structure

### Main C# Scripts
- `MoveToGoalAgent.cs`  
  Implements the ML-Agents `Agent` logic: observations, actions, rewards, and resets.
- `Goal.cs`  
  Cheese logic: collision detection and random respawn.
- `Trap.cs`  
  Trap collision logic: triggers reset.
- `Wall.cs`  
  Boundary collision logic: triggers reset if the agent touches limits.
- `Obstacle.cs`  
- `UIManager.cs`  
  Updates UI elements (e.g., cheese counter).

### Training Config
- `moveToGoal.yaml`  
  PPO trainer configuration used to train the agent.

---

## Requirements

- **Unity** (Unity 6 / recent Unity versions recommended)
- **Unity ML-Agents** package installed
- Python environment for training:
  - `mlagents`
  - `torch`
  - `tensorboard`

> Tip: Using **conda** or a dedicated venv is recommended for clean setup.

---
## Project Link

https://drive.google.com/file/d/19lQ6CKptjHOKXJVsN27biu8mQjDuKuUr/view?usp=sharing

## How to Train

1) Open the Unity project  
2) Ensure each training environment contains:
   - `Behavior Parameters` with **Behavior Name** set to: `MoveToGoal`
   - `Decision Requester` enabled (or manual decisions via script)
   - `Ray Perception Sensor 3D` configured to detect cheese/traps/walls
3) Run training from terminal:

```bash
mlagents-learn moveToGoal.yaml --run-id=MoveToGoal --time-scale=20 --train



