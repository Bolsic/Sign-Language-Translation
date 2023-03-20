# Sign-Language-Translation
 Comparison of different models for automatic sign language translation

 The project was done as a part of the PFE summer camp in 2022. From start to finish, the project took 14 days.

 The task was to compare different network models for translating sign language:

 1. Extended archetecture for the MNIST dataset - Extended MNIST CNN
 2. Keypoint Classification
 3. kNN model
 4. EfficientNetB3

 ## Database

Dataset used is the Synthetic ASL Alphabet dataset wich consists of 27000 color images of ASL alphabet letters in the 512x512 resolution. Theese images are syntheticly generated wich gives them more diversyty in skin color and backround. 

https://www.kaggle.com/datasets/lexset/synthetic-asl-alphabet


## Preprocessing

Every image is altered in a few ways with random paramaters to increase their diversity.

### Hand detection

Hand detection was realised using Media Pipe Holistic Pipeline witch detects 21 keypoints on the hand and returns their x, y and z coordinate, z being the estimated depth. 

### Image Binrisation

For the kNN model every image is binarised based on the skin color detected. Then the image is split into nxn cells and then a number between 0 and 1 coresponding to the percentage of black space in the cell is assigned to every cell. This matrix of numbers will be used as the input for the kNN model. 

## Extended MNIST CNN

This method is based of a CNN model for clasification of images in the MNIST ASL dataset, wich contains grayscale images in 28x28 resolution.

https://github.com/bnsreenu/python_for_microscopists/blob/master/212-sign_language.py

The archetecture is expanded with more convolution layers and more maxpooling layers. 

## kNN model

This model works under the asumption that the data given will form clusters. The model was tested for every combination of k and n.
k - number of closest neighbours observed
n - the resolution of the feature map

The best result was gotten for n = 20 and k = 1.

## Keypoint Clasification

This method uses the keypoints given by the Media Holistic Pipeline as the input for the model. Two versions were tested, one that only takes in the x and y coordinates and one taht also takes in the estimated depth (z coordinate).

## EfficientNetB3

EfficientNetB3 is a well established state of the art architecture for image clasification and is here mostly for comparison reasons.

## Results

 - kNN model (n=20, k=1) - accuracy = 56%
 - Keypoint Classification (x and y) - accuracy = 85.8%
 - Keypoint Classification (x, y and z) - accuracy = 95.6%
 - Extended MNIST CNN - accuracy = 96.25%
 - EfficientNetB3 - accuracy = 99%