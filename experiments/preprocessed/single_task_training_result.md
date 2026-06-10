| Configuration | Raw verified (%) | Epoch | Preprocessed (%) | Epoch | # Features |
|---------------|-----------------:|------:|-----------------:|------:|----------:|
| center_single | 100.00 | 26  | 100.00 | 217 | 4  |
| distribute_four | 50.29 | 14  | 49.75 | 122 | 28 |
| distribute_nine | 47.64 | 7   | 47.77 | 70  | 63 |
| in_out | 100.00 | 104 | 100.00 | 90  | 8  |
| in_distri | 63.51 | 206 | 62.90 | 183 | 35 |
| left_right | 100.00 | 105 | 99.95 | 205 | 8  |
| up_down | 99.95 | 41  | 100.00 | 61  | 8  |


The results obtained with preprocessed symbolic representations closely match those obtained from the raw verified pipeline across all seven I-RAVEN configurations. The simpler configurations—center_single, left_right, up_down, and in_out—are solved almost perfectly under both settings, achieving approximately 100% validation accuracy. In contrast, the more challenging distribute_four and distribute_nine configurations remain near 50% accuracy regardless of preprocessing, indicating that the bottleneck lies in the reasoning problem itself rather than in data loading or representation generation. The in_distri configuration remains of intermediate difficulty, reaching approximately 63% validation accuracy in both cases.

Overall, preprocessing does not produce a meaningful change in predictive performance. The differences between raw and preprocessed runs are below one percentage point for all configurations and are consistent with normal run-to-run variation. The primary effect of preprocessing is therefore computational rather than statistical: it significantly reduces data preparation overhead and training time while preserving the original performance characteristics of the reproduced SCL model. The relative difficulty ranking of the I-RAVEN configurations remains unchanged, with directional and simpler structural tasks being solved reliably, the distributed configurations remaining challenging, and the in_distri configuration occupying an intermediate position.