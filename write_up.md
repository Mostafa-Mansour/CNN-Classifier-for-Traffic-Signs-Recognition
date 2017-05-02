# Traffic Sign Recognition 

## The goal of this project is to build a Convolution Neural Network (CNN) for a self-driving car to recognize traffic signs. In this project the [German Traffic Signs Dateset](http://benchmark.ini.rub.de/) is used. The Network is trained using a CPU.
---

## The following steps have been followed to build this project:

### 1. Load the data and prepare train, validation and test sets.
### 2. Get a statistical summary for the different sets and visulaize some data.
### 3. Design a model architecture for the CNN.
### 4. Train the model using the train data set and validate it using the validation data set.
### 5. Test the final model architecture using the test set.
### 6. Test the final model on new images.
---

[//]: # (Image References)

[image1]: ./examples/image.png "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./new_images/1.png	  
[image4]: ./new_images/2.png
[image5]: ./new_images/3.png
[image6]: ./new_images/4.png
[image7]: ./new_images/5.png
[image8]: ./new_images/6.png
[image9]: ./new_images/22.png

### 1. Load the data and prepare train, validation and test sets.
* The data set can be downloaded from [here](https://d17h27t6h515a5.cloudfront.net/topher/2017/February/5898cd6f_traffic-signs-data/traffic-signs-data.zip). After unziping the .zip file, we will get three ".p" files, three data sets, for training, validation and testing.
* Then, the data is loaded using pickle module in python.
* At this point we got three data sets of RGB traffic signs. All of these 32x 32 RGB images will be converted to gray scale using opencv.

![alt text][image2]

* Finally, we will make a normalization (whitening) to these sets using numpay library. 
Now we have three sets containing normalized gray-scale images for traffic signs. 

---
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

---
### 3. Design a model architecture for the CNN.

#### The final model consists of the following layers:

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

---
### 4. Train the model using the train data set and validate it using the validation data set.
* The model is trained using the following hyperparameters:
	*learning rate=0.001 - EPOCHS=20 - BATCH_SIZE=128
* For this model, Cross Entropy loss function was chosen to be reduced using Adam optimizer.
* The validation accuracy is about 97%.
*  This accuracy was not obtained from the first time. It was about 94%. Using one more convolutional layer and making some adjustments on the images such as equalizing histograms, converting to gray scale and "whitening" - normalizing - each batch using its mean and standard deviation and also using dropout regularization technique with peak=0.75, increased the validation accuracy to 97%.
* The model was saved to be used later for testing and prediction.

---
### 5. Test the final model architecture using the test set.
After tuning the hyperparameters and getting the final model, the final model was tested on the test data set. The test accuracy was 94.4%.

---
### 6.Test the final model on new images.
The model was tested on new images. The following six images were fed to the model to be predicited using softmax function.
* The images were resized and converted to gray scale to fit the input of the netwrok (32x32).
* Then, Equalizing the histogram was applied to  the images
* The top five predictions were calculated and the softmax predictions were plotted.

![alt text][image3]	![alt text][image4]	![alt text][image5]	![alt text][image6]	![alt text][image7]	![alt text][image8]

The model was able to predict correctly the first five images but was not able to predict the last image with test accuracy=83.3%.

![alt text][image9]

I think this low accuracy is because of the low quality of the image. So, more image preprocessing methods should be applied. Also, making this model more deeper by adding more convolutional layers may solve this problem.

For the code, please check [here](Traffic_Sign_Classifier-.ipynb).
