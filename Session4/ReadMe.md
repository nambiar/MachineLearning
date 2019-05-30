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

After the end of each layer our approach is to pass the feature which is expressed more or extracted by the kernels for doing that we employ maxpooling which would then pass it on to the next layer . Also by doing this max pooling reduces the burden of next layer as it has to now only work on the feature that has more value [this value is measured or computed from the training images provided]. In the given exercise after the first convolution we can immediately use maxpooling as image is concentrated at center pixels and so they talk more and this helps in reducing image size as well.

### Receptive Field

This holds the key to number of layers . the rule of thumb is that when are able to visualize the entire image (or reach an estimate of 70 - 90% of image i,e 400x400 reach's 11x11 size) we can stop adding further layers . Receptive field is based on number of 3x3 conv added as each layer see 3x3 space of image then next layer captures 5x5 part of image and so on. To increase receptive field we employ maxpooling as it doubles it . In the above excercise we can stop at 7x7 or 11x11 or even 14x14 depending upon architecture used.

### SoftMax

An activation for 1D array at the last to give the probability to the 10 class neurons which are fired. This allows the cross entropy loss function a better view of what output are fired at what rates and adjust weights accordingly . 

#### Model

A model is a layered CNN architecture which has convolution layer[containing convolution blocks] and transition layer [Max pooling Dropout ]

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

Keep checking both training and validation accuracy they go hand in hand or relatively same so no overfitting one is large over another then overfitting.

#### Dropout

All models are overfitting which means it perform well on training data and give not so well results on validation data. Then use dropout to remove some neurons in each layer (randomly) from firing such that it allows the model to learn to have further non linearity in its way to detect the feature which allows for great variation  . Also adding dropout reduces training time 

#### Learning Rate

The rate at which the weights /parameters of different layers change after back propagation. This is dependent on the batch size and epoch and if its overfitting or not . If everything work fine .Start with a 0.003 learning rate and if it reaches a max and then deviates then its not the perfect learning rate for the batch size , decrease it further . That's how to get required accuracy for that model on a particular batch size .

