# Verification & Optimisation of a Capacitive MEMS Displacement Sensor

Resimulation and geometric optimisation of a capacitive MEMS displacement sensor in COMSOL Multiphysics, based on a 2025 IEEE WINTECHCON reference paper. This project reproduces the reference design, identifies an inconsistency in its reported results, and proposes an improved sensor geometry that cuts capacitance deviation by **4.6x**.

📄 [Full report (PDF)](./report.pdf)

## Problem

MEMS capacitive displacement sensors measure position by tracking how capacitance changes with the air gap between two electrodes. In practice, "fringe" electric fields near the electrode edges make real sensors deviate from the ideal parallel-plate behaviour, reducing accuracy. A Kelvin Guard Ring — a ring held at the same potential as the sensing electrode — is used to suppress this effect.

Starting from a published sensor design (IEEE WINTECHCON 2025), the goals were to:
- Reproduce its electric field and capacitance-vs-displacement results independently
- Check the reported results against electrostatic theory
- Optimise the guard ring and insulator geometry to reduce deviation from ideal capacitance

## Approach

- Rebuilt the sensor geometry (concentric sensing electrode, Kelvin Guard Ring, ground ring) in **COMSOL Multiphysics 6.1** using the Electrostatics module, 3D stationary solver, with a fine mesh near electrode boundaries
- Ran a parametric sweep of the air gap from 10 µm to 600 µm, at both 1 V and 5 V excitation
- Compared resimulated electric potential and electric field norm distributions against the reference paper
- Ran a second parametric sweep varying **Kelvin Guard Ring width** and **inner insulator width** to find a geometry that minimises capacitance deviation from the ideal case

## Results

| | Value |
|---|---|
| Reference paper deviation from ideal capacitance | 8.79% |
| **Optimised design deviation** | **1.92%** |
| Optimised Kelvin Guard Ring width | 3000 µm |
| Optimised inner insulator width | 30 µm |

- The 1 V resimulation closely matched both the reference paper and theoretical predictions.
- At 5 V, the reference paper reported capacitance values that **contradict electrostatic theory** — capacitance in a linear dielectric should be independent of applied voltage. The resimulation confirmed the theoretical (voltage-independent) behaviour, indicating the reference paper likely had a modelling or reporting error.
- Widening the guard ring and narrowing the inner insulator both reduced fringe-field effects and pulled the sensor's response closer to ideal.

![Optimisation result: deviation reduced from 8.79% to 1.92%](figures/optimization_result.png)
![Capacitance vs displacement at 1V](figures/capacitance_vs_displacement.png)
![Effect of Kelvin Guard Ring width on deviation](figures/guard_ring_effect.png)

## Tools

COMSOL Multiphysics 6.1 (Electrostatics module) · IEEE LaTeX

## Authors

Izha Safdar & Adee Bin Shahid — Department of Mechatronics Engineering, NUST CEME

## Reference

K. N., C. K. P., and Y. G., "Design of Capacitive based MEMS Displacement Sensor using COMSOL," *Proc. 2025 IEEE 6th International Women in Technology Conference (WINTECHCON)*, 2025.
