# FINAL ResNet-18 harmonised evidence-reporting handover

## Status
This is a **post-hoc reporting analysis** over the completed 450-image
classification-preserving ResNet-18 localisation attack. The attack was not rerun.

Exact scientific archive: **450/450 bundles**. Stage-55 scientific audit: **PASS**.

## Common reporting framework
The same final evidence vocabulary used for TruFor is applied here:
DC, E/RMA, RRA, DCEC and DCEW.

ResNet-specific valid support is the exact stored `content_mask`, because the
model uses a fixed 512x864 canvas. Fixed horizontal padding is excluded.
GT is the exact stored `union_mask`.

Primary thresholds:
- tau_E = 0.5
- tau_RRA = 0.5

These are study-defined majority criteria, not universal literature cutoffs.

## Primary result
- classification preserved: **450/450**
- clean DCEC: **330/450 = 73.33%**
- DCEC 95% file-stem clustered-bootstrap CI:
  **67.65% to 78.91%**
- DCEW: **330/330 = 100.00% conditional on DCEC**
- DCEW 95% clustered-bootstrap CI:
  **100.00% to 100.00%**
- classification flips within DCEC: **0**
- DCEW decomposition: E-only **1**,
  RRA-only **0**, both **329**

## Continuous degradation
- mean E: **0.583972 -> 0.091559**
- median relative E degradation: **84.740%**
- mean RRA: **0.714313 -> 0.071822**
- median relative RRA degradation: **91.334%**
- median mu_w: **6.337872 -> 0.751376**
- median RRA lift: **8.025836 -> 0.461614**
- mean Pointing Game: **0.748889 -> 0.313333**
- max physical L_inf in source run: **0.003921585158**, approximately 1/255

## Threshold sensitivity
Same 3x3 grid as TruFor:
tau_E and tau_RRA in {0.25, 0.50, 0.75}.

DCEC denominator range: **41 to 450**.
Use `55_resnet18_threshold_sensitivity.csv` for exact DCEW rates/decomposition.

## Tie robustness
- clean cutoff ties: **6**
- adversarial cutoff ties: **23**
- DCEC label changes under tie-min / tie-max:
  **0 / 0**
- DCEW label changes under tie-min / tie-max:
  **0 / 0**

## Critical interpretation
DCEC/DCEW are a harmonised **reporting layer**, not the attack objective.
The executed source attack objective was `minimise_gradcam_E`.
Do not rewrite the experiment as though RRA or DCEC/DCEW were optimised.

Retain the earlier continuous ResNet metrics and use RRA/DCEC/DCEW alongside
them for cohesion with the TruFor chapter.

## Source hierarchy
1. `55_resnet18_primary_summary.json`
2. `55_resnet18_cluster_bootstrap_CI.csv`
3. `55_resnet18_threshold_sensitivity.csv`
4. `55_resnet18_subgroup_summary.csv`
5. `55_resnet18_continuous_metrics.csv`
6. `55_resnet18_harmonised_evidence_per_image.csv`
7. `55_resnet18_scientific_audit.json`
8. `55_resnet18_evidence_protocol_snapshot.json`

Checkpoint SHA256:
`25ad8b1482be20e9d5e450770d6970b820ebc9470c9da3c4ec46db2558009402`

RRA implementation:
`scripts/trufor/trufor_evidence_metrics.py`

RRA helper SHA256:
`c7efc786ee6bee1ef654b44abaffc56a5a621eff349a8c02d2dfbc002959df90`

Git commit:
`baf1caf41fb839bfe960ff491df3dc9017ae6085`
