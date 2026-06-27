# MAT1012: Numerical Techniques

This repository contains a collection of interactive Google Colab notebooks developed for the Numerical Techniques course. The project compendium applies core mathematical algorithms, numerical discretization strategies, and root-finding frameworks to non-standard computational problems.

---

## Technical Project Summaries and Coursework Alignment

### Project 1: Pseudo-Random Number Generator (PRNG)
* **Application Overview:** A deterministic number generator designed to produce a uniform sequence of values bounded strictly within the open interval \((0, 1)\).
* **Syllabus Matrix Relation:** This implementation directly adapts the foundational principles of **Module 1: Fixed-Point Iteration Method**. In standard root-finding applications, the iterative mapping \(x_{n+1} = g(x_n)\) is calibrated to achieve numerical convergence by satisfying the stability criteria \(\vert{}g'(x)\vert{} < 1\). This architecture deliberately subverts that condition by utilizing a high-frequency trigonometric transcendental function where \(\vert{}g'(x)\vert{} \gg 1\). The resulting instability forces exponential divergence of mathematical errors, utilizing sensitivity to initial floating-point seed values to simulate pseudo-random numerical behavior.

### Project 2: 3-Player Chess Mesh & Routing Engine
* **Application Overview:** A geometric coordinate tracking system that calculates and validates continuous movement path vectors across three independent player sectors meeting at a central singularity point.
* **Syllabus Matrix Relation:** This project integrates concepts from **Module 2: Finite Differences** and **Module 3: Multivariate Interpolation**. By shifting from standard 2D Cartesian grids to a non-standard polar geometry, the system uses discrete spatial finite differences (\(\Delta X\), \(\Delta Y\)) to maintain linear path tracking across irregular spaces. When piece vectors transition across the intersecting boundaries of the \(120^\circ\) player zones, nearest-neighbor multivariate interpolation logic is applied to prevent grid-clipping and enforce boundary collision rules.

### Project 3: Goat Grazing Transcendental Optimization
* **Application Overview:** An optimization engine built to calculate the exact structural leash length required to bound a grazing footprint to an exact percentage of a circular enclosure.
* **Syllabus Matrix Relation:** This engine couples **Module 4: Numerical Integration** with **Module 1: Solution of Nonlinear Algebraic and Transcendental Equations**. Because the overlapping circular contours form a complex transcendental area boundary, analytical integration equations become highly inefficient. The system implements **Simpson's 3/8 Rule** to numerically approximate the area segments over a localized mesh. The calculated area residuals are then passed directly into a **Bisection Method** optimization loop, which iteratively refines the leash boundaries until the root converges within a strict tolerance threshold (\(\epsilon = 10^{-5}\)).

---

## Repository Structure

```text
├── Project_1_PRNG/
│   └── Fixed_Point_PRNG.ipynb         # Interactive PRNG engine cell
├── Project_2_3Player_Chess/
│   ├── Coordinate_Routing.ipynb       # Finite difference tracking module
│   └── Mesh_Visualizer.ipynb          # Polar coordinate board renderer
└── Project_3_Goat_Grazing/
    ├── Root_Optimization.ipynb        # Simpson's 3/8 and Bisection solver
    └── Arena_Geometry_Visualizer.ipynb # Overlap intersection graphic mask
```
