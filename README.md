# 🎛️ Active Vibration Control of a Single Degree of Freedom (SDOF) System

This project showcases an in-depth study of Active Vibration Control (AVC) techniques applied to a Single Degree of Freedom (SDOF) mechanical system using feedback mechanisms. It includes system modelling, frequency-domain and time-domain analysis, state-space representation, and performance visualisation using MATLAB/Python.

---

## 📌 Objective

To explore the effects of different feedback control strategies—displacement, velocity, and acceleration—on the dynamics and stability of an SDOF system, both in frequency and time domains.

---

## ⚙️ System Model

The mechanical system is governed by the classical mass-spring-damper equation:

```math
m\ddot{x}(t) + c\dot{x}(t) + kx(t) = F_p(t) + F_s(t)
```

Where:

- m=5kg
- c=20Ns/m
- k=2.2×106 N/m
- Fp(t) = primary input force
- Fs(t) = secondary control force

---

## 📈 Frequency Domain Analysis

### ✅ Open-loop Frequency Response

Bode and Nyquist plots were generated for the open-loop system:

```math
G(j\omega) = \frac{1}{- \omega^2 m + j \omega c + k}
```

**📊 Plot:**
- **Figure 1**: Bode plot of open-loop system  
- **Observation**: Resonance at ≈ 105.57 Hz (natural frequency)

---

### ✅ Feedback Control Strategies

The feedback controller is expressed as:

```math
H(j\omega) = g_d + j \omega g_v - \omega^2 g_a
```

**Plots & Interpretation:**

- **Figure 2**: Nyquist plot with acceleration gain \( g_a \)  
- **Figure 3**: Bode plot with acceleration gain  
- **Figure 4**: Nyquist plot with velocity gain \( g_v \)  
- **Figure 5**: Bode plot with velocity gain  
- **Figure 6**: Nyquist plot with displacement gain \( g_d \)  
- **Figure 7**: Bode plot with displacement gain  

> **Observation**:  
> - \( g_v \) adds damping → Most stable  
> - \( g_a \) increases effective mass  
> - \( g_d \) increases effective stiffness

---

## 🔄 Closed-loop System Response

The closed-loop transfer function:

```math
G_{cl}(j\omega) = \frac{G(j\omega)}{1 + G(j\omega)H(j\omega)}
```

**📊 Plots:**
- **Figure 11-16**: Bode plots for each gain configuration
- **Figure 14-16**: Combined gain effects (e.g. \( g_d + g_v \), \( g_v + g_a \))

---

## ⌛ Time Domain Simulations

Initial condition:  
- \( x(0) = 0.1 \, \text{m}, \quad \dot{x}(0) = 0 \)

**Open-loop State-Space**:

```math
\begin{aligned}
\dot{z}_1(t) &= z_2(t) \\
\dot{z}_2(t) &= -\frac{k}{m}z_1(t) - \frac{c}{m}z_2(t) + \frac{1}{m}F_p(t)
\end{aligned}
```

**Closed-loop (e.g. with \( g_d \))**:

```math
\dot{z}_2(t) = -\left(\frac{k + g_d}{m}\right) z_1(t) - \left(\frac{c}{m}\right) z_2(t) + \frac{1}{m}F_p(t)
```

**📊 Plots:**

- **Figure 17**: Open-loop response  
- **Figure 18-22**: Closed-loop with varying \( g_d \)  
- **Figure 23-25**: Closed-loop with varying \( g_v \)  
- **Figure 26-28**: Closed-loop with varying \( g_a \)

> 💡 **Insight**:  
> - \( g_d \): Increases frequency  
> - \( g_v \): Damps oscillations  
> - \( g_a \): Slows frequency, but may reduce damping

---

## 🧮 Eigenvalue Stability Analysis

State matrix \( A \) is derived and eigenvalues plotted for each gain variation.

```math
A = 
\begin{bmatrix}
0 & 1 \\
-\frac{k + g_d}{m + g_a} & -\frac{c + g_v}{m + g_a}
\end{bmatrix}
```

**📊 Plots:**
- **Figure 29**: Open-loop eigenvalues  
- **Figure 30**: With \( g_d \)  
- **Figure 31**: With \( g_v \)  
- **Figure 32**: With \( g_a \)

> 🔍 Real part < 0 → Stable system (Hurwitz criterion)

---

## 🌊 Forced Vibration: Sine Excitation

System excited with 10 Hz sine wave.

**📊 Plots:**

- **Figure 33-35**: Open-loop response  
- **Figure 36-42**: Closed-loop responses with different gains under forced excitation

> 🎯 **Best performance**:  
> Combination of \( g_d + g_v \) – Shifts resonance and adds damping, reducing magnitude without delay

---

## 🧰 Tools & Libraries

- MATLAB R2024a / Python 3.11
- `NumPy`, `SciPy`, `Matplotlib`
- Control Systems Toolbox
- `ode45` / `scipy.integrate.ode`

