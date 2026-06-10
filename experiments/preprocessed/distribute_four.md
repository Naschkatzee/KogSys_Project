grep -n "best val acc" runs_preprocessed/distribute_four/train.log | tail -
tail -30 runs_preprocessed/distribute_four/*/summary.json
cat runs_preprocessed/distribute_four/*/meta.json | grep num_features

The preprocessed distribute_four experiment used the corresponding symbolic feature dimensionality of 28 features. In contrast to the raw-data experiment, this run did not use the index-based loading pipeline. Instead, the metadata confirms that no index file directory was used, meaning that the model operated on the preprocessed symbolic dataset generated from the original I-RAVEN files.

The experiment achieved a best validation accuracy of 49.75% at epoch 122. At the final epoch, validation accuracy was lower, reaching approximately 47.22%, while training accuracy was approximately 65.14%. This indicates that the best model state occurred substantially before the end of training and that final-epoch performance slightly underestimated the strongest result obtained during optimization.

Compared with the original raw-data experiment, which achieved 48.91% validation accuracy at epoch 17, and the raw-data verification rerun, which achieved 50.29% at epoch 14, the preprocessed result falls within the same performance range. The differences between the raw and preprocessed versions are small and inconsistent in direction. The preprocessed run performed slightly better than the original raw run but slightly worse than the raw verification rerun. Therefore, preprocessing did not produce a meaningful improvement in predictive performance for distribute_four.

The training dynamics differed somewhat between the pipelines. The raw-data runs reached their best validation accuracies relatively early, whereas the preprocessed run continued improving until epoch 122. However, the final accuracy level remained almost unchanged across all versions. This suggests that preprocessing affected the optimization trajectory but not the overall capability of the model to solve the task.

The main advantage of the preprocessed pipeline was computational efficiency. By loading serialized symbolic representations directly, the model avoided repeatedly parsing the original dataset files during training. As a result, epochs were substantially faster than in the raw-data pipeline. However, this computational benefit did not translate into a substantial accuracy gain.

Overall, the preprocessed distribute_four experiment confirms the conclusions drawn from the raw-data experiments. The configuration remains challenging for the reproduced SCL architecture, and validation accuracy stays around 50% regardless of whether the raw or preprocessed data pipeline is used. This supports the interpretation that the limited performance on distribute_four is caused primarily by task complexity rather than by data-loading strategy.

