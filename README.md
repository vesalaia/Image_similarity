# Image_similarity

## Table of Content


## Introduction

This is part of the Digital Humanities Hackathon 2023 (DHH23) project. The theme of our group was Enlightening Illustrations: Analyzing the Role of Images in Early Modern Scientific Publications. This is a continuous of the project to explore and analyse how the computer vision tools could be used to identify similar images among the dataset. This information would be essential for understanding how the pictures where re-used during the 18th century. 

## Approach

The basic idea is to use deep learning methods to convert images to vectors and use similarity metrics to identify other similar images among the dataset. Cosine similarity is is used to measure of the similarity between two image feature vectors. It measures the angle between the vectors, if the value is close to one vectors are similar and if it is close to zero then there is no similarity. Cosine similarity is often used to compare the similarity between documents and images.

The transformation from images to vectors is done using multi layer Convolutional Neural Networks (CNN) based classification models, Resnet in this case. This approach enables layers close to the input to learn low-level features (e.g., lines or edges) and layers deeper in the model to learn more abstract features (e.g., shapes or specific objects). The CNN architecture consists of several layers (e.g., 3 × 3 convolution and related activation functions) followed by
pooling (e.g., max pooling). This part of the CNN is called feature extraction. Then, two fully connected layers follow feature extraction, and the final layer is a softmax layer to predict the class label for the image. As here we are only interested on feature map or feature vectors, the fully connected layers are omitted and resulting vectors are used for calculating the similaity between differet images. Resnet is an CNN architecture that uses skip layers (a.k.a. shortcut), where data bypasses one or more layers and is fed deeper into the network, enabling training in very deep networks. For this project I use Resnet-18 with 18 layers and Resnet-50 with 50 layers.

## Visualization

## Conclusions

## References

## Data
Early modern illustrations can be found from [Data repository](https://github.com/dhh23/early_modern_data))
