---
title: 'What Changes When PI Control Is Added to the Excitation System?'
date: 2026-04-23
permalink: /posts/2026/04/smib-avr-pi-excitation/
tags:
  - control-theory
  - power-systems
  - excitation-system
  - AVR
  - PI-control
  - small-signal-stability
---

This post discusses a small but important modeling question in a single-machine infinite-bus (SMIB) system:

> What changes when the proportional voltage feedback in the excitation system is replaced by a PI controller?

The main conclusion is:

> Adding integral action forces the terminal voltage \(V\) to converge to the reference \(V^\star\), but it also introduces an extra slow pole.  
> This slow pole mainly appears in the excitation/voltage channel, especially in the integral state, \(E_{fd}\), internal voltage \(e\), and terminal voltage \(V\).  
> It is not primarily a frequency oscillation mode, although it can weakly affect \(\omega\) through electromechanical coupling.

In this post, I compare the two cases:

1. AVR with proportional voltage feedback only;
2. AVR with PI voltage feedback.

The comparison is based on nonlinear time-domain simulation and small-signal linearization around the corresponding equilibrium points.

---

## 1. Nonlinear SMIB Model

Consider the state vector before adding integral action:

\[
x =
\begin{bmatrix}
E_{fd} \\
e \\
\delta \\
\omega
\end{bmatrix}.
\]

Here,

- \(E_{fd}\) is the excitation voltage state;
- \(e\) is the internal transient voltage magnitude;
- \(\delta\) is the rotor angle;
- \(\omega\) is the rotor speed deviation.

The terminal voltage magnitude is computed from

\[
V =
\sqrt{
\alpha^2 e^2
+ 2\alpha\beta e\cos\delta
+ \beta^2
},
\]

where

\[
\alpha = \frac{x_L}{x+x_L},
\qquad
\beta = \frac{x}{x+x_L}.
\]

The network angle is

\[
\theta
=
\tan^{-1}
\left(
\frac{\alpha e\sin\delta}
{\alpha e\cos\delta+\beta}
\right).
\]

For numerical implementation, it is usually better to use `atan2` instead of `atan`, but the mathematical expression above is the same as the one used in the simulation.

The machine and excitation dynamics are

