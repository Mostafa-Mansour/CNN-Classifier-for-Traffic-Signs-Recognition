# Traffic Sign Recognition 

## The goal of this project is to build a Convolution Neural Network (CNN) for a self-driving car to recognize traffic signs. In this project the [German Traffic Signs Dateset](http://benchmark.ini.rub.de/) is used. The Network is trained using a CPU.
---

## The following steps have been followed to build this project:

### 1. Load the data and prepare train, validation and test sets.
### 2. Get a statistical summary for the different sets and visulaize some data.
### 3. Design a model architecture for the CNN.
### 4. Train the model using the train data set and validate it using the validation data set.
### 5. Test the final model architecture using the test set.
### 6.
---

[//]: # (Image References)

[image1]: ./examples/image.png "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/placeholder.png "Traffic Sign 1"
[image5]: ./examples/placeholder.png "Traffic Sign 2"
[image6]: ./examples/placeholder.png "Traffic Sign 3"
[image7]: ./examples/placeholder.png "Traffic Sign 4"
[image8]: ./examples/placeholder.png "Traffic Sign 5"

### 1. Load the data and prepare train, validation and test sets.
* The data set can be downloaded from [here](https://d17h27t6h515a5.cloudfront.net/topher/2017/February/5898cd6f_traffic-signs-data/traffic-signs-data.zip). After unziping the .zip file, we will get three ".p" files, three data sets, for training, validation and testing.
* Then, the data is loaded using pickle module in python.
* At this point we got three data sets of RGB traffic signs. All of these 32x 32 RGB images will be converted to gray scale using opencv.

![alt text][image2]

* Finally, we will make a normalization (whitening) to these sets using numpay library. 
Now we have three sets containing normalized gray-scale images for traffic signs. 

### 2. Get a statistical summary for the different sets and visulaize some data.
In the sets we have, we can find that:
* Number of training examples = 34799
* Number of validation examples = 4410
* Number of test examples = 34799
* Image shape is (32,32,1)
* Number of classes = 43
We can visualize some signs arbitrary and checking if they matche their true name in the data base. For example, visualizing a feature with index number 25 will give us the following image.

![alt text][image1] 

By checking index number 25 in the data base, we will find that it has a label of "Road Working" which matches the image.

### 3. Design a model architecture for the CNN.

#### My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Gray scale image 						| 
| Convolution 5x5     	| 1x1 stride, VALID padding, outputs 28x28x6 	|
| RELU                  |                                               |
| Convolution 5x5		| 1x1 stride, VALID padding, outputs 24x24x6	|
| RELU					|												|
| Convolution 5x5		| 1x1 stride, VALID padding, outputs 20x20x16	|
| RELU					| 												|
| Max pooling	      	| 2x2 stride,  outputs 10x10x16 				|
| Fully Connected	    | input=10x10x16	output=120					|
| RELU					|												|
| Fully connected		| input=120			output=84					|
| RELU					|												|
| Dropout				| peak= 0.75									|
| Fully connected 		| input=84			output=43					|
| Softmax				| Softmax cross entropy using one_hot_encoding	|
|						|												|
|						|												|

