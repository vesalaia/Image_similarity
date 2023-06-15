# Image_similarity

## Table of Content


## Introduction

This sub-project is related to the Digital Humanities Hackathon 2023 (DHH23) project, specifically our group's theme of 'Enlightening Illustrations: Analyzing the Role of Images in Early Modern Scientific Publications.' The sub-project project aims to explore and analyze the use of computer vision tools to identify similar images within an illustration dataset. This information is crucial for understanding how images were reused during the 18th century.

The illustrations we are working with are part of the Eighteenth-Century Collections On-line (ECCO) database. ECCO consists of page images and texts from materials printed between 1700 and 1800 [Greg2021]. It encompasses around 32 million pages, featuring nearly 185 thousand different book titles. Our focus is on the botanical subset of illustrations, which includes approximately 100K pages from ECCO scientific books, representing nearly 5000 unique book titles. The dataset we are using contains roughly 13K botanical images."


## Approach

The basic idea is to use deep learning methods to convert images to vectors and use similarity metrics to identify other similar images among the dataset. Cosine similarity is used to measure the similarity between two image feature vectors. It measures the angle between two vectors. If the value is close to one, vectors are similar. If it is close to zero, then there is no similarity. Cosine similarity is often used to compare the similarity between documents and images.

The transformation from images to vectors uses multi layer Convolutional Neural Networks (CNN) based classification models, Resnet in this case. This approach enables layers close to the input to learn low-level features (e.g., lines or edges) and layers deeper in the model to learn more abstract features (e.g., shapes or specific objects). The CNN architecture consists of several layers (e.g., 3 × 3 convolution and related activation functions) followed by pooling (e.g., max pooling). This part of the CNN is called feature extraction. Then, two fully connected layers follow feature extraction, and the final layer is a softmax layer to predict the class label for the image [Good2016]. We are only interested in feature map/feature vectors,  therefore, the fully connected layers are omitted and resulting feature vectors are used for calculating the similaity between differet images. Resnet is an CNN architecture that uses skip layers (a.k.a. shortcut), where data bypasses one or more layers and is fed deeper into the network, enabling training in very deep networks [Xie2017]. For this project I use Resnet-18 (18 layers) and Resnet-50 (50 layers), the size of feature vectors are 512 and 2048, respectively.

Starting assumption was that as Resnet-50 used 2048-dimensional vector for extracting features instead of 512-dimensional vector of Resnet-18, it would be able to detect differences more accurately. The analysis was based on similarites and comparing plotted results using close reading.

## Visualization

As discussed above the similarity is based on feature vectors and the cosine distance between these vectors. The similarity metric varies between 0.0 and 1.0, where higher value refers to more similar images. Experiments seem to indicate that expected similarity is in reality somewhere between 0.5 and 1.0. As the similarity is not an exact metric it is difficult to detect when two images are actually same and when clearly different. Example show that value of 0.948 is calculated exatly for the same picture when 0.980 is calculated clearly for different image sharing similar patterns.

Figure 1 shows an example where the cosine similarity score is close to 0.5, and as it can be seen the picture are very different.  

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/Low_similarity.png" width="350" title="Picture 1">
  <br>
  Figure 1.
</p>
Figure 2 and 3 covers two sets of images, the 5 images on the left is an example that depicts an image and 4-most similar images from the dataset. Similarity metrics close to 0.95 demonstrate that three other images are almost the same and the metric for the 4th image indicates it is already quite diiferent. The five images on the right shows an example where similar images are not identified, however, the metric value of 0.87 seems to inidcate only some of the patterns in the picture are similar, but the actail pictures are clearly different. Resnet-18 is used for Figure 2 and Resnet-50 is used for Figure 3, where same kind of patterns are visible.  
<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/Resnet18_1.png" width="350" title="Picture 2">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/Resnet18_2.png" width="350" title="Picture 2">
<br>
 Figure 2.
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/Resnet50_1.png" width="350" title="Picture 3">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/Resnet50_2.png" width="350" title="Picture 3">
<br>
  Figure 3.
</p>

Figures 4, 5, 6, and 7 are used to demonstrate how the similarity between images changes as the cosine similarity increases. In case where similarity score is close to 0.5 the difference is clear and no common patterns are visible. When the similarity score increates first some common patterns and shapes are surfacing and later when score increases further the images are starting to look more and more similar.

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_05.png" width="350" title="Figure 4">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_05_2.png" width="350" title="Figure 4">
  <br>
 Figure 4.

</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_06_1.png" width="350" title="Figure 5">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_06_2.png" width="350" title="Figure 5">
  <br>
  Figure 5.

</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_07_1.png" width="350" title="Figure 6">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_07_2.png" width="350" title="Figure 6">
  <br>
  Figure 6.

</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_08_1.png" width="350" title="Figure 7">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_08_2.png" width="350" title="Figure 7">
<br>
  Figure 7
</p>
<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_09_1.png" width="350" title="Figure 8">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/similarity_09_2.png" width="350" title="Figure 8">
<br>
  Figure 8.
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/scatter_plot_resnet18.png" width="500" title="Picture 16">
<br>
 2-dimensional graph of feature vectors using Resnet-18
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/scatter_plot_resnet50.png" width="500" title="Picture 17">
<br>
 2-dimensional graph of feature vectors using Resnet-50
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/search_image_resnet18.png" width="600" title="Picture 18">
<br>
Results showing the relative distance to searched image (Resnet-18)
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/search_image_resnet50.png" width="600" title="Example 19">
<br>
  Results showing the relative distance to searched image (Resnet-18)
</p>

## Conclusions

## References

[Good2016] Ian Goodfellow, Yoshua Bengio, Aaron Courville: Deep learning. The MIT Press. 2016

[Greg2021] Gregg, S. (2021). Old Books and Digital Publishing: Eighteenth-Century Collections Online (Elements in Publishing and Book Culture). Cambridge: Cambridge University Press. doi:10.1017/9781108767415

[Xie2017] Xie Saining, Girshick Ross, Dollar Piotr, Tu Zhuowen, He Kaiming. Aggregated Residual Transformations for Deep Neural Networks. Computer Vision
and Pattern Recognition. 2017.


## Data
Early modern illustrations can be found from [Data repository](https://github.com/dhh23/early_modern_data))
