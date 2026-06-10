grep -n "best val acc" runs_preprocessed/distribute_nine/train.log | tail -
tail -30 runs_preprocessed/distribute_nine/*/summary.json
cat runs_preprocessed/distribute_nine/*/meta.json | grep num_features

The preprocessed distribute_nine experiment used the corresponding symbolic feature dimensionality of 63 features. As in the other preprocessed experiments, the metadata confirms that no index file directory was used, indicating that the model operated on the serialized symbolic representations generated from the original I-RAVEN files rather than on the raw index-based loading pipeline.

The experiment achieved a best validation accuracy of 47.77% at epoch 70. At the final epoch, validation accuracy was lower, reaching approximately 45.49%, while training accuracy was approximately 66.74%. This shows that the strongest model state occurred well before the end of training and that evaluating only the final epoch would underestimate the best performance obtained during optimization.

Compared with the original raw-data experiment, which achieved 47.91% validation accuracy at epoch 66, and the raw-data verification rerun, which achieved 47.64% at epoch 7, the preprocessed result is almost identical. The differences between all three runs are below half a percentage point. This indicates that preprocessing did not materially affect predictive performance on the distribute_nine configuration.

Although the optimization trajectories differed slightly across runs, all versions converged to the same general accuracy range. The raw-data experiment reached its best result at epoch 66, the preprocessed experiment at epoch 70, and the raw verification rerun much earlier at epoch 7. Despite these differences in convergence timing, the final achievable performance remained stable at approximately 48%. This suggests that the model's limitation on distribute_nine is not caused by data loading or preprocessing, but by the complexity of the task itself.

The main advantage of preprocessing was computational efficiency. The preprocessed pipeline loaded symbolic representations directly from serialized files, avoiding repeated parsing of the original dataset during training. As a result, training epochs were substantially faster than in the raw-data pipeline. However, this efficiency improvement did not lead to an accuracy improvement.

Overall, the preprocessed distribute_nine experiment confirms the conclusions drawn from the raw-data experiments. The distribute_nine configuration remains one of the most challenging tasks for the reproduced SCL implementation, and validation accuracy stays below 50% regardless of whether the raw or preprocessed data pipeline is used. This supports the interpretation that the performance limitation is primarily caused by the complexity of distributed multi-object reasoning rather than by the choice of data preprocessing strategy.
