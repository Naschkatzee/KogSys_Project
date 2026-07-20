# Replication and Extension of the Scattering Compositional Learner on the I-RAVEN Benchmark

This repository contains the implementation and experimental results for a replication study of the **Scattering Compositional Learner (SCL)** proposed by Wu et al. on the **I-RAVEN** benchmark. In addition to reproducing the original visual reasoning pipeline, the project extends the original work with experiments with symbolic inputs.

---

## Repository Structure

```text
.
├── i-raven/                         # I-RAVEN dataset utilities
└── scl/                             # SCL implementation
    ├── runs_non-preprocessed_1/     # Results using non-preprocessed symbolic inputs (first run)
    ├── runs_non-preprocessed_2/     # Results using non-preprocessed symbolic inputs (second run)
    ├── runs_preprocessed/           # Results using preprocessed symbolic inputs
    ├── runs_seeds/                  # Results using different seeds
    └── runs_visual/                 # Results using visual inputs
```

---

## Experiments

The following experiments were conducted:

1. Visual inputs vs. Symbolic inputs
2. Preprocessed vs. Non-preprocessed symbolic inputs
3. Reproducibility of the symbolic pipeline
4. Single-task vs. Joint training
5. Stability across multiple random seeds

---

## Reproducing the Experiments

### Visual-input experiments

Visual experiments require preprocessing before training.

#### Preprocessing

```bash
python scripts/preprocess.py \
  --data-dir ../i-raven/full_data \
  --task center_single distribute_four distribute_nine left_right up_down in_out in_distri \
  --n 1000 \
  --use-visual-inputs
```

#### Single-task training

```bash
python main.py \
  --data-dir ../i-raven/full_data \
  --task <TASK> \
  --use-visual-inputs \
  --epochs 300 \
  --batch-size 128 \
  --eval-batch-size 32 \
  --lr 0.005 \
  --weight-decay 0.01 \
  --dump-dir ./runs_visual/<TASK>
```

where `<TASK>` is one of

- center_single
- distribute_four
- distribute_nine
- left_right
- up_down
- in_out
- in_distri

#### Joint training

```bash
python main.py \
  --data-dir ../i-raven/full_data \
  --task center_single distribute_four distribute_nine left_right up_down in_out in_distri \
  --use-visual-inputs \
  --num-features 80 \
  --epochs 300 \
  --batch-size 128 \
  --eval-batch-size 32 \
  --lr 0.005 \
  --weight-decay 0.01 \
  --dump-dir ./runs_visual/joint
```

---

### Random-seed experiment

To evaluate the stability of the joint symbolic model, the experiment was
repeated with five random seeds. The same seed was supplied to Python, NumPy,
and PyTorch for each run.

```bash
for seed in 0 1 2 3 4
do
  python main.py \
    --data-dir ../i-raven/full_data \
    --task center_single distribute_four distribute_nine left_right up_down in_out in_distri \
    --num-features 63 \
    --epochs 300 \
    --batch-size 128 \
    --eval-batch-size 32 \
    --lr 0.005 \
    --weight-decay 0.01 \
    --random-seed "$seed" \
    --numpy-random-seed "$seed" \
    --torch-random-seed "$seed" \
    --dump-dir "./runs_seeds/joint_seed${seed}"
done
```

---

## Experimental Results

The experiments show that

- the symbolic SCL pipeline can be successfully reproduced,
- symbolic inputs outperform visual inputs,
- preprocessing has only a small influence on final accuracy,
- joint training improves performance on the more challenging I-RAVEN configurations,
- the implementation produces stable results across different random seeds.

---

## Citation

This repository accompanies the Bachelor's project


The original model is described in:

Wu, Y., et al. *Scattering Compositional Learner: Discovering Objects, Attributes, Relationships and Rules from Abstract Visual Reasoning Problems.*
