grep -n "best val acc" runs_preprocessed/in_out/train.log | tail -
tail -30 runs_preprocessed/in_out/*/summary.json
cat runs_preprocessed/in_out/*/meta.json | grep num_features

The preprocessed in_out experiment used the corresponding symbolic feature dimensionality of 8 features. As in the other preprocessed experiments, the metadata confirms that no index file directory was used, indicating that the model operated on the serialized symbolic representations generated from the original I-RAVEN files rather than on the raw index-based loading pipeline.

The experiment achieved a best validation accuracy of 100.0% at epoch 90. At the final epoch, validation accuracy remained high at approximately 99.31%, while training accuracy was approximately 97.91%. Although the final epoch was slightly below the best checkpoint, the model clearly solved the task and maintained near-perfect generalization throughout most of the later training process.

Compared with the original raw-data experiment, which achieved 100.0% validation accuracy at epoch 104, and the raw-data verification rerun, which achieved 100.0% at epoch 124, the preprocessed result is fully consistent. All three runs reached perfect validation accuracy, demonstrating that the in_out configuration is reliably solved by the reproduced SCL implementation regardless of whether the raw or preprocessed pipeline is used.

The preprocessed run reached its best validation accuracy slightly earlier than the raw-data runs, but this difference should not be interpreted as a major methodological effect. Since no explicit random seed was specified, differences in convergence epoch are expected across independent runs. The important point is that all versions converged to the same peak performance level.

The main practical effect of preprocessing was improved computational efficiency. By loading precomputed symbolic representations directly, the preprocessed pipeline avoided repeated parsing of the original dataset files and therefore substantially reduced epoch duration. However, as with the other configurations, this efficiency improvement did not correspond to a meaningful change in predictive performance.

Overall, the preprocessed in_out experiment confirms the conclusions drawn from the raw-data experiments. The in_out configuration is highly tractable for the reproduced SCL architecture, and preprocessing preserves the model's ability to solve the task while making training considerably faster.
