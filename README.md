# Entanglement Swapping Sandbox -- State-Based

A classroom-friendly, state-vector-based entanglement swapping simulator designed for two-year community colleges, upper-level undergraduate instruction, and self-guided early learners in quantum information science.

This repository contains a pure-state simulator for entanglement swapping, together with instructor-facing documentation and teaching materials. The project is intentionally scoped to keep the mathematics accessible while still showing the essential physics of branch-conditioned remote entanglement.

## Overview

Entanglement swapping is a protocol in which two qubits become entangled even though they never interacted directly. In this simulator:

- qubits **1 and 2** form source pair A
- qubits **3 and 4** form source pair B
- qubits **2 and 3** are measured in a selected Bell-state branch
- qubits **1 and 4** become the remote output pair

The simulator is built around a restricted source-state family of the form

\[
|\psi(\alpha,\phi)\rangle = \cos\alpha\,|00\rangle + e^{i\phi}\sin\alpha\,|11\rangle
\]

and reports:

- **branch probability**
- **concurrence**
- **fidelity to the ideal swapped target state**

The repository also includes simplified noise controls for:

- shot-to-shot parameter jitter
- imperfect source-state preparation
- imperfect Bell-state measurement (BSM)

These noise controls are implemented in a **pure-state Monte Carlo** picture: each shot is treated as a definite pure-state realization, and the reported noisy metrics are averages over repeated shots.

## Educational purpose

This project is designed to help learners connect:

- Dirac notation
- tensor-product basis states
- Bell-state measurement
- branch-conditioned outcomes
- entanglement measures
- the distinction between **entanglement strength** and **state closeness**

The main instructional goal is to provide a technically correct but accessible pathway from two source states to a swapped remote state.

## Scope and limitations

This simulator is intentionally simplified.

It does **not** attempt to be a full hardware-level or open-system model. In particular, the main implementation does **not** use:

- density matrices
- partial traces
- mixed states
- decoherence channels
- detector models
- full experimental imperfections

Instead, the repository uses a restricted pure-state model with effective source and BSM perturbations. This keeps the simulator suitable for early quantum instruction while still making the effects of imperfect preparation and imperfect measurement visible.

A more rigorous treatment would use density operators and quantum channels. That extension is discussed in the instructor report but is not the main focus of this repository.

## Repository contents

Typical contents include:

- `entanglement_swapper_jupyter_lab.ipynb`  
  Interactive simulator notebook with widgets and plots

- `entanglement_swapper_instructor_report.pdf`  
  Compiled instructor report

- `LICENSE`  
  Repository license

Adjust filenames above as needed to match the actual repository structure.

## Main concepts in the simulator

### 1. Source states
Each source pair is initialized in a Bell-like state controlled by:

- `α` for amplitude balance
- `φ` for relative phase

### 2. Bell-state measurement branch
The user selects a Bell-state branch at the hub:

- `Phi+`
- `Phi-`
- `Psi+`
- `Psi-`

### 3. Remote swapped state
Projecting qubits 2 and 3 onto the selected Bell branch produces a conditional remote state on qubits 1 and 4.

### 4. Metrics
The simulator reports:

- **Branch probability**: probability that the selected Bell branch occurs
- **Concurrence**: entanglement measure for the remote output state
- **Fidelity**: overlap of the noisy remote state with the ideal remote target state for the chosen settings

### 5. Noise dials
The simulator includes simple teaching dials for:

- `Δα noise`
- `Δφ noise`
- `Source noise`
- `BSM noise`

These are meant to illustrate sensitivity to imperfect preparation and imperfect hub measurement while remaining within a pure-state treatment.

## Why both concurrence and fidelity?

A key teaching point of the simulator is that these metrics answer different questions:

- **Concurrence** asks: how entangled is the remote state?
- **Fidelity** asks: how close is the remote state to the intended ideal target?

A state can remain significantly entangled while deviating from the exact target state. Showing both metrics helps students avoid conflating those ideas.

## Running the notebook

### Requirements

The notebook uses standard Python scientific tools and Jupyter widgets:

- Python 3.x
- `numpy`
- `matplotlib`
- `ipywidgets`
- `IPython`

Install with:

```bash
pip install numpy matplotlib ipywidgets notebook
