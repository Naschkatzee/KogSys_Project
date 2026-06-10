grep -n "best val acc" runs_preprocessed/in_distri/train.log | tail -
tail -30 runs_preprocessed/in_distri/*/summary.json
cat runs_preprocessed/in_distri/*/meta.json | grep num_features

The preprocessed in_distri experiment used the corresponding symbolic feature dimensionality of 35 features. As in the other preprocessed experiments, the metadata confirms that no index file directory was used, indicating that the experiment operated on serialized symbolic representations generated from the original I-RAVEN files rather than on the raw index-based loading pipeline.

The experiment achieved a best validation accuracy of 62.90% at epoch 183. At the final epoch, validation accuracy remained close to this value at approximately 61.90%, while training accuracy reached approximately 79.71%. This indicates that the model continued to learn useful task structure over a relatively long training period and that the best validation performance occurred in the later stages of training.

Compared with the original raw-data experiment, which achieved 62.00% validation accuracy at epoch 270, and the raw-data verification rerun, which achieved 63.51% at epoch 206, the preprocessed result falls within the same performance range. The differences between the raw and preprocessed runs are small, amounting to roughly one to one and a half percentage points. Therefore, preprocessing did not produce a substantial change in predictive performance for the in_distri configuration.

The training dynamics of the preprocessed run were broadly similar to those observed in the raw-data experiments. In all cases, validation accuracy improved gradually over many epochs, unlike the simpler configurations where near-perfect performance was reached relatively quickly. This indicates that in_distri remains a more difficult task for the reproduced SCL architecture, although it is solved more successfully than distribute_four and distribute_nine.

The main benefit of preprocessing was again computational rather than predictive. By using serialized symbolic representations, the preprocessed pipeline substantially reduced data-loading overhead and shortened individual epoch times. However, the resulting accuracy remained essentially comparable to the raw-data experiments, showing that the preprocessing procedure did not materially alter the model's reasoning ability.

Overall, the preprocessed in_distri experiment confirms the pattern observed across the other configurations. Preprocessing preserves the model's performance while improving execution efficiency. The in_distri task remains moderately challenging, with validation accuracy around 63%, placing it between the near-perfect configurations and the substantially more difficult distributed configurations.
