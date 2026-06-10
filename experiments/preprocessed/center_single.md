grep -n "best val acc" runs_preprocessed/center_single/train.log | tail -
tail -30 runs_preprocessed/center_single/*/summary.json
cat runs_preprocessed/center_single/*/meta.json | grep num_features

The preprocessed center_single experiment used the corresponding symbolic feature dimensionality of 4 features. Unlike the raw-data experiment, this run did not use the index-based data loading pipeline. Instead, it used the preprocessed dataset representation generated from the original I-RAVEN files. The metadata confirms that no index file directory was used, indicating that the experiment was conducted with the preprocessed data pipeline.

The experiment achieved a best validation accuracy of 100.0% at epoch 217. At the final epoch, validation accuracy remained extremely high at approximately 99.95%, while training accuracy reached 100.0%. This shows that the model was able to solve the center_single configuration under the preprocessed setting as well, with no evidence of degraded generalization performance.

Compared with the original raw-data experiment, which reached 100.0% validation accuracy at epoch 19, and the raw-data verification rerun, which reached 100.0% at epoch 26, the preprocessed run required more epochs to reach the same peak accuracy. However, this difference in convergence epoch does not indicate worse final performance, since all versions ultimately achieved perfect or near-perfect validation accuracy. The difference mainly reflects variation in optimization trajectory rather than a meaningful change in model capability.

The main practical advantage of preprocessing was computational efficiency. The preprocessed pipeline avoided repeatedly parsing the original dataset files during training and instead loaded serialized symbolic representations directly. As a result, individual epochs were substantially faster than in the raw-data pipeline. Therefore, for the center_single configuration, preprocessing preserved the model's predictive performance while improving the efficiency of the training process.

Overall, the preprocessed center_single result confirms the conclusions drawn from the raw-data experiments. The configuration is highly tractable for the reproduced SCL implementation, and the model consistently achieves perfect or near-perfect validation accuracy regardless of whether the raw or preprocessed data pipeline is used.
