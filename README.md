# Image_similarity

## Table of Content


## Introduction

This is part of the Digital Humanities Hackathon 2023 (DHH23) project. The theme of our group was Enlightening Illustrations: Analyzing the Role of Images in Early Modern Scientific Publications. This is a continuous of the project to explore and analyse how the computer vision tools could be used to identify similar images among the dataset. This information would be essential for understanding how the pictures where re-used during the 18th century. 

## Approach

The basic idea is to use deep learning methods to convert images to vectors and use similarity metrics to identify other similar images among the dataset. Cosine similarity is used to measure the similarity between two image feature vectors. It measures the angle between two vectors. If the value is close to one, vectors are similar. If it is close to zero, then there is no similarity. Cosine similarity is often used to compare the similarity between documents and images.

The transformation from images to vectors uses multi layer Convolutional Neural Networks (CNN) based classification models, Resnet in this case. This approach enables layers close to the input to learn low-level features (e.g., lines or edges) and layers deeper in the model to learn more abstract features (e.g., shapes or specific objects). The CNN architecture consists of several layers (e.g., 3 × 3 convolution and related activation functions) followed by pooling (e.g., max pooling). This part of the CNN is called feature extraction. Then, two fully connected layers follow feature extraction, and the final layer is a softmax layer to predict the class label for the image [Good2016]. We are only interested in feature map/feature vectors,  therefore, the fully connected layers are omitted and resulting feature vectors are used for calculating the similaity between differet images. Resnet is an CNN architecture that uses skip layers (a.k.a. shortcut), where data bypasses one or more layers and is fed deeper into the network, enabling training in very deep networks [Xie2017]. For this project I use Resnet-18 (18 layers) and Resnet-50 (50 layers), the size of feature vectors are 512 and 2048, respectively.

## Visualization

## Conclusions

## References

[Good2016] Ian Goodfellow, Yoshua Bengio, Aaron Courville: Deep learning. The MIT Press. 2016

[Xie2017] Xie Saining, Girshick Ross, Dollar Piotr, Tu Zhuowen, He Kaiming. Aggregated Residual Transformations for Deep Neural Networks. Computer Vision
and Pattern Recognition. 2017.

## Data
Early modern illustrations can be found from [Data repository](https://github.com/dhh23/early_modern_data))
