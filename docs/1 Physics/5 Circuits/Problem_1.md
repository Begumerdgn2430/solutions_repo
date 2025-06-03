# Problem 1

# 🔌 Circuit Analysis Exercise: [Exercise Title]

##  Objective

Briefly describe the goal of the exercise. For example:
- Analyze the behavior of an RC circuit over time.
- Determine the current and voltage across components in an RLC circuit.

##  Problem Statement

Provide a detailed description of the circuit problem, including:
- The type of circuit (e.g., series, parallel, RLC).
- Given values (e.g., resistance, capacitance, inductance, voltage sources).
- What needs to be calculated or analyzed.

## Circuit Diagram

Include a schematic of the circuit. You can use tools like [Circuitikz](https://www.overleaf.com/learn/latex/Circuitikz_package) for LaTeX or embed an image:

![Circuit Diagram](path_to_circuit_image.png)

## Theoretical Background

Discuss the relevant theories and formulas:
- Ohm's Law
- Kirchhoff's Laws
- Differential equations governing the circuit behavior

##  Calculations

Show step-by-step calculations:
1. Apply Kirchhoff's Voltage and Current Laws.
2. Solve the differential equations.
3. Calculate the desired quantities (e.g., current, voltage, impedance).

##  Simulation

If applicable, include a simulation of the circuit using Python:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define parameters
R = 1000  # Resistance in ohms
C = 1e-6  # Capacitance in farads
V0 = 5    # Initial voltage in volts

# Time array
t = np.linspace(0, 0.01, 1000)

# Voltage across capacitor over time in an RC charging circuit
Vc = V0 * (1 - np.exp(-t / (R * C)))

# Plotting
plt.plot(t, Vc)
plt.title('Voltage Across Capacitor Over Time')
plt.xlabel('Time (s)')
plt.ylabel('Voltage (V)')
plt.grid(True)
plt.show()
