# 10-Week Plan

**Week 1** — Run the convection-diffusion pipeline end to end. Read `DVQuantumLayer.py` and understand how the 6 ansatzes are implemented. Complete PennyLane variational circuit tutorials. Read the QCPINN paper and Holmes et al. 2022. Read Maestro documentation.

**Week 2** — Gradient variance analysis of the existing 6 ansatzes. Write a script to measure Var[∂L/∂θ] across random initializations for each topology. Plot results to characterize barren plateau severity per ansatz.

**Week 3** — Maestro feasibility. Install Maestro Python bindings, test with PennyLane circuits exported to QASM, and identify where in `DVQuantumLayer.py` the execution call can be intercepted. Test Automode on the 6 existing ansatz circuits and record which backend it selects for each.

**Weeks 4–5** — Design and implement 1–2 new PDE-informed ansatz variants in `DVQuantumLayer.py`. Primary candidate: brick-layer nearest-neighbor entanglement. Measure gradient variance for new ansatzes and compare to the week 2 baseline.

**Weeks 6–7** — Full benchmark. Run training pipeline for all existing and new ansatzes. Record L2 error, gradient variance, convergence curves, and parameter count. Use Maestro where feasible to accelerate batched runs.

**Week 8** — Hardware compilation analysis. Transpile all ansatzes to IBM heavy-hex topology via Qiskit and count CNOTs after transpilation.

**Weeks 9–10** — Writeup and presentation. Three figures: gradient variance comparison, L2 error and convergence curves, CNOT count on IBM heavy-hex. 4–6 page technical report. Intern presentation to Aditya.
