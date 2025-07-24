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

- \( m = 5 \, \text{kg} \)
- \( c = 20 \, \text{Ns/m} \)
- \( k = 2.2 \times 10^6 \, \text{N/m} \)
- \( F_p(t) \) = primary input force
- \( F_s(t) \) = secondary control force

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
