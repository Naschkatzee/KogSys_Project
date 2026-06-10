grep -n "best val acc" runs/left_right/*/log.log | tail -1
tail -30 runs/left_right/*/summary.json
cat runs/left_right/*/meta.json | grep num_features

The left_right configuration used the corresponding symbolic feature dimensionality of 8 features.

The left_right experiment was conducted using the same experimental setup as the previous configurations in order to maintain comparability across the replication study. Training was performed for 300 epochs using the Adam optimizer with a learning rate of 0.005 and a weight decay of 0.01. The training batch size was set to 128 and the evaluation batch size to 32. The experiment employed the raw index-based data loading pipeline, where symbolic representations were generated directly from the original I-RAVEN dataset during training and evaluation.

The experiment completed successfully and achieved a best validation accuracy of 100.0% at epoch 22. Performance improved rapidly during the initial training stages, and perfect validation accuracy was reached within the first few dozen epochs. Although training continued for the full 300 epochs, no further improvement beyond the perfect score was possible. Validation performance remained extremely high throughout the remainder of training, with only minor fluctuations around the optimum.

Compared to the distribute_four and distribute_nine configurations, the left_right task proved substantially easier for the replicated SCL model. The architecture was able to learn the underlying symbolic relations efficiently and generalize almost perfectly to unseen examples. The near-identical training and validation performance observed during later stages of optimization suggests that the learned representations generalized robustly and that overfitting was minimal.

The strong performance is likely related to the structural properties of the task. Unlike the distributed configurations, which require reasoning over multiple objects arranged in larger spatial layouts, the left_right configuration involves a comparatively constrained relational structure. The model therefore faces a smaller combinatorial reasoning space and can more readily learn the relevant symbolic patterns.

From a technical perspective, the experiment further confirms the correctness and stability of the adapted implementation. Training completed without numerical instability, divergence, or implementation-related issues. The successful reproduction of near-perfect performance on this configuration provides additional evidence that the compatibility modifications introduced during the replication process preserved the intended functionality of the original model.

Together with the center_single results, the left_right experiment demonstrates that the replicated SCL architecture is capable of achieving near-perfect performance on several I-RAVEN configurations. At the same time, the contrast between these results and those obtained on distribute_four and distribute_nine highlights the substantial variation in task difficulty across the benchmark and suggests that the main challenges for the replicated model arise in configurations requiring more complex multi-object reasoning.
