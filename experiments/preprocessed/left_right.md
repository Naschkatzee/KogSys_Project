grep -n "best val acc" runs_preprocessed/left_right/train.log | tail -
tail -30 runs_preprocessed/left_right/*/summary.json
cat runs_preprocessed/left_right/*/meta.json | grep num_features

The preprocessed left_right experiment used the corresponding symbolic feature dimensionality of 8 features. As in the other preprocessed experiments, the metadata confirms that no index file directory was used, indicating that the model operated on serialized symbolic representations generated from the original I-RAVEN files rather than on the raw index-based loading pipeline.

The experiment achieved a best validation accuracy of 99.95% at epoch 205. At the final epoch, validation accuracy remained almost identical at approximately 99.90%, while training accuracy reached approximately 99.97%. This demonstrates that the model solved the left_right configuration almost perfectly under the preprocessed setting and maintained stable performance throughout the later stages of training.

Compared with the original raw-data experiment, which achieved 100.0% validation accuracy at epoch 22, and the raw-data verification rerun, which also achieved 100.0% at epoch 105, the preprocessed run produced essentially the same result. The numerical difference between 99.95% and 100.0% is negligible and does not indicate a meaningful reduction in model performance. All versions confirm that the left_right configuration is highly tractable for the reproduced SCL architecture.

The preprocessed run reached its best validation accuracy later than the original raw-data experiment, but the final achievable performance remained effectively unchanged. Since no explicit random seed was specified, differences in convergence epoch are expected and should not be interpreted as systematic evidence that preprocessing slows learning. Instead, the relevant conclusion is that preprocessing preserved the model's ability to solve the task.

As in the other configurations, the main benefit of preprocessing was computational efficiency. By using precomputed symbolic representations, the model avoided repeated parsing of the raw dataset files during training. This substantially reduced epoch time while preserving the predictive performance observed in the raw-data experiments.

Overall, the preprocessed left_right experiment confirms the conclusions drawn from the raw-data runs. The task is solved reliably by the reproduced SCL implementation, and preprocessing does not materially affect the model's reasoning performance. Its primary contribution is therefore improved training efficiency rather than increased accuracy.

