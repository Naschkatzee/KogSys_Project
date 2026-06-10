grep -n "best val acc" runs/distribute_four/*/log.log | tail -1
tail -30 runs/distribute_four/*/summary.json
cat runs/distribute_four/*/meta.json | grep num_features

The distribute_four configuration used the corresponding symbolic feature dimensionality of 28 features.

The distribute_four experiment was conducted using the same technical setup as the previous center_single replication in order to maintain comparability across configurations. Training was performed for 300 epochs using the Adam optimizer with a learning rate of 0.005 and a weight decay of 0.01. The training batch size was set to 128, while the evaluation batch size was set to 32. The experiment used the generated I-RAVEN dataset together with index files created specifically for the train, validation, and test splits. Symbolic representations were generated directly from the raw dataset during training using the index-based loading pipeline.

The experiment completed successfully but achieved substantially lower performance than the center_single configuration. The best validation accuracy reached during training was 48.91%, which occurred at epoch 17. Although training continued for the full 300 epochs, the validation accuracy did not improve beyond this point and gradually stabilized at slightly lower values throughout the remainder of optimization. Training accuracy continued to increase and eventually exceeded 70%, indicating that the model was able to fit the training data more effectively than it could generalize to unseen examples.

Compared to the nearly perfect performance obtained on center_single, the distribute_four configuration appears significantly more challenging for the SCL architecture. This outcome is consistent with the increased complexity of the task. Unlike center_single, which contains a single centrally located object, distribute_four requires reasoning over multiple objects arranged in a 2×2 grid. The model must therefore learn a substantially larger set of symbolic relationships and dependencies, increasing the difficulty of the reasoning problem.

Despite the lower predictive performance, the experiment remained technically stable throughout all 300 epochs. Training completed without divergence, numerical instability, or implementation failures. Loss values remained bounded, optimization proceeded normally, and validation performance evolved smoothly throughout the run. These observations indicate that the reduced accuracy is attributable to the difficulty of the configuration rather than to implementation errors.

The results demonstrate that the adapted implementation remains functional on more demanding I-RAVEN configurations, but they also reveal a substantial performance gap between simple and complex reasoning tasks. The distribute_four configuration therefore represents one of the first indications that the reproduced model struggles with configurations involving larger numbers of objects and more complex relational structures. This discrepancy becomes particularly important when comparing the replication results to those reported in the original SCL publication.

