# Stage-52 portrait qualitative figure conventions

Each example is a portrait-oriented 3-row x 2-column figure:

Row 1:
- bona fide counterpart
- clean forged / attack input

Row 2:
- clean TruFor anomaly map overlaid on the forged input
- adversarial TruFor anomaly map overlaid on the adversarial input

Row 3:
- adversarial image preview
- 100x absolute perturbation

The bona fide counterpart is matched exactly by:
- file_stem
- hardware_source

When split metadata are present, a split match is preferred.

The cyan GT contour is deliberately thicker than the previous Stage-50 display
so that it remains visible when the figure is reduced to a portrait
dissertation page.

The legend is embedded inside every panel:
- Inferno colour bar: TruFor anomaly score, fixed 0..1 scale
- dark/purple = lower anomaly evidence
- yellow/white = higher anomaly evidence
- cyan contour = manipulated-region ground truth
- perturbation is magnified 100x for visibility

Clean and adversarial anomaly maps are not independently renormalised.

The five family examples are selected automatically using clean-state metrics,
restricted to images with an exact bona fide pair. The sixth panel is an
explicit residual-evidence stress case and must not be described as
representative.
