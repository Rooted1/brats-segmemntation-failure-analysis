# BraTS Failure Mode Analysis: Under- vs Over-Segmentation in Brain Tumor MRI

## Project Overview
This project trains a 2D U-Net for brain tumor segmentation on the BraTS2020 dataset
and analyzes *where and why* the model fails — specifically, whether it tends to
under-segment (false negatives, missed tumor) or over-segment (false positives,
healthy tissue mislabeled as tumor), and whether that failure pattern correlates
with tumor size.

This question is motivated by the clinical stakes in chemotherapy targeting: a
false negative means under-treating remaining tumor, while a false positive risks
damaging healthy tissue. Model accuracy alone (e.g. Dice score) doesn't distinguish
between these two very different clinical failure modes.

## Research Question
Does a U-Net segmentation model's error type (false negative vs. false positive)
correlate with tumor size? Are small tumors disproportionately under-segmented?

## Dataset
[BraTS2020](https://www.kaggle.com/datasets/awsaf49/brats20-dataset-training-validation) —
multi-modal MRI (T1, T1ce, T2, FLAIR) with expert-annotated tumor sub-region masks.

## Methodology
1. **Preprocessing**: 3D volumes sliced into 2D axial cross-sections; per-patient,
   per-modality intensity normalization computed over brain-tissue voxels only
   (excludes background to avoid skewing statistics); slices filtered to those
   containing a meaningful tumor area (addresses class imbalance).
2. **Model**: 2D U-Net trained from scratch (no ImageNet pretraining — natural
   image features do not transfer well to multi-modal MRI, and BraTS provides
   sufficient scale for from-scratch training).
3. **Evaluation**: Dice score per patient/slice; false negative and false positive
   rates computed separately; error rates plotted against ground-truth tumor size
   to test for a size-dependent failure pattern.

## Project Status
- [ ] Data pipeline
- [ ] Baseline U-Net training
- [ ] Evaluation + Dice scoring
- [ ] Failure mode analysis (FN/FP vs. tumor size)
- [ ] Stretch: sub-region composition analysis
- [ ] Report
- [ ] Presentation

## Repo Structure
```
notebooks/   Kaggle/Colab notebooks (data prep, training, analysis)
src/         Reusable Python modules (dataset, model, metrics)
figures/     Generated plots and diagrams for the report
reports/     ACM-format report drafts
slides/      Presentation slides
```

## Author
Ruth Obe — MS in AI, UT Austin. AI in Healthcare course project.
