# TennisShotDetection

## About
* A key term numerous professional tennis players use on the ATP and WTA circuits is **shot-selection**. Choosing what type of shot to hit in different situations is an important part of winning matches.

## Goal: Create a model that can analyze shots hit and be used in matches to analyze shot-selection patterns made by professionals

# Creation

## Dataset
With no current large data sets with pictures of professional tennis player shots, I created a complete data set that can be found as `shots.zip`. This dataset has 300 images of serves, forehands, and backhands that have been split into train and test folders

# Code
## Custom Neural Net Training
### Downloading Dataset
By utilizing code that links to the raw download link for the data, the data can be downloaded by anyone who has access to the notebook
### Processing Images
Through utilizing simple transforms the images are changed to tensors that are ready to be fed into a model
### Splitting data and creating data loaders
The next step involves using Torchvision's dataset package to split data into test and train data. torch.utils.data gives us the power of using the DataLoader package which we can use to create an iterable loader to be used in training
### Setting up the model
The model I used replicated the TinyVGG model's structure with two convolutional layers followed by a classifier layer with each convolutional layer being made of 2 Conv2d, 2 ReLU, and 1 MaxPooling layer. The model used would take in an input of 3 for a tensor of each color layer and output a final string that would be based on the argmax of the probabilities that were given from the model (the list was in the format ['backhand','forehand','serve']. The commented print statements were used to find the correct shapes of tensors in intermediate steps (input for the second conv_block) to ensure the model would work properly
### Functions for training and testing
To make the testing and training process smoother, the training and testing were split into functions `train_step(),test_step()` which were then combined into one large test function `test()`. The train function utilized the basic training process with forward and backpropagation along with an optimizer that would be stepped based on inputs of the model. 
### Training
For training I used
* Loss Function: CrossEntropyLoss - torch.nn recommends this loss function for multiple detection models
* Optimizer: Adam - torch.nn recommends this or softmax optimizers

## Transfer Learning
For the Transfer learning method, the initial steps along with the training were the same as the **Custom Neural Net Training** process
Utilized the aid of mrdbourke for visualization 'https://github.com/mrdbourke/pytorch-deep-learning/'
### Model used
For the training, the model that was used was the Efficient_Net_B1 model. Overall ended with around an 80 percent accuracy but still leaves a lot to be desired
<img width="911" alt="image" src="https://github.com/ShrishChou/TennisShotDetection/assets/91390142/5b531232-7451-48ff-ae7e-cababbedfad1">
### Possible changes for the future
* creating a more comprehensive data set
  * would need more data from pros
* test with different models