---

## 📚 References

- Dr Jordan Cheer – Lab Manual & Lectures  
- Fuller, C.R., Elliott, S.J., Nelson, P.A.  
  *Active Control of Vibration*, Academic Press, 1997
  
---

## 🧮 Modified State-Space Representation

When applying feedback control, the control force \( F_s(t) \) is defined based on the feedback type:

### ▶️ 1. Displacement Feedback

Let:

```math
F_s(t) = -g_d x(t)
```

Substituting into the original equation of motion:

```math
m\ddot{x}(t) + c\dot{x}(t) + kx(t) = F_p(t) + F_s(t) = F_p(t) - g_d x(t)
```

Rewriting:

```math
m\ddot{x}(t) + c\dot{x}(t) + (k + g_d)x(t) = F_p(t)
```

Divide through by \( m \):

```math
\ddot{x}(t) = -\frac{c}{m} \dot{x}(t) - \left(\frac{k + g_d}{m}\right) x(t) + \frac{1}{m} F_p(t)
```

Define state variables:

```math
z_1(t) = x(t), \quad z_2(t) = \dot{x}(t)
```

State-space representation:

```math
\begin{bmatrix}
\dot{z}_1(t) \\
\dot{z}_2(t)
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
-\left(\frac{k + g_d}{m}\right) & -\left(\frac{c}{m}\right)
\end{bmatrix}
\begin{bmatrix}
z_1(t) \\
z_2(t)
\end{bmatrix}
+
\begin{bmatrix}
0 \\
\frac{1}{m}
\end{bmatrix}
F_p(t)
```

---

### ▶️ 2. Velocity Feedback

Let:

```math
F_s(t) = -g_v \dot{x}(t)
```

Substitute into the original system:

```math
m\ddot{x}(t) + c\dot{x}(t) + kx(t) = F_p(t) - g_v \dot{x}(t)
```

Combine damping terms:

```math
m\ddot{x}(t) + (c + g_v)\dot{x}(t) + kx(t) = F_p(t)
```

Divide by \( m \):

```math
\ddot{x}(t) = -\left(\frac{c + g_v}{m}\right) \dot{x}(t) - \frac{k}{m} x(t) + \frac{1}{m} F_p(t)
```

State-space:

```math
\begin{bmatrix}
\dot{z}_1(t) \\
\dot{z}_2(t)
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
-\left(\frac{k}{m}\right) & -\left(\frac{c + g_v}{m}\right)
\end{bmatrix}
\begin{bmatrix}
z_1(t) \\
z_2(t)
\end{bmatrix}
+
\begin{bmatrix}
0 \\
\frac{1}{m}
\end{bmatrix}
F_p(t)
```

---

### ▶️ 3. Acceleration Feedback

Let:

```math
F_s(t) = -g_a \ddot{x}(t)
```

Total force:

```math
m\ddot{x}(t) + c\dot{x}(t) + kx(t) = F_p(t) + F_s(t) = F_p(t) - g_a \ddot{x}(t)
```

Move terms to one side:

```math
(m + g_a)\ddot{x}(t) + c\dot{x}(t) + kx(t) = F_p(t)
```

Divide by \( m + g_a \):

```math
\ddot{x}(t) = -\left(\frac{c}{m + g_a}\right) \dot{x}(t) - \left(\frac{k}{m + g_a}\right) x(t) + \left(\frac{1}{m + g_a}\right) F_p(t)
```

State-space:

```math
\begin{bmatrix}
\dot{z}_1(t) \\
\dot{z}_2(t)
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
-\left(\frac{k}{m + g_a}\right) & -\left(\frac{c}{m + g_a}\right)
\end{bmatrix}
\begin{bmatrix}
z_1(t) \\
z_2(t)
\end{bmatrix}
+
\begin{bmatrix}
0 \\
\frac{1}{m + g_a}
\end{bmatrix}
F_p(t)
```

---

### ▶️ 4. Combined Feedback (General Case)

If all three feedback gains are active:

```math
F_s(t) = -g_d x(t) - g_v \dot{x}(t) - g_a \ddot{x}(t)
```

Modified equation:

```math
(m + g_a)\ddot{x}(t) + (c + g_v)\dot{x}(t) + (k + g_d)x(t) = F_p(t)
```

Final state-space form:

```math
\begin{bmatrix}
\dot{z}_1(t) \\
\dot{z}_2(t)
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
-\left(\frac{k + g_d}{m + g_a}\right) & -\left(\frac{c + g_v}{m + g_a}\right)
\end{bmatrix}
\begin{bmatrix}
z_1(t) \\
z_2(t)
\end{bmatrix}
+
\begin{bmatrix}
0 \\
\frac{1}{m + g_a}
\end{bmatrix}
F_p(t)
```

This general formulation helps analyse the combined impact of all control strategies on the system dynamics.
