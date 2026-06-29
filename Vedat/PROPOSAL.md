# Proposal

The current QC-PINN framework evaluates six fixed ansatz topologies by brute-force comparison without analyzing *why* one outperforms another. As variational quantum circuits grow deeper or wider, gradients of the loss with respect to quantum parameters vanish exponentially — Var[∂L/∂θ] ~ 2^(-n) — making training increasingly difficult. This is the barren plateau problem, and more expressive ansatzes suffer from it more severely.

- arXiv:2503.16678 — https://arxiv.org/abs/2503.16678
- Holmes et al. 2022, PRX Quantum 3, 010313 — https://journals.aps.org/prxquantum/abstract/10.1103/PRXQuantum.3.010313

## Planned Approach

The convection-diffusion PDE is spatially local — the solution at any point depends only on its immediate neighbors, encoded in the Laplacian and gradient terms. This suggests that ansatzes with nearest-neighbor entanglement patterns should better match the structure of the problem and suffer less from barren plateaus than topologies with longer-range connectivity. The current best performer, cascade, uses ring connectivity which is already closer to local than cross_mesh (all-to-all), which may partly explain its advantage — but a brick-layer nearest-neighbor design would take this further in a principled way. The goal is to empirically verify this through gradient variance analysis of the existing six topologies and implement one or two new structure-aware ansatz variants for comparison.

- arXiv:2402.18619 — https://arxiv.org/abs/2402.18619

## Maestro

The benchmarking phase requires running many training trials across multiple ansatz topologies, each with different entanglement structures. Qoro Quantum's Maestro is an automated simulation engine that selects the optimal backend — state vector, MPS, tensor network, or GPU-accelerated — based on circuit structure. The plan is to wrap the PennyLane QNode execution in `DVQuantumLayer.py` with Maestro for forward passes and expectation value estimation, while keeping PennyLane's parameter-shift rule for gradient computation.
