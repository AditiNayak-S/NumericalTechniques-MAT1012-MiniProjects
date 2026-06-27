# MAT1012:  Numerical Techniques

This repository houses a comprehensive suite of interactive Google Colab notebooks developed to solve complex, non-standard engineering and geometric problems using core numerical discretization, approximation, and root-finding frameworks. 

Every implementation translates standard syllabus algorithms into robust, production-ready computer logic, adhering to rigorous academic standards and computational design principles.

---

## Detailed Project Engineering Profiles & Coursework Alignment

### Project 1: Pseudo-Random Number Generator (PRNG) via Non-Convergent Iteration
* **Application Architecture:** A deterministic, high-frequency numeric generator designed to produce a uniform sequence of floating-point pseudo-random values bounded strictly within the open interval (0, 1).
* **Syllabus Matrix Relation:** This system adapts the foundational principles of **Module 1: Solution of Nonlinear Algebraic and Transcendental Equations (Fixed-Point Iteration Method)**. 
* **Mathematical Derivation & Mechanics:** In standard root-finding applications, an economic iterative mapping function $x_{n+1} = g(x_n)$ is carefully calibrated to achieve numerical convergence across successive steps by satisfying the contraction mapping theorem and stability criteria:
  $$\left| g'(x) \right| < 1$$
  This architecture deliberately subverts that rule to force computational instability. It implements a high-frequency, non-linear trigonometric transcendental mapping defined as:
  $$g(x) = \left( \alpha \cdot \sin(\beta \cdot x) + \gamma \right) \pmod 1$$
  By setting the scaling magnification factor $\alpha = 10^5$ and the high-frequency angular modifier $\beta \approx 1414.2135$, the system guarantees that the stability derivative heavily violates the threshold:
  $$\left| g'(x) \right| = \left| \alpha \cdot \beta \cdot \cos(\beta \cdot x) \right| \ggg 1$$
  This catastrophic violation forces mathematical truncation and rounding errors to magnify exponentially across successive iterations. Instead of converging to a single fixed point or localized attractor, the fractional component extraction ($\pmod 1$) maps these highly divergent residuals back into the $(0, 1)$ domain, generating a statistically uniform distribution stream optimized via numerical chaos.
* **Extended Implementation Insights & Verification:** The system uses double-precision floating-point formats to store state variables, capturing minute mathematical variations at the 15th decimal place. Because the transformation function operates at extreme frequencies, the sequence undergoes basic diagnostic testing within the runtime pipeline. This tracking logs the mean value ($\mu \approx 0.5$) and structural variance ($\sigma^2 \approx 0.0833$) across long execution sequences. These metrics confirm the generation of a balanced pseudo-random distribution, verifying that the chaotic divergence sequence successfully spreads output coordinates evenly across the entire target domain without collapsing into repetitive structural sub-loops or localized periodicity clusters.

---

### Project 2: 3-Player Chess Mesh Discretization & Path Routing Engine
* **Application Architecture:** A geometric coordinate tracking system and collision-detection engine that calculates, scales, and validates continuous movement path vectors across three independent player sectors meeting at a central singularity point.
* **Syllabus Matrix Relation:** This project integrates core methods from **Module 2: Finite Differences (Equal Intervals)** and **Module 3: Interpolation (Unequal Intervals)**.
* **Mathematical Derivation & Mechanics:** Standard two-player boards rely on uniform Cartesian coordinates $(x, y)$. A three-player layout utilizes a non-standard polar/trilinear coordinate mesh split into three $120^\circ$ ($2\pi/3$ radians) wedges meeting at an origin point $(0,0)$. 
  To trace movement, the system maps localized cell keys (Sector $k$, Radius $r$, Angle $\theta$) to global Cartesian coordinates using the transformation equations:
  $$X = r \cdot \cos\left(\theta + \frac{2k\pi}{3}\right), \quad Y = r \cdot \sin\left(\theta + \frac{2k\pi}{3}\right)$$
  Because the area of individual cells increases as the radius expands ($\text{Area} \approx r \cdot \Delta r \cdot \Delta \theta$), the spatial mesh density is inherently non-uniform, requiring careful variable domain bounding. The engine applies discrete spatial finite difference approximations to compute step-by-step direction vectors across the board:
  $$\Delta X = X_{\text{target}} - X_{\text{start}}, \quad \Delta Y = Y_{\text{target}} - Y_{\text{start}}$$
  When a piece crosses the boundary separating adjacent player sectors, its tracking indices shift abruptly. The engine applies nearest-neighbor multivariate interpolation against a threshold boundary ($\epsilon = 10^{-7}$) to smoothly map inter-sector trajectories, validate path continuity, and ensure no intermediate cells trigger an occupancy matrix collision flag.
