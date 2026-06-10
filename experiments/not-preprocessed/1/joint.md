grep -n "best val acc" runs/joint/*/log.log | tail -1
tail -30 runs/joint/*/summary.json
cat runs/joint/*/meta.json | grep num_features

The joint experiment trained a single SCL model on all seven I-RAVEN configurations simultaneously: Center Single, Distribute Four, Distribute Nine, Left-Right, Up-Down, In-Out, and In-Distribute. To accommodate the heterogeneous feature representations, all symbolic inputs were padded to the maximum dimensionality observed across configurations, resulting in a common input size of 63 features. The remaining architecture and optimization settings were unchanged from the individual experiments (five experts, hidden dimensions 32 and 16, reduction group size 2, batch size 128, learning rate 0.005, weight decay 0.01, 300 training epochs). The best validation accuracy of 82.73% was achieved at epoch 194.

Although overall performance remained substantially below the near-perfect accuracies observed for the simpler spatial configurations, the joint model successfully learned all tasks within a single parameterization. At the end of training (epoch 300), the aggregate validation accuracy was 82.51%, while training accuracy reached 84.31%, indicating only a modest train-validation gap and limited overfitting.

Per-configuration validation accuracies reveal a clear separation between easy and difficult problem families. The model retained almost perfect performance on Center Single (99.85%), Left-Right (99.90%), Up-Down (99.85%), and In-Out (99.95%). More complex configurations remained substantially harder, with accuracies of 55.05% for Distribute Four, 53.65% for Distribute Nine, and 69.40% for In-Distribute.

Interestingly, joint training improved performance on the difficult configurations relative to the corresponding single-task experiments. Distribute Four increased from approximately 49% to 55%, Distribute Nine from approximately 48% to 54%, and In-Distribute from approximately 62% to 69%. In contrast, the already-solved configurations experienced only negligible reductions, remaining close to perfect accuracy. These results suggest that sharing representations across multiple RPM structures provides beneficial inductive transfer for the more challenging tasks while preserving performance on simpler ones.

The joint experiment therefore demonstrates that SCL can learn a unified symbolic representation across heterogeneous RPM configurations. While performance on the most difficult distributive structures remains substantially below that of the easier tasks, multi-task learning appears to mitigate some of the difficulties encountered in isolated training, indicating that common relational patterns can be exploited across configuration types.


### Joint Training Results

| Metric | Value |
|---------|---------|
| Number of features | 63 |
| Best validation accuracy | 82.73% |
| Best epoch | 194 |
| Final validation accuracy (epoch 300) | 82.51% |

### Per-Configuration Validation Accuracy

| Configuration | Accuracy (%) |
|---------------|-------------:|
| Center Single | 99.85 |
| Left-Right | 99.90 |
| Up-Down | 99.85 |
| In-Out | 99.95 |
| In-Distribute | 69.40 |
| Distribute Four | 55.05 |
| Distribute Nine | 53.65 |