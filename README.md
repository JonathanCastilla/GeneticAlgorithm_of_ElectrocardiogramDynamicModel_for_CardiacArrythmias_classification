# 💓 Genetic Algorithm for ECG Dynamic Model & Arrhythmia Classification
### November 2023 – December 2023
### Tools: 
- MATLAB, 
- Python, 
- STM32, 
- Neural Networks
### 👨‍💻 Authors: 
- K. Alvarez, 
- A. Becerra, 
- J. Castilla, 
- G. López, 
- M. Ortiz, 
- A. Robellada, 
- R. Romero, 
- K. Villeda

---

## 🧭 Overview
This project implements a **Genetic Algorithm (GA)** to optimize the parameters of a dynamic mathematical model representing the human Electrocardiogram (ECG). The goal was to accurately synthesize ECG signals that match real-world patient data and use these synthetic parameters to classify cardiac conditions—specifically distinguishing between **Bradycardia** (resting state) and **Tachycardia** (post-exercise state).

The system integrates hardware for signal acquisition (STM32) with advanced software processing (GA optimization and Neural Networks) to identify patterns in cardiac rhythms.

---

## 🧠 Features
- **Genetic Algorithm (GA) Optimization**:
  - Implemented in MATLAB with operators for **Mutation (prob=0.8)**, **Crossover**, and **Elitism**.
  - Optimizes 21 synthetic parameters of a system of Differential Equations (ODEs) to fit acquired patient signals.
- **Dynamic ECG Modeling**:
  - Models the ECG using a set of 3 coupled Ordinary Differential Equations (ODEs) representing the cardiac trajectory in 3D space $(x, y, z)$.
  - Captures complex P, Q, R, S, and T wave dynamics.
- **Pattern Recognition (Neural Networks)**:
  - **Model A (Dynamic Parameters):** achieved **100% accuracy** in distinguishing rest vs. exercise states using the optimized parameters.
  - **Model B (Ordinary Equations):** achieved **87.11% accuracy**.
- **Hardware Integration**:
  - Signals acquired using **STM32 microcontrollers** and custom analog filter boards (Butterworth/Chebyshev) from 128 test subjects.

---

## ⚙️ Methodology
1. **Data Acquisition**:
   - Collected ECG data from 128 subjects in two states: **Rest** (simulating Bradycardia-like lower rates) and **Post-Exercise** (simulating Tachycardia).
   - Total records: 256 signals.
2. **Signal Preprocessing**:
   - Analog filtering (Butterworth) to remove noise.
   - Normalization and segmentation of cardiac cycles.
3. **Evolutionary Optimization**:
   - The GA searches for the optimal set of parameters ($a_i, b_i, \theta_i$) that minimize the error between the synthetic ODE model and the real patient signal.
   - **Population:** 100 individuals | **Generations:** 50.
4. **Classification**:
   - The extracted synthetic parameters serve as the input feature vector for a Dense Neural Network.
   - **Architecture:** Input (16) $\rightarrow$ Hidden (40) $\rightarrow$ Hidden (80) $\rightarrow$ Hidden (40) $\rightarrow$ Output (2: Rest/Exercise).

---

## 📊 Results & Performance
The project compared different modeling approaches, finding that the Dynamic ODE model combined with GA provided superior features for classification.

- **Dynamic Model Classification**:
  - **Accuracy:** **100%** (Perfect separation of classes).
  - Validated over 1000 training epochs.
- **Fourier Synthetic Model**:
  - Attempted to model signals using Fourier Series (30 components).
  - **Result:** Discarded due to poor convergence and inability to capture realistic ECG morphology compared to the ODE model.
- **Ordinary Equation Model**:
  - **Accuracy:** 87.11%.
  - Showed signs of overfitting compared to the robust Dynamic Model.

---

## 🛣️ Mathematical Foundation
The core trajectory is defined by the following differential system:

$$
 \dot{x} = \alpha x - \omega y
$$

$$
\dot{y} = \alpha y + \omega x
$$

$$
 \dot{z} = -\sum a_i \Delta \theta_i \exp\left(-\frac{\Delta\theta_i^2}{2b_i^2}\right) - (z - z_0) 
$$

Where $z$ represents the ECG amplitude, and parameters $a_i, b_i, \theta_i$ control the shape of the P-Q-R-S-T waves.

---

## 📘 Documentation
Includes full academic PDF report: *documentation.pdf*.
The report contains the specific ODE derivations, the "plano-fase" (phase plane) analysis, and training loss graphs.

---

## 📚 References
- McSharry et al. — *A dynamical model for generating synthetic electrocardiogram signals*.
- STM32 Hardware Documentation.
- Neural Network Design Principles (Keras/TensorFlow).

---

## © License
Academic and personal use permitted.