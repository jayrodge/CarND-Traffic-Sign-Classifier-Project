# **Traffic Sign Recognition** 

## Writeup
---
**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./Images/graph.png "Visualization"
[image2]: ./Images/c.png "Random Image"
[image3]: ./Images/g.png "Grayscale"
[image4]: ./signs/1.png "Traffic Sign 1"
[image5]: ./signs/2.png "Traffic Sign 2"
[image6]: ./signs/3.png "Traffic Sign 3"
[image7]: ./signs/4.png "Traffic Sign 4"
[image8]: ./signs/5.png "Traffic Sign 5"
[image9]: ./signs/6.png "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/jayrodge/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12360
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data is scattered in training set.

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because results were better and it is sort of normalisation.

Here is an example of a traffic sign image before and after grayscaling.

![Before][image2]
![After][image3]

As a last step, I normalized the image data because the model will able to learn the features better as compared to Non Normalized image.

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 GrayScale image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|		28x28x6										|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x6 |
| RELU  | 10X10X6 |
| Max Pooling | 2x2 stride, outputs 5x5x16 |
| Convolution 5x5 | 1x1 stride, outputs 1x1x400 |
| RELU | 1x1x400 |
| Flatten | 400 |
| Fully Connected, RELU | Input: 400, Output: 200 |
| Dropout | 0.7 |
|Fully Connected, RELU | Input: 200, Output: 120 |
| Dropout | 0.7 |
|Fully Connected, RELU | Input: 120, Output: 84 |
| Dropout | 1.0 |
|Fully Connected | Input: 84, Output: 43 |

 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an Google Colab

Learning rate : 0.001
Batch size : 128
Epochs : 40
Optimizer : Adam

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 99.4
* validation set accuracy of 94.8
* test set accuracy of 92.9


I used the LeNet architecture as it was taught in LeNet Lab and worked well with MNIST data
Initially, the accuracy was not good, and also overfiting.
I added a convolution layer in the existing LeNet architecture from LeNet Lab, and also added Dropout after the fully connected layer which improved the accuracy of the model.
Then, I increased the epoch to 40, and reduced the learning rate from 0.0001 to 0.001 which made significant improvements in the model.signsest a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are six German traffic signs that I found on the web:
<p align="center">
  <img width="100" height="100" src='./signs/1.png'>
  <img width="100" height="100" src='./signs/2.png'>
  <img width="100" height="100" src='./signs/3.png'>
  <img width="100" height="100" src='./signs/4.png'>
  <img width="100" height="100" src='./signs/5.png'>
  <img width="100" height="100" src='./signs/6.png'>
 </p>
 
The first and the fourth image, when closely watched, it might be difficult to classify because beacuse of the unneccessary information like the watermark in the images. Also, It might be difficult for this model to correctly classify the images with because of poor lighting conditions, fog and some objects like birds overlapping the traffic signs

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (30km/h)     		| 1 'Speed limit (30km/h)'  | 
| Go straight or right    			| 36 'Go straight or right'	|
| No entry				| 17 'No entry'										|
| Yield      		| 13 'Yield'					 				|
| Right-of-way at the next intersection			| 11 'Right-of-way at the next intersection'     							|
| Turn left ahead | 34 'Turn left ahead' |


The model was able to correctly guess 6 of the 6 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 92.9%

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

For the first image, the model is relatively sure that this is a speed limit 30km/h sign (probability of 0.96), and The top five soft max probabilities were

| Prediction        	|     Probability 	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (30km/h) |   0.96446 |
| Speed limit (60km/h) |   0.03542 |
| Dangerous curve to the left |   0.00007 |
| Speed limit (50km/h) |   0.00005 |
| End of all speed and passing limits |   0.00000 |




For the second image, the model correctly predicts, its a Go straight or right sign

| Prediction        	|     Probability 	        					| 
|:---------------------:|:---------------------------------------------:| 
| Go straight or right |   1.00000 |
| Speed limit (30km/h) |   0.00000 |
| Speed limit (20km/h) |   0.00000 |
| Speed limit (70km/h) |   0.00000 |
| Bicycles crossing |   0.00000 |

For the third image, the model correctly predicts, its a No Entry sign

| Prediction        	|     Probability 	        					| 
|:---------------------:|:---------------------------------------------:| 
| No entry |   1.00000 |
| Priority road |   0.00000 |
| No vehicles |   0.00000 |
| End of all speed and passing limits |   0.00000 |
| Turn left ahead |   0.00000 |


For the fourth image , the model correctly predicts, its a Yield 

| Prediction        	|     Probability 	        					| 
|:---------------------:|:---------------------------------------------:| 
| Yield |   1.00000 |
| No vehicles |   0.00000 |
| Keep right |   0.00000 |
| Ahead only |   0.00000 |
| Speed limit (70km/h) |   0.00000 |


For the fifth image, the model correctly predicts, its a Right-of-way at the next intersection

| Prediction        	|     Probability 	        					| 
|:---------------------:|:---------------------------------------------:| 
| Right-of-way at the next intersection |   1.00000 |
| Beware of ice/snow |   0.00000 |
| Double curve |   0.00000 |
| Roundabout mandatory |   0.00000 |
| Pedestrians |   0.00000 |


For the sixth image, the model correctly predicts, its a Turn left ahead

| Prediction        	|     Probability 	        					| 
|:---------------------:|:---------------------------------------------:| 
| Turn left ahead |   0.87606 |
| End of speed limit (80km/h) |   0.12230 |
| End of all speed and passing limits |   0.00132 |
| Beware of ice/snow |   0.00026 |
| Keep right |   0.00004 |
