# Leaky Integrate-and-Fire (LIF) Neuron
This is a simple computational neuroscience project implementing and exploring the LIF neuron as a part of _Neuromatch Academy_ Tutorial. I will implement something extra to the tutorial (i.e. Excitatory vs. Inhibitory neurons..)

The goal of this project is to:
- Practice basic Python scripting in neuron modeling
- Understand the LIF membrane equation
- Simulate membrane potential dynamics under different input currents
- Explore how parameters (τₘ, R, Vₜₕ, V_reset, E_L) affect spiking behavior
- Visualize neuron firing patterns

Although individual neuronal activity matters, most of the research labs focus on viewing the brain as a whole! However, that will implement more complex computation which is beyond my knowledge for now XD. This is my first repository and modeling practice so I will start by stimulating one single neuron and hopefully I will be able to model brain-wide activity in the future!

## Electrophysiology? It's all just physics..
The ionic equivalent of conductance is **ion channels**
- conductance is a measure of permeability to ionic flux
- conductance = the current carried by that ion divided by its “driving force”, where driving force = (Vm - Ex)

The ionic equivalent of voltage is **driving force**. Driving force is "How badly ions want to flow through" 
- The driving force is the difference between the membrane potential (Vm) and the ion’s equilibrium (Nernst) potential.

The ionic equivalent of capacitance is the **hydrophobic plasma membrane itself**
- membrane can be charged and discharged.

The neuron can also be modeled as a resistor 
- High membrane resistance: less leak across the membrane, signal stays stronger.

## The LIF membrane equation
<img width="240" height="64" alt="image" src="https://github.com/user-attachments/assets/6236a6b4-5e43-4be7-89d7-4e382ecbd163" />

The membrane equation describes the time evolution of membrane potential in response to synaptic input and leaking of charge across the cell membrane

I'll try to break this equation down using the knowledge obtained in NSCI200 at McGill (Dr. Ruthazer section specifically):
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
