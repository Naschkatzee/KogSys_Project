# Replication of Wu et al. on the i-RAVEN Benchmark

This repository contains a replication study of the symbolic analogy model evaluated on the i-RAVEN benchmark.

## Overview

The goal of this project is to reproduce the results reported in the original paper using both:

- preprocessed symbolic features
- raw verified symbolic features
- joint and single-task training settings

The experiments evaluate performance on the seven standard i-RAVEN configurations:

- center_single
- distribute_four
- distribute_nine
- in_out
- in_distri
- left_right
- up_down

## Repository Structure

```text
runs_preprocessed/      # experiments using preprocessed symbolic features
runs_raw_verified/      # experiments using verified raw symbolic features
scripts/                # training and evaluation scripts
```

## Running Experiments

Example:

```bash
python train.py \
    --task center_single \
    --epochs 300 \
    --batch_size 128 \
    --lr 0.005
```

Joint training:

```bash
python train.py \
    --task center_single distribute_four distribute_nine \
           in_out in_distri left_right up_down
```

## Results Summary

The replication reproduces the main trends reported in the original work:

- near-perfect performance on simpler configurations
- moderate performance on `in_distri`
- lower performance on `distribute_four` and `distribute_nine`
- consistent improvements for difficult tasks under joint training

## Status

Current work includes:

- single-task experiments
- joint-training experiments
- multi-seed evaluation
- analysis of reproducibility and variance across random initializations

## License

This repository is intended for academic and research purposes.