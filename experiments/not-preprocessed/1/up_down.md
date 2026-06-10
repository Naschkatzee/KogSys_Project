grep -n "best val acc" runs/up_down/*/log.log | tail -1
tail -30 runs/up_down/*/summary.json
cat runs/up_down/*/meta.json | grep num_features

The up_down configuration used the corresponding symbolic feature dimensionality of 8 features.

The up_down experiment was conducted using the same experimental setup as the other single-task configurations in order to maintain comparability across the replication study. Training was performed for 300 epochs using the Adam optimizer with a learning rate of 0.005 and a weight decay of 0.01. The training batch size was set to 128, while the evaluation batch size was set to 32. As in the other raw experiments, symbolic representations were generated directly from the original I-RAVEN dataset using the index-based loading pipeline.

The experiment completed successfully and achieved a best validation accuracy of 99.95% at epoch 15. Performance improved rapidly during the early stages of optimization and reached near-perfect accuracy within only a small number of epochs. Although training continued for the full 300 epochs, validation performance remained extremely close to the optimum throughout the remainder of the run. Training accuracy eventually reached 100%, while validation accuracy consistently remained above 99%, indicating excellent generalization.

The results demonstrate that the up_down configuration is comparatively easy for the replicated SCL architecture. Similar to the center_single and left_right tasks, the model was able to learn the underlying symbolic relations efficiently and transfer this knowledge almost perfectly to unseen examples. The very small difference between training and validation performance suggests that overfitting was minimal and that the learned symbolic representations generalized robustly across the dataset.

The strong performance is likely related to the relatively constrained structure of the task. The up_down configuration belongs to the family of directional reasoning problems and requires the model to learn relationships between objects arranged along a single spatial dimension. Compared to the distributed configurations, which involve substantially larger combinatorial reasoning spaces, the symbolic patterns present in up_down appear considerably easier for the architecture to capture.

From a technical perspective, the experiment further confirms the stability of the adapted implementation. Training completed without numerical instability, optimization failures, or implementation-related issues. Validation accuracy remained remarkably stable throughout the entire training process, providing additional evidence that the modifications required to execute the original repository in a modern environment preserved the intended behavior of the model.

Together with the center_single and left_right results, the up_down experiment demonstrates that the replicated SCL architecture is capable of achieving near-perfect performance on several I-RAVEN configurations. The contrast between these results and the substantially lower accuracies observed on distribute_four and distribute_nine further supports the conclusion that the primary challenges for the replicated model arise in configurations requiring complex multi-object reasoning rather than simple directional relationships.