* **Extended Implementation Insights & Verification:** The tracking logic represents the board as a partitioned mesh topology composed of 96 discrete cells (3 sectors $\times$ 4 radial rings $\times$ 8 angular lanes). Path calculations use a discrete finite difference step vector scaled by the shortest boundary edge length. This prevents long-range pieces (like the Rook or Bishop) from skipping past adjacent cells without evaluating their status. The collision engine parses every coordinate step by calculating its localized inverse mapping, ensuring perfect tracking stability even near the coordinate singularity at the center point where directions invert instantly. This framework demonstrates how complex geometric routing can be managed without huge matrix look-up sets.

---

### Project 3: Goat Grazing Transcendental Geometry Optimization
* **Application Architecture:** An optimization engine built to calculate the exact structural leash length ($R$) required to bound a grazing footprint to a precise user-defined percentage of a circular enclosure.
* **Syllabus Matrix Relation:** This engine couples **Module 4: Numerical Integration (Simpson's 3/8 Rule)** with **Module 1: Iterative Non-linear Root Optimization Engines**.
* **Mathematical Derivation & Mechanics:** Finding the exact leash length $R$ that allows a goat tied to the perimeter of a circular arena (radius $r=1$) to graze exactly half the total area ($A = \pi/2$) requires solving a complex transcendental equation derived from overlapping circular segments:
  $$f(R) = \left(4 - R^2\right)^{1/2} + R^2\arccos\left(\frac{R}{2}\right) - \frac{R}{2}\left(4 - R^2\right)^{1/2} - \frac{\pi}{2} = 0$$
  When handling irregular or non-circular boundary variations, analytical solutions become mathematically intractable. The system handles this by running a high-order numerical integration loop using **Simpson's 3/8 Rule** to compute the overlapping areas across $n$ discrete subintervals (where $n$ is a multiple of 3):
  $$\int_{a}^{b} y(x) \, dx \approx \frac{3h}{8} \left[ y(x_0) + 3\sum_{i=1,4,7\dots}^{n-2} y(x_i) + 3\sum_{i=2,5,8\dots}^{n-1} y(x_i) + 2\sum_{i=3,6,9\dots}^{n-3} y(x_i) + y(x_n) \right]$$
  The calculated area error residual ($E = A_{\text{computed}} - A_{\text{target}}$) is passed as an automated feedback parameter into a **Bisection Method** root-finding matrix. By evaluating signs ($f(R_{\text{low}}) \cdot f(R_{\text{high}}) < 0$) and continuously halving the bounding interval, the engine bypasses derivative discontinuities at the perimeter intersections and isolates the optimal leash dimensions within a strict tolerance threshold ($\epsilon = 10^{-5}$).
* **Extended Implementation Insights & Verification:** To balance processing efficiency and geometric accuracy, the system runs the nested numerical solver inside a two-tier configuration. The integration step breaks down the intersecting chords using up to 500 spatial slices, lowering truncation errors to a baseline threshold of $O(h^4)$, which matches the expected theoretical upper bound error profile for Newton-Cotes frameworks. The bisection engine monitors interval convergence at each loop step, protecting the system from computational divergence or zero-division traps if a user inputs extreme target values (such as $<10\%$ or $>90\%$). The final converged tether radius is then output alongside a coordinate grid mask that validates the structural footprint of the grazing zone.

---

## Repository Structure

```text
├── Project_1_PRNG/
│   └── Fixed_Point_PRNG.ipynb         # Divergent Fixed-Point iteration PRNG script
├── Project_2_3Player_Chess/
│   ├── Coordinate_Routing.ipynb       # Spatial finite difference path calculation cell
│   └── Mesh_Visualizer.ipynb          # Polar coordinate transformation board renderer
└── Project_3_Goat_Grazing/
    ├── Root_Optimization.ipynb        # Simpson's 3/8 and Bisection integration solver
    └── Arena_Geometry_Visualizer.ipynb # Intersection matrix gradient mask renderer
