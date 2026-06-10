grep -n "best val acc" runs_preprocessed/up_down/train.log | tail -
tail -30 runs_preprocessed/up_down/*/summary.json
cat runs_preprocessed/up_down/*/meta.json | grep num_features

The preprocessed up_down experiment used the corresponding symbolic feature dimensionality of 8 features. As in the other preprocessed experiments, the metadata confirms that no index file directory was used, indicating that the model operated on serialized symbolic representations generated from the original I-RAVEN files rather than on the raw index-based loading pipeline.

The experiment achieved a best validation accuracy of 100.0% at epoch 61. At the final epoch, validation accuracy remained almost identical at approximately 99.95%, while training accuracy was approximately 99.90%. This shows that the model solved the up_down configuration under the preprocessed setting and maintained near-perfect performance throughout the later training stages.

Compared with the original raw-data experiment, which achieved 99.95% validation accuracy at epoch 15, and the raw-data verification rerun, which also achieved 99.95% at epoch 41, the preprocessed run produced an essentially identical result. The slight numerical difference between 99.95% and 100.0% is negligible and does not indicate a meaningful change in model behavior. All versions show that the up_down configuration is reliably solved by the reproduced SCL implementation.

The preprocessed run reached its best validation accuracy at epoch 61, which is later than the original raw-data run but close to the same general convergence range as the verification rerun. Since no explicit random seed was specified, such differences in convergence epoch are expected across independent runs. The important result is that all pipelines converged to near-perfect accuracy.

The main benefit of preprocessing was computational efficiency. By loading precomputed symbolic representations directly, the model avoided repeated parsing of the original dataset files and substantially reduced epoch duration. However, as in the other experiments, this efficiency improvement did not lead to a meaningful improvement in predictive performance.

Overall, the preprocessed up_down experiment confirms the conclusions drawn from the raw-data experiments. The configuration is highly tractable for the reproduced SCL architecture, and preprocessing preserves the model's ability to solve the task while making the training process considerably faster.
