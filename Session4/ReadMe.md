# Architectural Basics

The basics required for any CNN model to be designed and evaluated

## Images through Channels

The basic build block is the input image which contains any number of channel depending on how it is captured. Gray scale or RGB.

***The present challenge is to detect a  hand written image of the number***

First things first :

We need to extract features that is edges to gradients to patterns to part of the object and so on. 

### How many layers

Its totally dependent on the problem at hand and size of feature to image ratio. If the input has a specific location or area in image then that area has to be captured by the layers . For example each layer captures 3x3 part of image then number of layers if required feature to be captured is 7x7 then 3 layers are required. In the given execrcise most of the hand writtend images has information between 5x5 and 25x25 

### 3x3 Convolutions

The CNN is based on convolution and 3x3 forms basis of that as it scans through the 9 pixels and computes a single value feature extractor from it. The other component of it is how many strides one can take while doing it . If information is sparsely distributes stride more than 1 can be done .

### 1x1 Convolutions

As we compute the kernels in each layer the channels of the given layer will be increased just as in our exercise when we reach layer 3 with a 64 channels , this amount of expressivity is not required and has impact on performance of the model . In such cases 1x1 can be used to decrease the channels i.e (24x24x64)** (1x1x64)x10 as 10 classes are to be matched with.

### MaxPooling

After the end of each layer our approach is to pass the feature which is expressed more or extracted by the kernels for doing that we employ maxpooling which would then pass it on to the next layer . Also by doing this max pooling reduces the burden of next layer as it has to now only work on the feature that has more value [this value is measured or computed from the training images provided]. In the given exercise after the first convolution we can immediately use maxpooling as image is concentrated at center pixels and so they talk more and this helps in reducing image size as well. Should not be used before the prediction layer as that would cripple the work done by lower layers as at that instance having maxpool will remove a part of image (as at that point receptive field equals the object size)that contains the information which is not the intention of using it.

### Receptive Field

This holds the key to number of layers . the rule of thumb is that when are able to visualize the entire image (or reach an estimate of 70 - 90% of image i,e 400x400 reach's 11x11 size) we can stop adding further layers . Receptive field is based on number of 3x3 conv added as each layer see 3x3 space of image then next layer captures 5x5 part of image and so on. To increase receptive field we employ maxpooling as it doubles it . In the above exercise we can stop at 7x7 or 11x11 or even 14x14 depending upon architecture used.

### Kernels & Number of Kernels

3x3 is a kernel or feature extractor and The number of such kernels depends on the Image and number of classes that needs to be classified. In any given scenario we follow the approach of gradually increasing the number of kernels as we go deeper into the network and then when there is sufficient expressability we reduce the channels and do the same thing again in the next layer.

### SoftMax

An activation for 1D array at the last to give the probability to the 10 class neurons which are fired. This allows the cross entropy loss function a better view of what output are fired at what rates and adjust weights accordingly . 

#### Model: Conv & Transition 

A model is a layered CNN architecture which has convolution layer[containing convolution blocks] and transition layer [Max pooling  and channel down sampling using 1x1]. Each layer starts with convolution layer and then transition layer.



### Learning Rate, Batch size, Epoch , Training Accuracy 

To train your network you take the test samples and divide it in batch with random initialization of test images with random distribution across feature sets to be captured.

Epoch is one time running of all the batches from the test set of images.

When you are training the model the following observations are to be made 

#### Training Accuracy : 

As you train your training accuracy keeps on increasing and kind of stagnates with epoch.

If training accuracy is low , wrong architecture change it .

Training time is high , batch size is an issue optimize it 

Train for more epoch if model needs has less parameters to reach required accuracy .

#### Validation Accuracy : 

How models works on validation image sets 

Keep checking both training and validation accuracy they go hand in hand or relatively same so no overfitting, one is larger than another then overfitting.

#### Learning Rate

The rate at which the weights /parameters of different layers change after back propagation. This is dependent on the batch size and epoch and if its overfitting or not . If everything work fine .Start with a 0.003 learning rate and if it reaches a max and then deviates then its not the perfect learning rate for the batch size , decrease it further . That's how to get required accuracy for that model on a particular batch size .

#### Batch Normalization

When the model has been optimized using the conv & transition layer approach we see that the accuracy remains the same and does not increase . The main catch here or in the above exercise as well was that each layer during back propagation sees a larger shift in the amplitudes between the kernel values and these results in increase in loss function and thus for that number of epoch would not give us a greater accuracy . But we can increase epoch's and still increase accuracy but that also does not give a very large boost to accuracy . Batch normalization applied after each conv layer makes sure that amplitudes are scaled properly and does not result in a trend called gradient explosion by subtracting mean and add trainable parameters which can be tuned according to loss function. This results in increase accuracy . Also seen during Program 4 of class it decreases the training time . In the last layer usage of dropout shall provide unnecessary variance because in prediction layer the previous layers have enough mean and variance for back propagation to improve the accuracy.

#### Number of Epochs and when to increase them

As validation accuracy can be known from out model.fit function in tensor flow. We see that when we give an arbitrary value 20 for number of epoch the accuracy keeps increasing reaches a local max and then decreases . At that point you should fix the epochs, otherwise training further would only imply overfitting as seen with training accuracy increasing and validation accuracy decreasing.

#### Dropout

All models are overfitting which means it perform well on training data and give not so well results on validation data. Then use dropout to remove some neurons in each layer (randomly) from firing such that it allows the model to learn to have further non linearity in its way to detect the feature which allows for great variation .  Also adding dropout reduces training time 

#### LRS

Whenever we give a test data the random weights, parameters  are initialized and calculated across the kernels bias etc . Once we get the output and calculate the error of training set and then back prop adjusts the initialized parameters so that they tend towards test output. The rate at which these parameters are corrected/estimated depends upon learning rate . Small learning rate more time , large learning rate results in good training and low validation accuracy. 

#### Stochastic Gradient Descent

As understanding goes from the class Stochastic gradient descent estimates the error in the training data and then updates weight by using back prop. We did not use it in our exercise. It actually calculates the gradient descent of the entire set of parameters which might leads to non convergence of paramters for max accuracy. This was the reason to use the Adaptive Gradient Descent algo's. 

An extended version of this which is adaptive Stochastic Gradient descent which lets us adapt every parameter for every epoch and gives a callback (I think its a feature of keras to mention a learning rate after each epoch) 



