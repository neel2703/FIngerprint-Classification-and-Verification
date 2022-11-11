## Results

![results](https://user-images.githubusercontent.com/82512279/201339572-4c2dcc58-61df-4397-ade8-8bc09d2a4f1b.png)

## Comments
- The selected models perform much better than the Baseline models because of a
better and more complex CNN architecture. Preprocessing the images and training the
models on Orientation Maps also improved the accuracy and computation speed.
- A common drawback for all of the selected models is that they overfit. This is
likely due to the models being trained on a dataset smaller than the ones used in research
due to system constraints.
- FCTP-Net is our best model in terms of performance as it gives the highest accuracy and
shows less overfitting compared to other architectures.
- We could try to improve the accuracy by implementing custom optimizers more suited to
our problem.
- The performance in the research papers was comparatively higher because those models
were trained for a high number of epochs(100,000).

## Hyperparameters
- The optimizer used in all the models was Adam with a learning_rate=0.0001. A small
learning rate helped us achieve 82% accuracy on the FCTP-Net model.
- Local Response Normalization(LRN) was used in the FCTP-Net model after every
MaxPooling layer. LRN implements lateral inhibition in our model. ReLU neurons have
unbounded activations and we need LRN to normalize that. We want to detect
high-frequency features with a large response. If we normalize around the local
neighborhood of the excited neuron, it becomes even more sensitive as compared to its
neighbors.
- At the same time, LRN will dampen the responses that are uniformly large in any given
local neighborhood. Basically, we want to encourage some kind of inhibition and boost
the neurons with relatively larger activations.
- The LRN gave a better result compared to BatchNormalization in the FCTP-Net
architecture.
- The ‘Sparse Categorical Entropy’ loss function was used because we label encoded the
classes.

## Conclusion
- Convolutional Architectures give us the best results for fingerprint classification
problems. FCTP-Net gave us the best result for our classification problem with an
accuracy of 82%.
- We need to classify fingerprints to increase the speed of the Fingerprint Matching process
and thereby improve our penetration rate.
- Hyperparameter tuning was performed and the best hyperparameters were used for our
models to achieve optimal results.