\[
\dot E_{fd}
=
\frac{1}{T'_{d0}}
\left(
-K_1 E_{fd}
-K_2(V-V^\star)
+u
\right),
\]

\[
\dot e
=
\frac{1}{T_d}
\left(
-ae
+bV\cos(\delta-\theta)
+E_{fd}
\right),
\]

\[
\dot\delta = \omega,
\]

\[
\dot\omega
=
\frac{1}{M}
\left(
P_m
-d\omega
-
\frac{eV\sin(\delta-\theta)}{x}
\right).
\]

The parameters used in the simulation are

\[
T'_{d0}=0.1,
\qquad
T_d=0.05,
\qquad
K_1=1.5,
\qquad
K_2=6,
\]

\[
M=0.2,
\qquad
d=0.28,
\qquad
P_m=0.1,
\qquad
V^\star=0.9.
\]

The constants

\[
a = \frac{x_d}{x'_d},
\qquad
b = \frac{x_d-x'_d}{x'_d}
\]

come from the transient voltage equation.

---

## 2. Excitation System Without PI Control

Without PI control, the excitation equation is

\[
\dot E_{fd}
=
\frac{1}{T'_{d0}}
\left[
-K_1 E_{fd}
-K_2(V-V^\star)
+u
\right].
\]

If \(u=0\), the equilibrium condition of this equation is

\[
0 =
-K_1 E_{fd}
-K_2(V-V^\star).
\]

Therefore,

\[
K_1 E_{fd}
=
-K_2(V-V^\star),
\]

or

\[
E_{fd}
=
-\frac{K_2}{K_1}(V-V^\star)
=
\frac{K_2}{K_1}(V^\star-V).
\]

This equation is important.

It does **not** require

\[
V=V^\star.
\]

Instead, it only says that the excitation state \(E_{fd}\) balances the proportional voltage error. Therefore, a proportional AVR can stabilize the voltage, but it generally leaves a nonzero steady-state voltage error.

This is exactly what appears in the numerical result.

The equilibrium point is

\[
x_e =
\begin{bmatrix}
E_{fd} \\
e \\
\delta \\
\omega
\end{bmatrix}
=
\begin{bmatrix}
0.3611479986 \\
0.6784867217 \\
0.6488693916 \\
0
\end{bmatrix}.
\]

The corresponding terminal voltage is

\[
V_e = 0.809713000359.
\]

Since

\[
V^\star = 0.9,
\]

the steady-state voltage error is

\[
V_e - V^\star
=
0.809713000359 - 0.9
=
-0.090286999641.
\]

So the proportional AVR stabilizes the system, but the voltage settles below the reference.

---

## 3. Adding PI Control to the Excitation System

Now introduce an integral state

\[
W_1
\]

with dynamics

\[
\dot W_1 = V - V^\star.
\]

The excitation equation becomes

\[
\dot E_{fd}
=
\frac{1}{T'_{d0}}
\left[
-K_1E_{fd}
-K_2(V-V^\star)
-K_3W_1
+u
\right].
\]

The new state vector is

\[
x =
\begin{bmatrix}
E_{fd} \\
e \\
\delta \\
\omega \\
W_1
\end{bmatrix}.
\]

The key difference is the equilibrium condition of the integral state:

\[
\dot W_1 = 0.
\]

Since

\[
\dot W_1 = V - V^\star,
\]

at equilibrium we must have

\[
V_e - V^\star = 0.
\]

Therefore,

\[
V_e = V^\star.
\]

This is the mathematical reason why integral action removes the steady-state voltage error.

The numerical equilibrium is

\[
x_e =
\begin{bmatrix}
E_{fd} \\
e \\
\delta \\
\omega \\
W_1
\end{bmatrix}
=
\begin{bmatrix}
0.7700156811 \\
0.8463750024 \\
0.5056987424 \\
0 \\
-2.3100470432
\end{bmatrix}.
\]

The terminal voltage is

\[
V_e = 0.900000000000.
\]

Thus, after adding PI control,

\[
V_e = V^\star.
\]

Compared with the proportional-only case, the excitation voltage increases from

\[
E_{fd}=0.3611
\]

to

\[
E_{fd}=0.7700.
\]

The internal voltage also increases from

\[
e=0.6785
\]

to

\[
e=0.8464.
\]

The rotor angle decreases from

\[
\delta=0.6489
\]

to

\[
\delta=0.5057.
\]

This means that the PI excitation controller raises the voltage level and changes the operating point of the electromechanical system.

---

## 4. Linearization

For small-signal analysis, write

\[
\dot x = f(x,u).
\]

Linearization around an equilibrium point \((x_e,u_e)\) gives

\[
\Delta \dot x
=
A\Delta x + B\Delta u,
\]

where

\[
A =
\left.
\frac{\partial f}{\partial x}
\right|_{x=x_e,u=u_e},
\qquad
B =
\left.
\frac{\partial f}{\partial u}
\right|_{x=x_e,u=u_e}.
\]

The terminal voltage small-signal output is

\[
\Delta V = C_V \Delta x,
\]

where

\[
C_V =
\left.
\frac{\partial V}{\partial x}
\right|_{x=x_e}.
\]

Since \(V\) depends only on \(e\) and \(\delta\), we have

\[
C_V =
\begin{bmatrix}
0 &
\frac{\partial V}{\partial e} &
\frac{\partial V}{\partial \delta} &
0
\end{bmatrix}
\]

for the no-PI case, and

\[
C_V =
\begin{bmatrix}
0 &
\frac{\partial V}{\partial e} &
\frac{\partial V}{\partial \delta} &
0 &
0
\end{bmatrix}
\]

for the PI case.

From

\[
V =
\sqrt{
\alpha^2 e^2
+ 2\alpha\beta e\cos\delta
+ \beta^2
},
\]

we obtain

\[
\frac{\partial V}{\partial e}
=
\frac{
\alpha^2 e + \alpha\beta\cos\delta
}{V},
\]

and

\[
\frac{\partial V}{\partial \delta}
=
\frac{
-\alpha\beta e\sin\delta
}{V}.
\]

The frequency output is

\[
\Delta \omega = C_\omega \Delta x.
\]

For the no-PI model,

\[
C_\omega =
\begin{bmatrix}
0 & 0 & 0 & 1
\end{bmatrix}.
\]

For the PI model,

\[
C_\omega =
\begin{bmatrix}
0 & 0 & 0 & 1 & 0
\end{bmatrix}.
\]

---

## 5. Linearized Model Without PI

The linearized state matrix is

\[
A =
\begin{bmatrix}
-15.0000 & -25.4781 & 7.5546 & 0 \\
20.0000 & -73.6585 & -32.4251 & 0 \\
0 & 0 & 0 & 1 \\
0 & -0.7369 & -0.6593 & -1.4000
\end{bmatrix}.
\]

The input matrix for the input \(u\) is

\[
B =
\begin{bmatrix}
10 \\
0 \\
0 \\
0
\end{bmatrix}.
\]

The voltage output matrix is

\[
C_V =
\begin{bmatrix}
0 & 0.4246 & -0.1259 & 0
\end{bmatrix}.
\]

The frequency output matrix is

\[
C_\omega =
\begin{bmatrix}
0 & 0 & 0 & 1
\end{bmatrix}.
\]

The eigenvalues are

\[
\lambda(A)
=
\left\{
-63.0461,\;
-25.6195,\;
-0.6965+j0.1446,\;
-0.6965-j0.1446
\right\}.
\]

All eigenvalues are in the open left-half plane, so the equilibrium is locally asymptotically stable.

The two fast real poles,

\[
-63.0461,
\qquad
-25.6195,
\]

are mainly associated with the fast excitation and internal voltage dynamics.

The complex pair,

\[
-0.6965\pm j0.1446,
\]

is the dominant electromechanical mode.

For a complex pair

\[
s =
-\sigma \pm j\omega_d,
\]

the natural frequency is

\[
\omega_n =
\sqrt{\sigma^2+\omega_d^2},
\]

and the damping ratio is

\[
\zeta =
\frac{\sigma}{\omega_n}.
\]

Here,

\[
\sigma = 0.6965,
\qquad
\omega_d = 0.1446.
\]

Thus,

\[
\omega_n
\approx
\sqrt{0.6965^2+0.1446^2}
\approx 0.7113,
\]

and

\[
\zeta
\approx
\frac{0.6965}{0.7113}
\approx 0.979.
\]

So the no-PI electromechanical mode is highly damped and only weakly oscillatory.

---

## 6. Linearized Model With PI

After adding PI control, the linearized state matrix becomes

\[
A =
\begin{bmatrix}
-15.0000 & -26.6200 & 6.7967 & 0 & -5.0000 \\
20.0000 & -73.6585 & -25.9932 & 0 & 0 \\
0 & 0 & 0 & 1 & 0 \\
0 & -0.5908 & -0.9030 & -1.4000 & 0 \\
0 & 0.4437 & -0.1133 & 0 & 0
\end{bmatrix}.
\]

The input matrix is

\[
B =
\begin{bmatrix}
10 \\
0 \\
0 \\
0 \\
0
\end{bmatrix}.
\]

The voltage output matrix is

\[
C_V =
\begin{bmatrix}
0 & 0.4437 & -0.1133 & 0 & 0
\end{bmatrix}.
\]

The frequency output matrix is

\[
C_\omega =
\begin{bmatrix}
0 & 0 & 0 & 1 & 0
\end{bmatrix}.
\]

The eigenvalues are

\[
\lambda(A)
=
\left\{
-62.4484,\;
-26.1878,\;
-0.6933+j0.5644,\;
-0.6933-j0.5644,\;
-0.0358
\right\}.
\]

Again, all eigenvalues are in the open left-half plane, so the PI-controlled equilibrium is locally asymptotically stable.

However, compared with the no-PI case, one new pole appears:

\[
\lambda_{\text{slow}} = -0.0358.
\]

This pole is very close to the imaginary axis.

Its time constant is approximately

\[
\tau_{\text{slow}}
=
\frac{1}{0.0358}
\approx 27.9\text{ s}.
\]

A rough four-time-constant settling estimate is

\[
T_s
\approx
4\tau_{\text{slow}}
\approx 111.7\text{ s}.
\]

This explains why the PI controller can remove the voltage steady-state error, but the final convergence of some variables becomes slow.

The electromechanical pair becomes

\[
-0.6933\pm j0.5644.
\]

For this mode,

\[
\sigma = 0.6933,
\qquad
\omega_d = 0.5644.
\]

Therefore,

\[
\omega_n
=
\sqrt{0.6933^2+0.5644^2}
\approx 0.894,
\]

and

\[
\zeta
=
\frac{0.6933}{0.894}
\approx 0.776.
\]

So adding PI control changes the oscillation frequency and reduces the damping ratio of the electromechanical mode from approximately

\[
0.979
\]

to

\[
0.776.
\]

However, the real part of the electromechanical pair remains close to

\[
-0.69.
\]

Thus, the main new slow behavior is not caused by the complex electromechanical mode, but by the new real pole

\[
-0.0358.
\]

---

## 7. Which State Becomes Slow After Adding PI?

The PI controller adds the state

\[
W_1
\]

with

\[
\dot W_1 = V - V^\star.
\]

This means the new slow pole is most directly related to the integral state \(W_1\).

Since \(W_1\) enters the excitation equation,

\[
\dot E_{fd}
=
\frac{1}{T'_{d0}}
\left[
-K_1E_{fd}
-K_2(V-V^\star)
-K_3W_1
+u
\right],
\]

the slow mode propagates through the chain

\[
W_1
\longrightarrow
E_{fd}
\longrightarrow
e
\longrightarrow
V.
\]

Therefore, the variables most affected by the slow pole are

\[
W_1,\quad E_{fd},\quad e,\quad V.
\]

The rotor speed \(\omega\) is not the main slow variable. It is primarily governed by the electromechanical mode

\[
-0.6933\pm j0.5644.
\]

Of course, because the system is coupled, the slow pole can still have a small effect on \(\omega\), but the most visible slow tail appears in the voltage and excitation-related states.

This is an important practical point:

> PI control improves steady-state voltage tracking, but the price is a slower voltage/excitation recovery.

---

## 8. Transfer Function From \(u\) to \(\omega\)

The transfer function from the input \(u\) to the frequency state \(\omega\) is useful for root-locus analysis.

### 8.1 Without PI

The transfer function is

\[
G_{\omega u}^{\text{no PI}}(s)
=
\frac{-147.39s}
{(s+63.05)(s+25.62)(s^2+1.393s+0.506)}.
\]

The zero at

\[
s=0
\]

means that a constant input perturbation in \(u\) does not create a nonzero steady-state frequency deviation. Physically, the rotor speed must return to zero at a new equilibrium.

The poles of this transfer function are the same as the eigenvalues of the linearized system:

\[
s=-63.05,\quad
s=-25.62,\quad
s=-0.6965\pm j0.1446.
\]

### 8.2 With PI

With PI control, the transfer function becomes

\[
G_{\omega u}^{\text{PI}}(s)
=
\frac{-118.15s^2}
{(s+62.45)(s+26.19)(s+0.03578)(s^2+1.387s+0.7991)}.
\]

The important new term is

\[
s+0.03578.
\]

This is the additional slow pole introduced by integral action.

There is also an additional zero at the origin, giving \(s^2\) in the numerator. This means that, in the \(u\to\omega\) channel, the slow integral mode may not dominate the frequency response as strongly as it dominates voltage-related variables.

This agrees with the time-domain interpretation:

- \(\omega\) is mainly affected by the electromechanical mode;
- \(V\), \(E_{fd}\), \(e\), and \(W_1\) are more visibly affected by the slow PI pole.

---

## 9. Root-Locus Interpretation

The root locus of \(u\to\omega\) shows how the closed-loop poles would move if a scalar feedback gain were placed around this linearized input-output channel.

For the no-PI model,

\[
G_{\omega u}^{\text{no PI}}(s)
=
\frac{-147.39s}
{(s+63.05)(s+25.62)(s^2+1.393s+0.506)}.
\]

There are four open-loop poles and one zero at the origin.

For the PI model,

\[
G_{\omega u}^{\text{PI}}(s)
=
\frac{-118.15s^2}
{(s+62.45)(s+26.19)(s+0.03578)(s^2+1.387s+0.7991)}.
\]

There are five open-loop poles and two zeros at the origin.

The most important root-locus difference is the extra pole near the origin:

\[
s=-0.03578.
\]

Because this pole is close to the imaginary axis, it indicates a slow mode. In a feedback design, this pole can strongly affect low-frequency behavior and the long-time transient.

However, because the transfer function \(u\to\omega\) has zeros at the origin, the slow pole is not necessarily the most visible mode in the frequency output. To see the slow PI effect more clearly, it is often better to also inspect

\[
u\to V,
\qquad
u\to E_{fd},
\qquad
u\to W_1.
\]

---

## 10. Summary of Numerical Results

| Quantity | Without PI | With PI |
|---|---:|---:|
| \(E_{fd,e}\) | 0.3611 | 0.7700 |
| \(e_e\) | 0.6785 | 0.8464 |
| \(\delta_e\) | 0.6489 | 0.5057 |
| \(\omega_e\) | 0 | 0 |
| \(W_{1,e}\) | -- | -2.3100 |
| \(V_e\) | 0.8097 | 0.9000 |
| Voltage tracking | steady-state error | zero steady-state error |
| Extra slow pole | no | yes, \(-0.0358\) |
| Dominant electromechanical pair | \(-0.6965\pm j0.1446\) | \(-0.6933\pm j0.5644\) |
| Electromechanical damping ratio | 0.979 | 0.776 |

The most important difference is:

\[
V_e^{\text{no PI}} = 0.8097 \neq 0.9,
\]

while

\[
V_e^{\text{PI}} = 0.9.
\]

Thus, the PI controller successfully eliminates the voltage steady-state error.

But the price is the new slow pole

\[
-0.0358,
\]

which creates a slow convergence tail mainly in the excitation and voltage states.

---

## 11. Main Takeaways

1. A proportional AVR can stabilize the SMIB system, but it does not generally guarantee \(V=V^\star\) at steady state.

2. Adding integral action introduces

   \[
   \dot W_1 = V - V^\star,
   \]

   which forces

   \[
   V_e = V^\star
   \]

   at equilibrium.

3. The PI controller changes the operating point significantly:

   \[
   E_{fd}: 0.3611 \to 0.7700,
   \]

   \[
   e: 0.6785 \to 0.8464,
   \]

   \[
   \delta: 0.6489 \to 0.5057.
   \]

4. The PI controller adds a slow pole:

   \[
   -0.0358.
   \]

5. This slow pole mainly slows the voltage/excitation channel:

   \[
   W_1,\quad E_{fd},\quad e,\quad V.
   \]

6. The frequency state \(\omega\) is still mainly shaped by the electromechanical complex pair, not by the slow integral pole.

7. Therefore, for this SMIB example:

   > PI control improves steady-state voltage regulation, but it can make voltage/excitation recovery slower and can change the damping properties of the electromechanical mode.

---
