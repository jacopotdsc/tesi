# Thesis Citation Guide

This file defines the citation keys and the intended use of the main references
for the thesis. When generating LaTeX text, use the keys exactly as written
below. Do not introduce author--year keys or alternative aliases.

## General rules

- Cite a source only when it supports the specific statement being made.
- Prefer primary papers over surveys for technical claims.
- Use `legged_optimization` for broad classifications and background.
- Do not cite the TITA and Lite3 overview files as scientific references.
- Preserve acronyms and capitalization through the braces already used in the
  BibTeX titles.
- Avoid grouping many interchangeable citations. Two or three complementary
  sources are normally sufficient.

## Model-based locomotion

- `legged_optimization`: general survey of optimization-based legged-robot
  control, reduced models, trajectory optimization, WBC, and MPC.
- `cheetah_mpc`: classical convex SRBD MPC for quadrupedal locomotion; use for
  online ground-reaction-force optimization with a reduced model.
- `whole_body_nmpc`: whole-body nonlinear MPC through contacts; use when
  contrasting full-order and reduced-order formulations.
- `fast_whole_body_mpc`: real-time whole-body MPC obtained by accepting limited
  numerical accuracy. Correct arXiv identifier: `2407.10789`.

## Wheeled-legged locomotion

- `wheeled_legged_survey`: general overview and classification of
  wheeled-legged robots.
- `keep_rollin`: whole-body motion control and planning for wheeled quadrupeds.
- `rolling_deep`: hybrid rolling and stepping locomotion through online
  trajectory optimization.
- `wheeled_whole_body_mpc`: whole-body MPC with moving wheel contacts and online
  gait-sequence adaptation.
- `racing_wheeled_quadruped`: high-speed wheeled-quadruped racing, load
  transfer, active roll control, and stability limits.

## End-to-end reinforcement learning

- `challenging_terrain`: learned quadrupedal locomotion on difficult terrain;
  useful for teacher--student training and sim-to-real transfer.
- `parallel_rl`: massively parallel GPU simulation for rapid RL training.
- `perceptive_rl`: perceptive quadrupedal locomotion with noisy exteroception
  and sim-to-real deployment.
- `ppo`: original PPO algorithm used to train the policies in this thesis.

## Residual and hybrid learning

- `residual_robot_control`: foundational residual RL formulation in which a
  learned correction is added to a conventional controller.
- `model_gap`: learned correction of the mismatch between reduced-order and
  full-order quadruped models.
- `modular_residual`: residual learning distributed across modules of a
  model-based locomotion architecture.
- `deep_tracking`: model-based trajectories used as targets for a learned
  tracking controller; this is not a torque-level residual architecture.
- `adaptive_rl_mpc`: adaptive architecture in which RL changes model,
  swing-control, and gait-frequency components of MPC.
- `non_gaited_rl_mpc`: hierarchical architecture in which RL provides contact
  and navigation commands to a lower-level MPC.
- `residual_mpc`: closest published reference to the thesis architecture; MPC
  and RL operate concurrently and their outputs are blended at torque level.

## GPU-accelerated optimal control

- `cusadi`: GPU batching of symbolic expressions and many optimal-control
  instances.
- `relu_qp`: GPU-accelerated quadratic programming based on an unrolled ADMM
  structure.
- `parallel_lqr`: associative-scan formulation for temporal parallelization of
  dynamic programming and LQR.
- `mpx`: main framework reference. Use for primal-dual iLQR, temporal and
  state-space parallelization, JAX implementation, and MPC-in-the-loop
  reinforcement learning.

## Simulation

- `mujoco`: original MuJoCo physics-engine paper.

## Recommended citation combinations

- Reduced-order MPC and WBC: `\cite{legged_optimization,cheetah_mpc}`.
- Full-order versus reduced-order MPC:
  `\cite{whole_body_nmpc,cheetah_mpc}`.
- Evolution of wheeled-legged control:
  `\cite{keep_rollin,rolling_deep,wheeled_whole_body_mpc}`.
- End-to-end RL and GPU simulation:
  `\cite{challenging_terrain,parallel_rl,perceptive_rl}`.
- Motivation for residual learning:
  `\cite{residual_robot_control,model_gap,residual_mpc}`.
- Comparison of hybrid architectures:
  `\cite{adaptive_rl_mpc,non_gaited_rl_mpc,residual_mpc}`.
- GPU acceleration of MPC:
  `\cite{cusadi,relu_qp,parallel_lqr,mpx}`.

## Key mapping from earlier drafts

- `amatucci2026mpx` -> `mpx`
- `eisman2026racing` or `racing` -> `racing_wheeled_quadruped`
- `kamohara2025rlaugmented` or `adaptive_mpc` -> `adaptive_rl_mpc`
- `patrizi2026augmented`, `patrizi2026rlaugmented`, or `non_gaited` ->
  `non_gaited_rl_mpc`
- `jeon2025residualmpc` or `jeon2025residual` -> `residual_mpc`
- `todorov2012mujoco` -> `mujoco`
- `schulman2017ppo` -> `ppo`

## Corrections to the imported reference list

- Khazoom et al., *Tailoring Solution Accuracy for Fast Whole-Body Model
  Predictive Control of Legged Robots*: arXiv `2407.10789`, not `2407.13698`.
- Chen and Nguyen, *Learning Agile Locomotion and Adaptive Behaviors via
  RL-Augmented MPC*: arXiv `2310.09442`, not `2309.09442`. This paper is not in
  the current core `.bib`; add it only if it is actually cited.
