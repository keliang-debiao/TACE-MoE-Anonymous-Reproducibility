TACE-MoE Anonymous Reproducibility Package
This repository contains the anonymous reproducibility materials for TACE-MoE, a multi-evidence mixture-of-experts framework for binary classification of AI-generated and human-created images. The package provides the model implementation, experiment configurations, data-audit utilities, training and evaluation scripts, statistical analysis tools, tests, documentation, validation records, and manuscript-aligned reference tables.
Repository Contents
Path	Contents
src/tace_moe/	Core Python implementation of TACE-MoE and its supporting utilities.
scripts/	Executable programs for dataset recording, inventory construction, grouping, splitting, training, calibration, evaluation, robustness analysis, statistical analysis, table export, and repository validation.
configs/	YAML configuration files for the main model, datasets, baselines, ablations, and lightweight repository validation.
data/manifests/	Dataset registry, inventory schema, and documentation for locally generated audit and split-control manifests.
tests/	Unit tests covering evidence extraction, model and loss behavior, calibration, metrics, robustness transformations, data splitting, and bootstrap analysis.
docs/	Model, data, execution, output, anonymity, and reproducibility documentation.
artifacts/logs/	Repository-level validation, test, checksum, and structured validation records included with the package.
artifacts/manuscript_targets/	Machine-readable tables transcribed from the manuscript for post-run comparison. These files are isolated from model training and evaluation.


Model Implementation
The src/tace_moe/ package contains the following modules:
Module	Included functionality
model.py	TACE-MoE architecture, RGB encoder, independent evidence encoders, expert heads, entropy-aware router, adaptive feature fusion, and final prediction head.
evidence.py	Nearest-pixel residual construction, Haar high-frequency evidence extraction, frequency standardization, and image-derived routing statistics.
losses.py	Fused binary classification loss, expert supervision, cross-evidence contrastive loss, class-conditional discrepancy loss, and Brier regularization.
data.py	Dataset loading, preprocessing, manifest handling, and batch construction.
training.py	Fold-level optimization, checkpoint selection, prediction export, and run-record generation.
engine.py	Training and inference loops, early stopping, checkpoint writing, metric evaluation, and JSON output helpers.
calibration.py	Independent temperature scaling and calibrated probability generation.
metrics.py	Classification, discrimination, calibration, reliability, and selective-prediction metrics.
splits.py	Group-disjoint fold construction and partition-overlap checks.
audit.py	Decoded-image hashing, perceptual hashing, similarity-edge construction, connected-component grouping, and cross-partition auditing.
bootstrap.py	Group-level paired bootstrap comparison and multiple-comparison adjustment utilities.
robustness.py	Image perturbation operators and robustness-evaluation support.
baselines.py	Implementations and builders for the image-based comparison models defined by the repository configuration.
config.py	YAML loading, nested configuration access, and configuration serialization.
seed.py	Reproducible random-seed and data-loader worker initialization.
cli.py	Command-line interfaces for model inspection, split construction and checking, calibration, metrics, reliability analysis, risk-coverage analysis, and bootstrap comparison.


Workflow Scripts
The scripts/ directory includes:
Script	Purpose
00_capture_dataset_records.py	Captures source-dataset metadata and remote file listings.
01_build_inventory.py	Builds image inventories containing stable identifiers, labels, hashes, dimensions, codecs, file descriptors, and related audit fields.
02_extract_dinov2_embeddings.py	Extracts frozen DINOv2 embeddings used for similarity auditing.
02_build_groups.py	Constructs connected groups from pairing, hash, perceptual-hash, and embedding-based relationships.
03_build_splits.py	Generates group-disjoint fit, selection, calibration, and test partitions.
04_train_fold.py	Trains TACE-MoE for a selected fold and seed.
05_fit_temperature.py	Fits the independent temperature-scaling parameter from calibration predictions.
06_train_baseline.py	Trains a configured comparison model under the repository evaluation protocol.
07_train_external_checkpoint.py	Trains the development-only checkpoint used for frozen external evaluation.
08_evaluate_external.py	Evaluates a frozen checkpoint on a configured external dataset.
09_cluster_bootstrap.py	Performs paired group-level bootstrap comparisons.
10_run_robustness.py	Runs the configured clean and perturbed-image evaluations.
11_export_tables.py	Converts generated outputs into structured analysis tables.
12_validate_submission.py	Audits repository text and filenames for anonymous-submission constraints.
13_validate_repository.py	Runs repository-level structural and functional validation checks.
14_write_archive_checksums.py	Generates archive-wide SHA-256 checksums.
15_descriptor_distributions.py	Exports class-conditional image and file-descriptor distributions for acquisition-artifact auditing.


Configuration Files
- configs/tace_moe.yaml defines the main data partitions, preprocessing, evidence construction, model dimensions, objective weights, training settings, calibration procedure, metrics, bootstrap analysis, and robustness conditions.
- configs/datasets.yaml records the public dataset handles, expected class organization, dataset roles, and local data-root conventions.
- configs/baselines.yaml defines the comparison models and their shared selection, calibration, and hyperparameter settings.
- configs/ablations.yaml defines router-context variants, component ablations, calibration-factor combinations, and objective-weight sensitivity settings.
- configs/ci_validation.yaml provides a compact configuration for repository-level functional checks.
Data Manifests
The package includes dataset_registry.json, inventory_schema.json, and a manifest-directory guide. The repository code generates the remaining inventories, hashes, embeddings, grouping records, fold assignments, and overlap-audit files from locally obtained dataset snapshots.
Raw image datasets are not included in this repository. The package also excludes locally generated manuscript-scale checkpoints, cached embeddings, and prediction outputs.
Documentation
- docs/MODEL_CARD.md describes the intended task, architecture, objective components, outputs, and use limitations.
- docs/DATA_CARD.md describes the roles of the development and external datasets and the snapshot-recording policy.
- docs/EXECUTION.md records the end-to-end execution sequence and required audit checks.
- docs/AI_RUNBOOK.md provides a staged execution and evidence-retention workflow for an automated coding agent.
- docs/OUTPUT_CONTRACT.md defines checkpoint contents, prediction fields, metric conventions, statistical outputs, and separation of generated outputs from manuscript targets.
- docs/REPRODUCIBILITY_CHECKLIST.md summarizes the implemented reproducibility and audit controls.
- docs/ANONYMITY.md documents the safeguards applied to the anonymous review package.
Tests and Validation Materials
The tests/ directory contains checks for evidence transformations, model outputs, objective computation, calibration, metric calculation, perturbation behavior, group-disjoint splitting, and bootstrap analysis. The artifacts/logs/ directory contains the validation records packaged with this repository.
Manuscript Target Tables
The CSV files under artifacts/manuscript_targets/ are machine-readable transcriptions of manuscript tables. They are provided only as comparison targets after a complete run. Training, calibration, inference, aggregation, and statistical-analysis code do not use these files as inputs.
Anonymous Review Scope
The repository contains no author names, institutional affiliations, email addresses, ORCID identifiers, grant identifiers, private repository links, source-control history, or machine-specific absolute paths. Dataset paths are repository-relative or supplied at runtime.
