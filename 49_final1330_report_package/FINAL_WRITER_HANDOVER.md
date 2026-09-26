# FINAL TruFor adversarial-localisation writer handover

## Status

This document supersedes all provisional 966-image Phase-A reporting.

The complete frozen adversarial-evaluation population is now available and validated:

- frozen attack population: **1330**
- centrally available: **1330/1330**
- Stage-45 scientific-state audit: **PASS**
- Stage-45 failures: **0**
- classification preserved: **1330/1330**
- maximum physical L-infinity: **0.003921568627 = 1/255**

## Primary DC-DCEC-DCEW analysis

The primary spatial-evidence rule is the pre-specified study-defined majority criterion:

- `tau_E = 0.5`
- `tau_RRA = 0.5`

The RMA/E and RRA metrics are literature-aligned localisation measures, but `0.5/0.5` is **not claimed to be a universal literature-mandated cutoff**.

Human review is a sidecar interpretive experiment only and was not used to calibrate these thresholds.

Final primary result:

- clean DCEC: **436/1330 = 32.782%**
- document-stem clustered-bootstrap 95% CI:
  **30.318% to 35.360%**
- DCEW: **436/436 = 100%**
- classification flips within the clean-DCEC denominator: **0**
- E-only DCEW at `0.5/0.5`: **0**
- RRA-only DCEW at `0.5/0.5`: **0**
- both E and RRA below threshold: **436**

Thus every primary DCEW case retained the image-level attack decision while both spatial-evidence measures fell below the primary evidence threshold.

## Continuous evidence degradation

Across all **1330** attacked images:

- mean E:
  **0.550601 clean -> 0.003676 adversarial**
- median relative E degradation:
  **99.994%**
  with 95% clustered-bootstrap CI
  **99.993% to 99.995%**

- mean RRA:
  **0.499670 clean -> 0.008699 adversarial**
- median relative RRA degradation:
  **100.000%**

- median clean `mu_w`:
  **16.371255**
- median adversarial `mu_w`:
  **0.000693**

- median clean RRA lift:
  **13.768055**
- median adversarial RRA lift:
  **0.000000**

## Threshold sensitivity

The evidence thresholds were varied over the 3 x 3 grid:

- `tau_E`: 0.25 / 0.50 / 0.75
- `tau_RRA`: 0.25 / 0.50 / 0.75

Clean-DCEC denominators ranged from **21 to 1011 images**.

Conditional DCEW was 100% in all nine cells: **True**.

Specific decomposition:

- `(0.25, 0.25)`: 1011 DCEC / 1011 DCEW; 1 E-only, 1010 both
- `(0.50, 0.25)`: 774 DCEC / 774 DCEW; 1 E-only, 773 both
- all remaining threshold pairs: every DCEW case failed both E and RRA
- classification flips: 0 in every threshold-sensitivity cell

Interpretation: the clean-DCEC denominator is threshold-dependent, but the adversarial evidence-collapse conclusion is not dependent on the primary 0.5/0.5 choice.

## RRA tie robustness

RRA top-K cutoff ties occurred in:

- clean maps: **64**
- adversarial maps: **1141**

Maximum tie-induced RRA width:

- clean: **8.83198734e-06**
- adversarial: **1.67968422e-05**

Stage 47 confirmed:

- clean DCEC label changes under tie-min/tie-max: **0**
- adversarial DCEW label changes under tie-min/tie-max: **0**

Therefore the primary binary conclusions are insensitive to the recorded cutoff-tie ambiguity.

## Perturbation constraint

Stage 45 independently reopened every retained adversarial tensor and recomputed the perturbation.

Results:

- audited: **1330/1330**
- failures: **0**
- maximum E recomputation errors: numerical precision only
- maximum physical L-infinity:
  **0.003921568627 = 1/255**

The attack therefore respects the declared physical L-infinity budget.

## Compute cost

Use the per-image active attack wall time stored in each `result.json`, not raw shard calendar duration.

The latter contains workstation-specific interruptions such as WSL shutdown/restart and should not be used as portable scientific compute cost.

Final active-compute statistics:

- aggregate active GPU compute:
  **159.094 GPU-hours**
- mean:
  **7.177 min/image**
- median:
  **2.591 min/image**
- IQR:
  **0.715 to 12.418 min/image**
- 95th percentile:
  **25.456 min/image**
- active throughput:
  **8.360 images/hour**
- Spearman native megapixels vs active runtime:
  **rho = 0.9345**

Hardware:

`NVIDIA RTX PRO 5000 Blackwell`

The strong resolution/runtime relationship explains the highly skewed per-image runtime distribution.

