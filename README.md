# Fashion-MNIST

Project using the Fashion MNIST dataset to classify multiple image classes using the TinyVGG CNN architecture (https://poloclub.github.io/cnn-explainer/) built in TensorFlow 2.X.

## This project uses:
* TensorFlow 2.X to create, train and evaluate the performance of a multi-class image classification dataset
* Sequential API to build a version of TinyVGG (3 Convolutional layers, 2 MaxPool layers, 1 Fully-Connected Dense layer with softmax activation)
* Learning rate scheduling to empirically find the ideal range for the model learning rate

Fashion MNIST dataset contains images of 10 classes of clothing, with 60k training samples and 10k test samples (85.7:14.3). The images are of resolution 28x28 pixels. The model validates using the test data during the training of the model.

The labels used in the dataset are not one-hot encoded [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] and so in training, `sparse_categorical_crossentropy` is used in the loss function.

![image](https://github.com/DavAll22/Fashion-MNIST/assets/124359152/7350b43c-678f-4ab1-811b-ee9df9908ef7)


## Evaluation
* The model was initially trained for 50 epochs using learning rate scheduling from 1e-4. The loss was plotted against the log learning rate and a learning rate of around 1e-3 was found to be the most optimal.

![image](https://github.com/DavAll22/Fashion-MNIST/assets/124359152/5151eaf6-0e47-4e9b-813a-d10d29b653e9)

* After training past epoch 25, the model overfits and accuracy and loss worsen, so training was limited to 25 epochs

* On the test data, the model achieves a loss of 0.372 and an accuracy of 90.02%.
  * Compared to the training loss, the validation loss starts to diverge indicating the data is overfitting (model won't be able to generalise well to new data)
  * Further methods should be used to reduce this, like data augmentation, different model network layout, hyperparameter tuning etc.)
  
![image](https://github.com/DavAll22/Fashion-MNIST/assets/124359152/30ffb726-61dd-466c-937c-cea240a0903f)


## Predictions

* Prediction probabilities for each class is generated from the test data and the corresponding class label is assigned to the maximum prediction from the model
* A confusion matrix is plotted from the predictions
  * The model gets confused over classes which have similar features, like *Shirt* and *T-Shirt/Top*

The per-class F1-Score is evaluated and shown that class *Shirt* is the worst performing from the 10 classes. More data could be obtained for this class to improve the score.
![image](https://github.com/DavAll22/Fashion-MNIST/assets/124359152/0494a843-446d-48de-9f44-5b2998df7b89)
