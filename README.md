# 📌 Interpretable Cyber-Physical Attack Detection in Smart Grids

## A Leakage-Controlled Multi-Testbed Evaluation of Fusion, Robustness, and Observability Limits

## 👥 Authors

- **Muhammad Ridwanul Hoque**
  *INQUIRE Laboratory and School of Electrical and Computer Engineering, University of Oklahoma, Norman, OK, USA*
- **Sarah Sharif**
  *INQUIRE Laboratory and School of Electrical and Computer Engineering, University of Oklahoma, Norman, OK, USA*
- **Reza Saeed Kandezy**
  *School of Electrical and Computer Engineering, University of Oklahoma, Norman, OK, USA*
- **Yaser Banad\***
  *INQUIRE Laboratory and School of Electrical and Computer Engineering, University of Oklahoma, Norman, OK, USA*

\*Corresponding author: bana@ou.edu

[![License: Noncommercial](https://img.shields.io/badge/License-Noncommercial-blue.svg)](LICENSE)

## 📄 Abstract

Cyber-physical smart-grid detectors are typically treated as black boxes and validated exclusively on clean, temporally shuffled datasets, which risk overly optimistic performance claims. This work presents a multi-testbed evaluation study built around an interpretable, time-windowed fusion Random Forest, adopting the pessimistic result whenever evaluation protocols disagree. (i) On a public paired cyber-physical dataset, shuffled cross-validation is optimistic: macro-F1 falls from 0.96 to 0.88 ± 0.06 under rolling-origin temporal evaluation. A topology-free graph convolutional network (GCN) serving as a control confirms that this lightweight model is competitive on these splits. (ii) The adaptive and adaptive-joint feature-space attacks, which are infeasible as realistic grid manipulations, degrade macro-F1 to 0.67 and 0.34 respectively. Adversarial training and randomized smoothing partially restore performance, and a physics-constrained evolution-strategy evasion on the IEEE 14-Bus testbed shows the same vulnerability pattern. (iii) On real IEC-104 traffic, the cyber view reliably catches structural attacks (recall of 0.87 to 0.98) but largely fails on semantic value manipulation (recall of 0.11 to 0.35). An observability taxonomy on the IEEE 14-Bus system reveals that stealthy false data injection defeats all three observation views. (iv) On a full AC weighted least-squares state-estimation testbed, a forecasting-aided temporal test is evaded by slow ramps precisely where a rate-invariant physics-manifold test sustains detection at a common 5% false-alarm target. A full end-to-end evaluation on IEEE 118-Bus confirms the ordering but bounds its strength: the manifold test detects every trial down to 0.05°/step and 0.48 at 0.02°/step, against 0.14 for the temporal test.

## 🗂️ Repository Contents

| Script | Result in the paper |
|---|---|
| `build_features.py` | Builds the 1,529 fused 0.5 s windows of dataset 1. **Run first.** |
| `cyber_physical_fusion.py` | Physical vs. cyber vs. fusion detection |
| `ornl_baseline_shap.py` | SHAP feature importances |
| `exp1_blocked_cv.py` | Shuffled vs. time-blocked CV vs. chronological hold-out |
| `exp8_rolling_origin.py` | Rolling-origin temporal evaluation (0.88 ± 0.06) |
| `exp10_temporal_baselines.py` | Five model families under shuffled and rolling-origin protocols |
| `exp10b_lstm_optional.py` | Optional recurrent LSTM baseline (needs a deep-learning backend) |
| `exp2_gnn_headtohead.py` | Topology-free GCN control |
| `advanced_experiments.py`, `adversarial_robustness.py` | Feature-space attacks, adversarial training, randomized smoothing |
| `selective_detection.py` | Risk-coverage and selective abstention |
| `exp3_feasible_advtrain.py`, `exp3_run.py`, `exp3b_testbed2_ci.py` | IEEE 14-Bus physics-feasible FDI and evolution-strategy evasion |
| `iec104_crossval.py`, `iec104_hmi_crossval.py` | Real IEC-104 behavioral attacks |
| `exp4_semantic_fusion.py`, `exp4b_taxonomy_ci.py` | Observability taxonomy (20 seeds, Wilson 95% CIs) |
| `exp5_ac_stealth_temporal.py` | Full AC WLS estimator; stealthy FDI vs. bad-data detection |
| `exp6_manifold_detector.py`, `exp6_submission.py` | Temporal, manifold and fused detectors at 50 trials/point, common 5% false-alarm target |
| `exp6b_ksweep.py` | Manifold-dimension sensitivity sweep |
| `exp7c_ieee118_full.py` | Full end-to-end IEEE 118-Bus validation (resumable) |
| `exp9_manifold_attacker.py` | Manifold-aligned attacker bound |
| `regen_all_figs.py` | Regenerates every paper figure from the files in `results/` |

Scripts kept for reference only: `exp5_submission.py` (withdrawn ramp curves), `exp7_ieee118.py`, `exp7_bench.py` and `exp7b_ieee118_partial.py` (superseded by `exp7c_ieee118_full.py`).

## ⚙️ Setup

```bash
pip install -r requirements.txt
```

## 📊 Data

The datasets are not redistributed here.

- **Dataset 1:** SmartGrid-CyberPhysical-Attack-Dataset, IEEE DataPort, doi:10.21227/symr-bz19. Place it under `Dataset/`.
- **Dataset 3:** ICS dataset for smart grid anomaly detection (Matoušek et al.), IEEE DataPort, doi:10.21227/1trw-n685. Place it under `data/`.
- **IEEE 14-Bus and 118-Bus testbeds:** generated inside the scripts with `pandapower`; no download is needed.

## 🔁 Reproducibility Notes

- Random seeds are fixed in every script (seed 42 unless stated otherwise).
- Detector thresholds are calibrated on independent benign streams to a common 5% false-alarm target. On IEEE 14-Bus the rates measured on 400 held-out benign streams are 4.5%, 5.3% and 5.0% (temporal, manifold, fused).
- The benign manifold is fitted on **estimated** states, the output an operator actually observes, and its dimension is selected by cross-validation on benign streams only: K = 6 on IEEE 14-Bus and K = 8 on IEEE 118-Bus.
- All numerical outputs used by the figures are in `results/`.

## 📝 License

Original INQUIRE Lab code is licensed under the PolyForm Noncommercial License 1.0.0 (`LICENSE-CODE.txt`). Original INQUIRE Lab data, figures, and documentation are licensed under CC BY-NC 4.0 (`LICENSE-MATERIALS.txt`). See [LICENSE](LICENSE) for the scope. Datasets and software from other rights holders keep their original terms.

## 📚 Citation

If you use this code, please cite the associated article (citation details will be added on publication).
