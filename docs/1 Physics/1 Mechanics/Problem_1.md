# Problem 1

.

---

## The Basics: What Affects the Range?

When you launch a projectile at some angle $\theta$ with an initial speed $v_0$, the horizontal distance it travels—called the **range** $R$—depends on gravity and the launch angle. Here’s the equation that ties it all together:

$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

Where:
- $v_0$ is how fast you're launching it (in meters per second)
- $\theta$ is the angle you launch it at (in degrees)
- $g = 9.81 \, \text{m/s}^2$ is gravity pulling it down

Cool fact: The range is highest when $\theta = 45^\circ$.

---

##   Simulate It with Python

Here’s some Python code that calculates the range for different angles and plots

```python
import numpy as np
import matplotlib.pyplot as plt

# Gravity and initial speed
g = 9.81  # m/s^2
v0 = 20.0  # m/s

# Try angles from 0 to 90 degrees
angles_deg = np.linspace(0, 90, 100)
angles_rad = np.radians(angles_deg)

# Calculate the range for each angle
ranges = (v0 ** 2) * np.sin(2 * angles_rad) / g

# Plot it
plt.figure(figsize=(10, 6))
plt.plot(angles_deg, ranges)
plt.title("How Far Does It Go? Range vs Launch Angle")
plt.xlabel("Launch Angle (degrees)")
plt.ylabel("Range (meters)")
plt.grid(True)
plt.axvline(x=45, color='red', linestyle='--', label='Max Range at 45°')
plt.legend()
plt.tight_layout()
plt.show()
```

![alt text](<Screenshot 2025-03-31 at 22.09.39.png>)

---

##  Final
- The **sweet spot** for distance is 45°—that’s when the projectile goes the farthest.
- The graph is symmetric: launching at 30° gives you the same range as 60°.
- If you increase the launch speed, the range increases a lot (since it’s based on $v_0^2$).

---

