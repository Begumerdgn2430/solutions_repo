# Problem 3
# Payload Trajectories Near Earth

When a payload is released from a rocket near Earth, its path is governed by Newtonian gravity and initial conditions such as velocity, direction, and altitude. This document explores the types of trajectories possible—elliptical, parabolic, or hyperbolic—and simulates them using numerical integration.

## Physical Background

The gravitational force acting on a payload of mass $m$ due to the Earth (mass $M$) is given by Newton’s Law of Gravitation:

$$
\vec{F}_g = - \frac{G M m}{r^2} \hat{r}
$$

where:
- $G = 6.67430 \times 10^{-11} \ \text{m}^3\text{kg}^{-1}\text{s}^{-2}$ is the gravitational constant,
- $r$ is the distance from the center of the Earth,
- $\hat{r}$ is the unit vector pointing from the object to the Earth.

The motion of the payload can be determined by solving Newton's second law:

$$
\vec{a} = \frac{\vec{F}_g}{m} = - \frac{G M}{r^2} \hat{r}
$$

## Initial Conditions

- **Altitude**: 800 km above Earth's surface
- **Earth radius**: $R_E = 6371$ km
- **Initial position**: $\vec{r}_0 = (R_E + 800, 0)$ km
- **Initial velocities**: 5 to 13 km/s in the tangential (positive y) direction

## Trajectory Types

- **Elliptical orbit**: $v < v_{\text{escape}}$
- **Parabolic escape**: $v = v_{\text{escape}}$
- **Hyperbolic escape**: $v > v_{\text{escape}}$

Escape velocity from a distance $r$ is:

$$
v_{\text{escape}} = \sqrt{\frac{2 G M}{r}}
$$
 ![alt text](image-8.png)

## Python Simulation

The following Python code numerically integrates the motion using the Runge-Kutta method and plots the trajectory for various initial velocities. Earth is represented as a blue circle on the plot.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
G = 6.67430e-11           # gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24              # Earth mass (kg)
R_E = 6.371e6             # Earth radius (m)
altitude = 800e3          # 800 km above surface
r0 = R_E + altitude       # initial distance from center of Earth (m)
initial_pos = np.array([r0, 0])  # starting to the right of Earth
velocities_kms = np.arange(5, 13.5, 0.5)  # km/s
velocities = velocities_kms * 1000  # convert to m/s

def gravity(t, y):
    x, vx, y_, vy = y
    r = np.sqrt(x**2 + y_**2)
    ax = -G * M * x / r**3
    ay = -G * M * y_ / r**3
    return [vx, ax, vy, ay]

# Set up plot
plt.figure(figsize=(8, 8))
theta = np.linspace(0, 2*np.pi, 300)
earth_x = R_E * np.cos(theta)
earth_y = R_E * np.sin(theta)
plt.plot(earth_x, earth_y, 'b', label='Earth')

colors = plt.cm.plasma(np.linspace(0, 1, len(velocities)))

for v0, color in zip(velocities, colors):
    # Initial state: x, vx, y, vy
    y0 = [r0, 0, 0, v0]  # tangential velocity upwards
    sol = solve_ivp(gravity, [0, 10000], y0, max_step=1, rtol=1e-8)

    x = sol.y[0]
    y = sol.y[2]
    
    plt.plot(x, y, color=color, label=f'v0 = {v0/1000:.1f} km/s')

# Plot Earth and formatting
plt.gca().set_aspect('equal')
plt.title("Payload Trajectories Near Earth")
plt.xlabel("x [m]")
plt.ylabel("y [m]")
plt.legend()
plt.grid(True)
plt.xlim(-2e7, 2e7)
plt.ylim(-2e7, 2e7)
plt.show()
```
# Colab #
[Colab Link](https://colab.research.google.com/drive/1UPn6MBFrlmQp4cqLCaJ4XPxoa8Iq_RWj?usp=sharing)