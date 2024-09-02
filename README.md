Kianosh Arian 810198345, Project Number Five, Phase 2

Project Objective:
The goal of this project is to build a neural network to classify images into four categories of animals and to analyze the impact of different parameters on this neural network.

Overview:
In this project, we first read a dataset containing various animals and store it in a TensorFlow dataset. Then, we convert these images to grayscale and one-hot encode the labels. After that, we create a neural network and train it on the data. We will experiment with different parameters such as optimizer, epoch, regularization, and loss function to optimize our network. Finally, we evaluate this network on test data. The data loaded in this project are divided into train and test sets, each organized into folders based on their category. We use a predefined Keras function to read these categorized folders.

Phase 1 - Preprocessing:
We read the data using Keras' categorical image reading function, then convert them to grayscale and one-hot encode them. The reason for one-hot encoding is that our data is categorical, and different categories are unrelated to each other. If we convert them to regular numbers, it would imply a relationship between the numbers and hence between the categories. Since they are unrelated, we use one-hot encoding to allow the use of the CategoricalCrossentropy loss function.

Phase 2 - Designing the Neural Network:
In this section, we build a neural network based on the given criteria, consisting of dense and flatten layers. The number of parameters in this network:

Layer (type)
Output Shape
Param #

Rescaling (Rescaling)
(None, 256, 256, 1)
0

Resizing (Resizing)
(None, 50, 50, 1)
0

Flatten (Flatten)
(None, 2500)
0

Dense (Dense)
(None, 200)
500200

Dense_1 (Dense)
(None, 4)
804

Since our images are 50x50, the output of the flatten layer is 2500, and the next dense layer has 200 nodes. Therefore, we have 200*2500=500000 parameters, plus 200 for the bias, making a total of 500200 parameters.

Phase 3 - Data Classification:

Part 1:
Momentum is one of the optimizer parameters that works by ignoring small errors when the model is progressing in one direction and continues to advance in that direction. When we use momentum, the model captures less noise from the data, potentially improving the model. With a momentum of 0.5, the model's predictions improve and get better, but with a momentum of 0.9, the predictions get worse, weakening the model. No, if the momentum is too high, it will ignore too many incorrect data points and worsen the model instead of improving it. When using Adam, the result is better than regular SGD and almost equal to the result obtained with SGD and momentum=0.5.

Part 2:
Using 20 epochs improves our results. This is because algorithms like SGD gradually approach the correct solution, and it may not reach the correct answer in one pass through the data. Therefore, we use multiple epochs to allow SGD to get sufficiently close to the final answer. It is not always necessary to use multiple epochs; if we reach the desired coefficients and accuracy in the first pass, we can stop there to avoid overfitting. When training the model for 90 epochs and then testing it on the test data, we see that overfitting has occurred, and the performance on the test is weaker than on the train. No, using too many epochs is not desirable due to overfitting. To prevent this, we can use early stopping mechanisms, which will stop the model once it reaches a specified point, even if all epochs are not completed.

Part 3:
The MSE function gives us much weaker results for several reasons. The MSE function is not suitable for classification. One reason is that when using this function, our input dataset should have a normal distribution, whereas in categorical problems, the data is divided into several categories and is not normally distributed. Also, this function is suitable for predicting numerical values in regression problems. In classification problems, our output is a softmax function that gives values between 0 and 1, while MSE expects values between negative and positive infinity and does not provide a good minimum point. MSE is appropriate for regression problems with normally distributed data.

Part 4:
L2 regularization adds a coefficient of weights to the loss function to prevent the model from creating large weights and relying on only one parameter. Dropout randomly removes some nodes during each training iteration to prevent overfitting. Applying L2 regularization improves our F1 score, while applying dropout weakens the model's performance.

The errors could be due to the camera being too close to the subjects in the photos or the presence of multiple animals in one image.