## Manipulation-family summary

~~~text
              value   n  DCEC_n  DCEC_rate_all  DCEW_n  DCEW_rate_given_DCEC  E_clean_mean  E_adv_mean  RRA_clean_mean  RRA_adv_mean  A_median  mu_clean_median  mu_adv_median  RRA_lift_clean_median  RRA_lift_adv_median
          digital_1 153      81       0.529412      81                   1.0      0.555221    0.000698        0.647885      0.000119  0.141951         3.529308       0.001275               4.396326                  0.0
          digital_2 135       3       0.022222       3                   1.0      0.192353    0.000257        0.529934      0.000466  0.083335         1.762296       0.000080               6.317990                  0.0
          digital_3 786     282       0.358779     282                   1.0      0.642020    0.005003        0.480012      0.012459  0.027570        23.689218       0.000823              17.062328                  0.0
         facedancer 107       0       0.000000       0                   NaN      0.111944    0.000020        0.387024      0.000015  0.074975         1.494296       0.000024               5.799460                  0.0
textdiffuserft_bfei 149      70       0.469799      70                   1.0      0.703198    0.005453        0.504649      0.011373  0.041575        18.765848       0.002534              12.315046                  0.0
~~~

Important interpretation:

DCEC prevalence is not synonymous with all clean localisation information.

`facedancer` has **0/107** images satisfying the absolute 0.5/0.5 DCEC rule, but its continuous localisation metrics remain informative. Its small manipulated regions make an absolute `E >= 0.5` criterion particularly stringent.

`digital_2` similarly has only **3/135** clean-DCEC images despite median clean RRA above 0.5.

Therefore report continuous E, RRA, `mu_w` and RRA lift alongside the thresholded DCEC/DCEW analysis.

## Hardware summary

~~~text
      value   n  DCEC_n  DCEC_rate_all  DCEW_n  DCEW_rate_given_DCEC
     huawei 450     111       0.246667     111                   1.0
   iphone15  81      29       0.358025      29                   1.0
iphone15pro 358     215       0.600559     215                   1.0
       scan 441      81       0.183673      81                   1.0
~~~

## Split summary

~~~text
        value    n  DCEC_n  DCEC_rate_all  DCEW_n  DCEW_rate_given_DCEC
      dev_val  288      84       0.291667      84                   1.0
official_test 1042     352       0.337812     352                   1.0
~~~

## Scientific provenance

Frozen pretrained TruFor checkpoint SHA256:

`ac1d90e329a72e0d66e8665e123a19e94bfae3209c3ef8a4f9ca3b91578c7844`

Frozen adversarial protocol SHA256:

`5840aa9bee076b493c6a645e140edaad892373433c7e919e95ed4e60e44158d5`

Phase-2 execution-plan SHA256:

`e7e057388cc43f48931b93dfb3e2aead22df6ecea5a9769f6dc948ef29e88eeb`

Frozen pretrained image-level classification threshold:

`0.532955974340439`

Primary evidence thresholds:

`tau_E = 0.5`  
`tau_RRA = 0.5`

Evidence protocol:

`scripts/trufor/evidence_evaluation_protocol_v1.json`

Git branch at packaging:

`main`

Git commit at packaging:

`1422aa02711dbeb6b906eddccd0a7c0a5b298885`

## Recommended dissertation wording

> Across the complete 1,330-image clean-correct attack population, all adversarial examples retained TruFor's attack-class decision under the frozen image-level threshold. Spatial evidence nevertheless collapsed: mean relevance mass E decreased from approximately 0.551 to 0.0037, while mean RRA decreased from approximately 0.500 to 0.0087. Median relative degradation was 99.994% for E and 100% for RRA. Under the pre-specified study-defined majority criterion (`E >= 0.5` and `RRA >= 0.5`), 436 images qualified as decision-correct and evidence-correct; all 436 fell below both evidence thresholds after perturbation while retaining the attack-class decision. This result was unaffected by RRA tie resolution and conditional DCEW remained 100% throughout a 3 x 3 threshold-sensitivity analysis.

## Writer source hierarchy

Use the following in this order:

1. `FINAL_KEY_RESULTS.csv`
2. `data/48_final1330_primary_report_table.csv`
3. `data/47_final1330_reporting_summary.json`
4. `data/46_final1330_primary_summary.json`
5. `data/46_final1330_threshold_sensitivity.csv`
6. `data/46_final1330_subgroup_summary.csv`
7. `data/46_final1330_evidence_per_image.csv`
8. `data/45_final1330_scientific_state_summary.json`

The old Phase-A 966-image package is historical/provisional and must not be used for final dissertation values.
