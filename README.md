# PIDLab

A browser-based playground for PID controller design and analysis. Step Response, Bode Diagram, and Root Locus — all in a single HTML file, no install required.

<img width="1882" height="796" alt="image" src="https://github.com/user-attachments/assets/17b09e9b-7572-4be5-a99a-fd7ef9717f75" />

## Try it

Download latest version of `pid_simulator.html` and double-click it. Works in any modern browser.

## What it does

PIDLab lets you specify a SISO plant `P(s) = N(s)/D(s) · e^(-sL)` and a parallel-form PID controller
C(s) = Kp + Ki/s + Kd · N · s / (s + N)

and visualize the closed-loop behavior three ways:

- **Step Response** — time-domain simulation with rise time, overshoot, settling time, steady-state value, and steady-state error
- **Bode Diagram** — open-loop magnitude and phase, with gain margin, phase margin, and the corresponding crossover frequencies (ω_cg, ω_cp), matching MATLAB's `margin()` conventions
- **Root Locus** — closed-loop pole-zero map of `T(s) = CP/(1+CP)`, with sweep traces showing how the poles move as Kp, Ki, or Kd is varied (×0.1 to ×10) from the current values

The Root Locus sweep traces are the distinctive feature: at a glance you see which gain has leverage on which pole, and in which direction, which makes manual PID tuning much more intuitive than working from step response alone.

## How to use

The left panel sets the plant and controller:

- **Numerator N(s)** and **Denominator D(s)** — polynomial coefficients in descending order, space-separated. Example: `1 2 1` means `s² + 2s + 1`.
- **Dead time L** — pure delay in seconds. Set to 0 to enable Root Locus (rational analysis only).
- **Kp / Ki / Kd** — controller gains in parallel form.
- **Deriv. filter N** — first-order filter cutoff applied to the derivative term. Typical 10–100. Larger N means closer to ideal derivative but adds a fast closed-loop pole at −N.
- **Stop time / Step size dt** — simulation horizon and integration step.
- **Setpoint** — reference value for the step response.

Hit `Simulate` (or Enter in any field) to update all three views.

## Limitations

- SISO only
- Root Locus is disabled when dead time L > 0 (Padé approximation would lie about the closed-loop poles, so the view is honest and disables itself)
- Plant orders above ~10 may show numerical noise in pole locations

## License

MIT

## Citation

If PIDLab is useful in published work, a citation to the related paper is appreciated:

> Gulgonul, S. (2026). *Analytical PI Tuning for Second-Order Plants with Monotonic Response and Minimum Settling Time*. [https://github.com/senolgulgonul/pidlab]
