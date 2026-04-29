# Cahn-Hilliard on a Sphere

This repository contains small FEniCS experiments for solving the Cahn-Hilliard equation on the surface of a sphere. The main workflow loads a volumetric sphere mesh from `data/sphere.xml`, extracts its boundary as a surface mesh, and evolves a phase field on that curved geometry.

The core implementation in `surface_ch.ipynb` uses a mixed `P1-P1` finite-element formulation for the order parameter and chemical potential, solves the nonlinear system with FEniCS' `NonlinearVariationalSolver`, and adapts the timestep based on Newton convergence. Solutions are written to `.pvd` files for visualisation.

The surface free energy used in the main notebook is

```math
E(\phi)
= \int_\Gamma \left(
\frac{\varepsilon}{2} |\nabla_\Gamma \phi|^2
+ \frac{1}{\varepsilon} W(\phi)
\right)\, \mathrm{d}S,
```

with double-well potential

```math
W(\phi) = 18 \Lambda \bigl(\phi(1-\phi)\bigr)^2.
```

Here, `\Gamma` is the sphere surface, `\phi` is the phase field, `\nabla_\Gamma` denotes the surface gradient, `\varepsilon` controls the interface width, and `\Lambda` sets the strength of the bulk potential.

Repository contents:

- `surface_ch.ipynb`: main surface Cahn-Hilliard solver on the spherical boundary mesh.
- `surface_cells.ipynb`: extended coupled surface model with additional fields.
- `surface_mesh.ipynb`: earlier 1D / mesh prototyping notebook.
- `data/sphere.xml`: input mesh used to construct the sphere surface.
