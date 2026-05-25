# Anonymized Distribution Network Dataset for Probabilistic State Estimation

This repository provides the anonymized dataset used in:

> X. Huang, Y. Zhu, Y. Zhou\*, L. Xia, and Z. Yuan, "Entropy-Guided Iterative Probabilistic State Estimation for Distribution Networks with Sparse Measurements," *IEEE Transactions on Power Systems*, 2025.

## Overview

The dataset contains a 752-node medium-voltage distribution network derived from a real-world system. All node identifiers have been anonymized; no substation names, feeder names, or geographic information are included. The network topology and electrical parameters are preserved to allow full reproducibility of the experimental results.

## Repository Structure

```
├── sample_topology.csv       # 752-node admittance matrix (edges)
├── sample_input.csv          # Sample model input (one snapshot)
├── sample_output.csv         # Sample model output (predictions)
├── sample_edge_mask.csv      # Edge in-service status
├── 752system/
│   ├── DistTf.csv            # Distribution transformer nodes (load locations)
│   └── FeederFiles/
│       ├── branch_F02.csv    # Feeder F02 branch data
│       ├── branch_F09.csv    # Feeder F09 branch data
│       ├── branch_F14.csv    # Feeder F14 branch data (167-node subsystem)
│       └── branch_F31.csv    # Feeder F31 branch data (59-node subsystem)
```

## File Descriptions

### `sample_topology.csv`

Network admittance matrix in edge-list format.

| Column | Description |
|--------|-------------|
| `from_nd_id` | Source node ID (anonymized) |
| `to_nd_id` | Target node ID (anonymized) |
| `Y_real` | Real part of admittance (S) |
| `Y_imag` | Imaginary part of admittance (S) |

### `sample_input.csv`

A single snapshot of model input covering all 752 nodes.

| Column | Description |
|--------|-------------|
| `nd_id` | Node ID (anonymized) |
| `P_inj` | Active power injection (MW) |
| `Q_inj` | Reactive power injection (MVAr) |
| `V_mag` | Voltage magnitude (pu) |
| `V_angle` | Voltage angle (rad) |

### `sample_output.csv`

Model predictions corresponding to the sample input.

| Column | Description |
|--------|-------------|
| `nd_id` | Node ID (anonymized) |
| `V_mag_pred` | Predicted voltage magnitude (pu) |
| `V_mag_lower` | Lower bound of 2-sigma interval (pu) |
| `V_mag_upper` | Upper bound of 2-sigma interval (pu) |

### `sample_edge_mask.csv`

Edge in-service status mask.

| Column | Description |
|--------|-------------|
| `edge_id` | Edge index |
| `edge_mask` | 1 = in service, 0 = out of service |

### `752system/DistTf.csv`

Distribution transformer (load node) information.

| Column | Description |
|--------|-------------|
| `node_id` | Node ID (anonymized) |
| `P` | Active power (MW) |
| `Q` | Reactive power (MVAr) |
| `I` | Current (A) |

### `752system/FeederFiles/branch_F*.csv`

Per-feeder branch (edge) data with impedance parameters.

| Column | Description |
|--------|-------------|
| `EdgeNo` | Edge number |
| `F-Node` | From node ID |
| `T-Node` | To node ID |
| `r` | Resistance (pu) |
| `x` | Reactance (pu) |
| `b` | Susceptance (pu) |
| `Switch` | Whether a switch exists (Y/N) |
| `SwitchState` | Switch state (1 = closed) |
| `maxAmp` | Maximum current (A) |
| `type` | Component type |

## Three Test Systems

The paper evaluates on three systems extracted from this network:

| System | Nodes | Description |
|--------|-------|-------------|
| 752-node | 752 | Full feeder cluster |
| F14 | 167 | Subsystem defined by `branch_F14.csv` |
| F31 | 59 | Subsystem defined by `branch_F31.csv` |

## Citation

If you use this dataset, please cite the associated paper:

```bibtex
@article{huang2025entropy,
  author  = {Huang, X. and Zhu, Y. and Zhou, Y. and Xia, L. and Yuan, Z.},
  title   = {Entropy-Guided Iterative Probabilistic State Estimation for Distribution Networks with Sparse Measurements},
  journal = {IEEE Transactions on Power Systems},
  year    = {2025}
}
```

## License

This dataset is released for academic research purposes only. Commercial use requires explicit permission from the authors.
