The joint training experiment completed successfully after the earlier compatibility and preprocessing issues were resolved. The final joint model achieved an overall test accuracy of approximately 82.5% after 300 epochs.

A particularly important aspect of the joint training results is that the experiment reports accuracy separately for each configuration within the shared model. The final test accuracies at epoch 300 were approximately:
| Configuration | Joint Training Accuracy |
|---|---:|
| center_single | 99.85% |
| distribute_four | 55.05% |
| distribute_nine | 53.65% |
| in_distri | 69.40% |
| in_out | 99.95% |
| left_right | 99.90% |
| up_down | 99.85% |

The results reinforce the same pattern that already emerged during the single-task experiments. Simpler relational configurations such as center_single, left_right, up_down, and in_out were reproduced almost perfectly even under the more difficult joint training setup. Their accuracies remained extremely close to 100%, indicating that the reconstructed implementation is fully capable of learning these types of symbolic relations even when multiple tasks are trained simultaneously.

The more complex distributed configurations, however, remained substantially more difficult. The joint model achieved only around 55% accuracy on distribute_four, around 54% on distribute_nine, and approximately 69% on in_distri. Although these results are somewhat better than several of the corresponding single-task experiments, they still remain significantly below the accuracies reported in the original SCL paper for Balanced-RAVEN joint training.

An important observation is that joint training did not collapse or destabilize learning. The model converged smoothly across all 300 epochs, and the training and test metrics remained stable throughout the later stages of optimization. The overall training accuracy stabilized around 84%, while the overall test accuracy remained around 82–83%, suggesting relatively good generalization for the jointly trained model as a whole. Unlike some of the single-task distributed experiments, the gap between train and test performance was comparatively modest in joint mode, indicating less severe overfitting behavior.

The final joint training results therefore provide additional evidence that the reconstructed implementation behaves consistently and reproducibly across all major I-RAVEN configurations. At the same time, they also strengthen the central conclusion of the replication effort: the adapted implementation successfully reproduces the original SCL behavior on simpler symbolic reasoning tasks, but persistent discrepancies remain for highly distributed multi-object relational configurations. These discrepancies are likely influenced by a combination of factors, including differences between I-RAVEN and Balanced-RAVEN, manual replacement of unavailable jactorch components, and the extensive compatibility modifications required to execute the repository in a modern Python and PyTorch environment.
