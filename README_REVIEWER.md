# LuViRA Reviewer Reproduction Package

Generated: 2026-09-13T16:24:30.189739+00:00

## Purpose

This package reproduces the numerical experiments, figures, tables,
model architectures, and reported-run evaluations used in the manuscript.

Run notebook Cells 1–21 in numerical order.

## Dataset location

The notebook expects the LuViRA dataset at:

    /data/luvira

## Experimental protocol

Grid trajectories:
- training: 35 odd-numbered usable grid IDs
- test: 33 even-numbered usable grid IDs

Retained aligned samples:
- train: 29,928
- test: 28,233

Radio / GT:
- retained row indices are 0, 5, 10, ...
- n_use = min(radio_rows, gt_rows)

Vision:
- RGB and depth are paired independently by nearest timestamp
  to the same retained radio/GT timestamp.

## Important distinction: reproduction vs reported-run verification

The package contains both:

1. Fresh independent retraining.
2. Exact evaluation of saved reported-run checkpoints/artifacts.

These are intentionally kept separate.

For example:
- fresh Cell-17 radio+depth fusion: approximately 42.9 mm
- exact reported-run Table-5 radio+depth fusion: 43.0 mm

The small retraining difference is not hidden.

## Figure 13 versus Table 7

Figure 13:
- 9 radio-usable random trajectories
- standalone heteroscedastic-NLL radio model
- historical random mean: approximately 1806.8 mm

Table 7:
- 5 fully multimodal random trajectories
- historical Radio column comes from Q6_random_predictions.csv
- fusion B/C/D are evaluated from their reported-run checkpoints
- Table-7 Mean row is a pooled sample-level mean

Do not interchange these populations or radio provenances.

## Main reproduced results

Standalone grid-test models:
- Radio: 53.2 mm
- Depth: 64.3 mm
- Colour: 122.0 mm

Oracle:
- 30.0 mm

Fusion Table 5:
- A Radio: 52.5 mm
- B Radio + Depth: 43.0 mm
- C Radio + Colour: 65.6 mm
- D Radio + Depth + Colour: 48.4 mm

Radio silent failure:
- Grid: 53.2 mm
- Random: 1806.8 mm
- Error inflation: 34x
- Predicted uncertainty increase: approximately 24.5%

Free-heading Table 7:
- Historical Radio: 2005 mm
- Radio + Depth: 1603 mm
- Radio + Colour: 2332 mm
- Radio + Depth + Colour: 1932 mm

## Directory structure

tables/
    Numerical outputs, verification tables, manifests, claim ledger.

figures/
    Reproduced manuscript and reviewer-audit figures.

models/
    Reproduced and reported-run model checkpoints.

reported_run_artifacts/
    Historical artifacts required to verify reported results,
    including Q6_random_predictions.csv.

cache/
    Large intermediate model-input and feature arrays.
    These are not included in the lightweight reviewer bundle.

## Manuscript reconciliation

The numerical reproduction is complete.

However, the current manuscript contains several statements that must
be corrected or clarified before resubmission.

See:

    tables/FINAL_manuscript_reconciliation_register.csv

The existence of this register is intentional. Reproduction differences
are documented rather than silently altered.

## Integrity

See:

    artifact_manifest.csv
    SHA256SUMS.txt

for artifact sizes and cryptographic hashes.

## Notebook

Save/export the final reviewer notebook itself as:

    /data/luvira/reports/reviewer_reproduction/LuViRA_reviewer_reproduction.ipynb

before sending the package to reviewers.
