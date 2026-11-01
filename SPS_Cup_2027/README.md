# IEEE Signal Processing Cup 2027 — FaceVitals

This directory prepares the submission structure inside the existing Vital Detect
repository. It contains only this README and `.gitkeep` placeholders; submission
data, processing code, and evaluation tools will be added in future development.

Source: [2027 SP Cup Official Document — FaceVitals, Section 1.2, “Data organization” (PDF pages 10–11)](https://signalprocessingsociety.org/sites/default/files/2026-10/2027-SP-Cup-Official-Document-FaceVitals.pdf#page=10).
Task 1's permission to use MATLAB or Python also appears in Section 2.3.
This README summarizes the requested submission file organization, rather than
the complete competition regulations.

## Directory structure

The four directory names below reproduce the official document exactly.
The `.gitkeep` files are repository placeholders so Git tracks empty directories;
they are not official submission artifacts.

```text
SPS_Cup_2027/
├── Round1_Baseline/
│   └── .gitkeep
├── Round2_HR_SpO2/
│   └── .gitkeep
├── Round3_Constrained/
│   └── .gitkeep
├── Round4_FullSystem_Clinical/
│   └── .gitkeep
└── README.md
```

**Official document inconsistency:** The regulations describe three competition
rounds, but Section 1.2 lists four submission directories. All four names are
preserved here. The document does not explicitly resolve how the three rounds
map onto the four directories. In particular, the Round 3 full-system requirements
below must not be treated as an official mapping to either `Round3_Constrained/`
or `Round4_FullSystem_Clinical/`. That mapping needs clarification from the
organizers before submission; no fourth-round requirements are inferred here.

## File naming convention

Use `RoundX_Condition_Constraint.mat`:

- `RoundX`: Competition round number, as described for Rounds 1–3.
- `Condition`: Recording condition, such as `Baseline`, `LowLight`,
  `LowResolution`, or `LowBandwidth`.
- `Constraint`: Applicable constraint tag from Section 2, such as `C1`, `C4`,
  or `C7`; use `None` for the unconstrained baseline.

For example, `Round1_Baseline_None.mat` is the baseline Round 1 file.
Square brackets in `Round2_[Condition]_[Constraint].mat` mark placeholders to
replace with the tested condition and constraint tag.

## Round 1 — Heart Rate

Required submission files:

- `Round1_Baseline_None.mat`: Facial video and reference HR at baseline conditions.
- `target_video.mp4`: Raw facial video.
- `reference_signal.csv`: Synchronized ground-truth HR from a pulse oximeter or ECG.
- `processed_output.csv`: Estimated HR output.
- `process_round1.m`: Processing pipeline script, using the filename printed in
  the official PDF. Python is also permitted for the Task 1 pipeline; the PDF
  does not specify a separate Python script filename.

## Round 2 — HR + SpO2

Required submission files:

- `Round2_[Condition]_[Constraint].mat`: Facial video and reference HR and SpO2
  under the tested condition.
- `process_round2.m`: Processing script.
- `target_video.mp4`: Corresponding facial video.
- `reference_signal.csv`: Corresponding ground-truth HR and SpO2 channels.
- `processed_output.csv`: Corresponding estimated HR and SpO2 channels.

Section 1.2 extends the Round 1 corresponding files with SpO2 reference and
output channels. No additional per-parameter filenames or CSV schemas are
specified here.

## Round 3 — Full System

Required submission artifacts for HR, SpO2, and blood pressure (BP):

- Real-time processing code for the deployable pipeline.
- `target_video.mp4` or a live-stream log.
- `reference_signal.csv`: Ground-truth HR, SpO2, and BP signals.
- `processed_output.csv`: Real-time estimates for all three parameters.
- `benchmark_comparison.csv`: Comparison against a standard dataset or clinical
  reference device.

These requirements follow the document's three-round description and do not
resolve the directory mapping inconsistency noted above.

## Required MATLAB variables

Under “Folder Contents (for Tasks 1 and 2),” Section 1.2 requires each applicable
`.mat` file to contain all six variables:

| Variable | Contents |
| --- | --- |
| `facial_video` | Raw RGB facial video frames. |
| `roi_data` | Facial ROI coordinates or masks, including forehead and cheeks. |
| `reference_signal` | Ground-truth physiological signals for the round. |
| `processed_signal` | Estimated signals from the processing pipeline. |
| `metrics` | Evaluation results for the metrics listed below. |
| `params` | Camera resolution, frame rate, illuminance in lux, camera-to-subject distance, Fitzpatrick skin type, age, and applied Section 2 constraints. |

## Evaluation metrics

- Mean Absolute Error (MAE).
- Root Mean Square Error (RMSE).
- Pearson correlation coefficient (r).
- Bland–Altman limits of agreement.

For Task 1 HR evaluation, MAE and RMSE are expressed in beats per minute (BPM),
and correlation compares estimated HR with reference HR. This skeleton adds no
metric implementations, acceptance thresholds, data schemas, or fabricated
submission files.
