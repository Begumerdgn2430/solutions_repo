# Problem 1

import numpy as np
import matplotlib.pyplot as plt
from math import sqrt, cos, pi

# Parameters
A = 1.0  # Amplitude
lambda_ = 1.0  # Wavelength
k = 2 * pi / lambda_  # Wave number
f = 1.0  # Frequency
omega = 2 * pi * f  # Angular frequency
phi = 0.0  # Initial phase
t = 0.0  # Time

# Define a square polygon vertices (example)
vertices = [(0, 0), (1, 0), (1, 1), (0, 1)]
N = len(vertices)  # Number of sources

# Create grid
x = np.linspace(-2, 2, 100)
y = np.linspace(-2, 2, 100)
X, Y = np.meshgrid(x, y)
eta_sum = np.zeros_like(X, dtype=float)

# Superposition of waves
for x0, y0 in vertices:
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    eta = A / np.sqrt(r + 1e-10) * cos(k * r - omega * t + phi)  # Avoid division by zero
    eta_sum += eta

# Plot
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, eta_sum, levels=50, cmap='viridis')
plt.colorbar(label='Displacement')
plt.title('Interference Patterns on Water Surface')
plt.xlabel('X')
plt.ylabel('Y')
plt.scatter([v[0] for v in vertices], [v[1] for v in vertices], color='red', label='Sources')
plt.legend()
plt.savefig('interference_pattern.png')