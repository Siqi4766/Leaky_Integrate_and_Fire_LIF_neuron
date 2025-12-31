# Intro
This is a computational neuroscience project implementing and exploring the **Leaky Integrate-and-Fire (LIF)** neuron model. It was developed as a comprehensive summary of the key concepts from the _Neuromatch Academy_ Tutorial (specifically W0D1 and W0D2). While _Neuromatch_ provides step-by-step guidance, I consolidates those steps into a object-oriented Python simulation (`LIFNeurons` class).

The goal of this project is to:
- Practice basic Python scripting in neuron modeling
- Understand the LIF membrane equation
- Simulate membrane potential dynamics under different input currents
- Explore how parameters (τₘ, R, Vₜₕ, V_reset, E_L) affect spiking behavior
- Visualize neuron firing patterns 

This is the first model I built, welcome to point out any bugs / algorithms to be optimized!

# The LIF Membrane Equation
<img width="240" height="64" alt="image" src="https://github.com/user-attachments/assets/6236a6b4-5e43-4be7-89d7-4e382ecbd163" />

The membrane equation describes the time evolution of membrane potential in response to synaptic input and leaking of charge across the cell membrane

- E_L: resting membrane potential (~ -70 mV)
- R: membrane resistance
- I(t): input current (amps or pA).
- τₘ: membrane time constant (seconds or ms), τₘ describes how fast the membrane potential changes in response to a current. τₘ is also the time to charge membrane to 63% of Vmax (governs temporal summation).
  - τₘ = rm (membrane resistance) x Cm (membrane capacitance)
  - Large τ = good temporal summation.
  - Small τ = poor temporal summation.
  - τ decides whether inputs in time can add together.
- on the left side of equation it's the derivative of V in terms of t = how membrane potential (in volts) changes over time
- Leak term <img width="62" height="42" alt="Screenshot 2025-11-29 at 5 09 40 PM" src="https://github.com/user-attachments/assets/abc235c8-89d8-42c7-a124-674f83fc1286" />: if V is above resting membrane potential, this term is negative and pulls V back down exponentially with time constant τₘ
- Input term <img width="59" height="38" alt="Screenshot 2025-11-29 at 5 13 55 PM" src="https://github.com/user-attachments/assets/02034c3c-42d7-4af0-84f8-64dbd3bdf190" />: drives the membrane toward a new steady voltage proportional to input current.

Note that when the membrane potential crosses threshold, the differential equation STOPS being applied!! V will reset once threshold is reached.

# Random Synaptic Input Equation
<img width="622" height="122" alt="image" src="https://github.com/user-attachments/assets/6a841548-fa71-44e1-b8e4-5f54651dc41c" />

# Neuron as binary number?
We can treat an action potential (spike) represents 1 and resting state represents 0. Then we can plot these 0 and 1 into a binary raster plot that:
- graphically represent of the precise times at which one or more neurons fire an action potential (spike) over a period of time. 
