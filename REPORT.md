# YOLOv11n-CDL Reproduction + Low-Light Robustness Extension — Report

## Research question

Does CDL's design (ConvSmart + DSA + P2 head) improve YOLOv11n pavement-defect detection
under low light, does low-light training augmentation improve it further, and can a learned
illumination-correction module (AGE) add further robustness — including the brightness-gated
AGE extension tested as R5?

## Method

The tracked implementation is in `src/common.py` and `configs/`.

Experiment ladder:

- **R1:** stock YOLOv11n baseline
- **R2:** CDL — ConvSmart + DSA + P2 detection path
- **R3:** CDL + low-light training augmentation
- **R4:** CDL + augmentation + naive AGE
- **R5:** CDL + augmentation + brightness-gated AGE

The source notebook uses a frozen approximately 4,000-image RDD2022 subset with four defect
classes: D00, D10, D20, and D40.

## Existing run analysis

The following statements are carried over from the supplied notebook's existing outputs and
analysis. They have not been regenerated during the GitHub conversion.

- R2 improves clean-set mAP over R1 in the supplied run but does not materially improve the
  synthetic dark test sets.
- R3 improves the dark-condition metrics relative to R2, with a small clean-set trade-off.
- R4's naive AGE provides little additional dark-condition benefit over R3 while reducing
  clean-set performance.
- R5's brightness-gated AGE recovers the clean-set loss observed for R4 and improves the
  dark-condition metrics in the supplied run.

## Limitations

- The dark test sets are synthetic and are not equivalent to real nighttime imagery.
- The training and test corruption pipelines are deliberately different, but both belong to
  the broader darkening/noise family.
- The frozen experiment pool is much smaller than the full RDD2022 dataset.
- Contiguous filename-block splitting reduces but does not eliminate near-duplicate-frame
  leakage.
- Run-to-run variance means very small metric differences should be interpreted cautiously.
- AGE follows the supplied TinyDark-YOLO-inspired design; the brightness-gated R5 mechanism
  is the extension tested in this project.

See `docs/decisions_log.md` and the notebook's Limitations section for the detailed
experimental decisions and caveats.
