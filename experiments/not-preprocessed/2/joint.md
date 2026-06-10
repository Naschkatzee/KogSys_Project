Failed.

When the same raw pipeline (as for single-task) was applied to joint training across all seven configurations, the run failed due to incompatible symbolic feature dimensions. The model was initialized with a unified feature dimensionality of 63 features per panel, but individual raw samples from smaller configurations did not contain tensors of that size. Therefore, the symbolic model could not reshape the input into the expected joint format. This confirmed that joint training requires a normalized or padded symbolic representation, which was provided by the preprocessed pipeline.

