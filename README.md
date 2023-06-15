# Image_similarity

## Table of Content


## Introduction

This sub-project is related to the Digital Humanities Hackathon 2023 (DHH23) project, specifically our group's theme of 'Enlightening Illustrations: Analyzing the Role of Images in Early Modern Scientific Publications.' The sub-project project aims to explore and analyze the use of computer vision tools to identify similar images within an illustration dataset. This information is crucial for understanding how images were reused during the 18th century.

The illustrations we are working with are part of the Eighteenth-Century Collections On-line (ECCO) database. ECCO consists of page images and texts from materials printed between 1700 and 1800 [Greg2021]. It encompasses around 32 million pages, featuring nearly 185 thousand different book titles. Our focus is on the botanical subset of illustrations, which includes approximately 100K pages from ECCO scientific books, representing nearly 5000 unique book titles. The dataset we are using contains roughly 13K botanical images."


## Approach

The main concept behind our approach is to utilize deep learning methods, specifically Convolutional Neural Networks (CNN), to convert images into vectors. By employing similarity metrics, we can then identify other similar images within the dataset. One commonly used similarity metric is cosine similarity, which measures the angle between two image feature vectors. A value close to one indicates high similarity, while a value close to zero indicates no similarity. Cosine similarity is frequently employed for comparing the similarity between documents and images.

To transform images into vectors, we utilize a multi-layer CNN-based classification model, specifically the Resnet architecture. This approach enables the network to learn low-level features, such as lines or edges, in the initial layers, and progressively learn more abstract features, such as shapes or specific objects, in deeper layers. The CNN architecture includes various layers, such as 3x3 convolutions with related activation functions, followed by pooling, typically max pooling. This initial part of the CNN is known as feature extraction. Subsequently, two fully connected layers are employed, and the final layer is a softmax layer used for image classification [Good2016]. However, for our purposes, we are only interested in the feature maps or feature vectors, so we omit the fully connected layers and utilize the resulting feature vectors for calculating similarity between different images.

Resnet refers to a CNN architecture that incorporates skip layers, also known as shortcuts. These shortcuts allow data to bypass one or more layers and be fed deeper into the network, enabling training in very deep networks [Xie2017]. In this project, we utilize two variations of Resnet: Resnet-18 (18 layers) and Resnet-50 (50 layers). The size of the feature vectors extracted using Resnet-18 is 512, while Resnet-50 produces 2048-dimensional feature vectors.

Our initial assumption was that Resnet-50, with its 2048-dimensional feature vectors, would be more accurate in detecting differences compared to Resnet-18, which produces 512-dimensional feature vectors. The analysis was based on similarities, and we compared the plotted results using close reading techniques.

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
