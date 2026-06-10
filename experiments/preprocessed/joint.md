grep -n "best val acc" runs_preprocessed/joint/train.log | tail -
tail -30 runs_preprocessed/joint/*/summary.json
cat runs_preprocessed/joint/*/meta.json | grep num_features

| Configuration | Raw verified (%) | Preprocessed (%) | Joint preprocessed (%) |
|---------------|-----------------:|-----------------:|-----------------------:|
| center_single | 100.00 | 100.00 | 99.75 |
| distribute_four | 50.29 | 49.75 | 52.85 |
| distribute_nine | 47.64 | 47.77 | 52.20 |
| in_out | 100.00 | 100.00 | 99.80 |
| in_distri | 63.51 | 62.90 | 67.90 |
| left_right | 100.00 | 99.95 | 99.70 |
| up_down | 99.95 | 100.00 | 99.75 |
| **Overall (joint only)** | — | — | **82.03** |


The joint training experiment achieved a peak validation accuracy of **82.03%** at epoch 154. Performance on the simpler configurations remained near perfect, with accuracies between 99.7% and 99.8% for center_single, left_right, up_down, and in_out. Compared to the individually trained models, the largest improvements were observed on the more challenging configurations: distribute_four increased from approximately 50% to 52.9%, distribute_nine from approximately 48% to 52.2%, and in_distri from approximately 63% to 67.9%. These gains suggest that multi-task training allows the model to share useful relational representations across configurations, improving generalization on the hardest reasoning tasks while preserving near-perfect performance on the easier ones. Nevertheless, the distributed configurations remain substantially more difficult than the directional and structural tasks, indicating that joint training alleviates but does not eliminate the underlying reasoning challenges of these problem types.