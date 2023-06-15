# Image_similarity

## Introduction

This sub-project is related to the Digital Humanities Hackathon 2023 (DHH23) project, specifically our group's theme of 'Enlightening Illustrations: Analyzing the Role of Images in Early Modern Scientific Publications.' The sub-project project aims to explore and analyze the use of computer vision tools to identify similar images within an illustration dataset. This information is crucial for understanding how images were reused during the 18th century.

The illustrations we are working with are part of the Eighteenth-Century Collections On-line (ECCO) database. ECCO consists of page images and texts from materials printed between 1700 and 1800 [Greg2021]. It encompasses around 32 million pages, featuring nearly 185 thousand different book titles. Our focus is on the botanical subset of illustrations, which includes approximately 100K pages from ECCO scientific books, representing nearly 5000 unique book titles. The dataset we are using contains roughly 13K botanical images."


## Approach

The main concept behind our approach is to utilize deep learning methods, specifically Convolutional Neural Networks (CNN), to convert images into vectors. By employing similarity metrics, we can then identify other similar images within the dataset. One commonly used similarity metric is cosine similarity, which measures the angle between two image feature vectors. A value close to one indicates high similarity, while a value close to zero indicates no similarity. Cosine similarity is frequently employed for comparing the similarity between documents and images.

To transform images into vectors, we utilize a multi-layer CNN-based classification model, specifically the Resnet architecture. This approach enables the network to learn low-level features, such as lines or edges, in the initial layers, and progressively learn more abstract features, such as shapes or specific objects, in deeper layers. The CNN architecture includes various layers, such as 3x3 convolutions with related activation functions, followed by pooling, typically max pooling. This initial part of the CNN is known as feature extraction. Subsequently, one or more fully connected layers are employed, and the final layer is a softmax layer used for image classification [Good2016]. However, for our purposes, we are only interested in the feature maps or feature vectors, so we omit the fully connected layers and utilize the resulting feature vectors for calculating similarity between different images.

Resnet refers to a CNN architecture that incorporates skip layers, also known as shortcuts. These shortcuts allow data to bypass one or more layers and be fed deeper into the network, enabling training in very deep networks [Xie2017]. In this project, we utilize two variations of Resnet: Resnet-18 (18 layers) and Resnet-50 (50 layers). The size of the feature vectors extracted using Resnet-18 is 512, while Resnet-50 produces 2048-dimensional feature vectors.

Our initial assumption was that Resnet-50, with its 2048-dimensional feature vectors, would be more accurate in detecting differences compared to Resnet-18, which produces 512-dimensional feature vectors. The analysis was based on similarities, and we compared the plotted results using close reading techniques.

## Usage
All analysis and visualization code is in one Jupyter Notebook. Key parameters and setting for program are:  [code]  (https://github.com/vesalaia/Image_similarity/blob/main/Search4SimilarImages-FeatureVector.ipynb))

<ul>
  <li>DATA_DIR: folder for all images you want to analyze, copy all images to this folder prior to the analysis</li>
  <li>DB_DIR: folder where all data structures are stored to avoid re-calculation</li>
</ul>

The project is based on a blog post by [Korz2020], but the original code has been modified and expanded. The initial code converted all images into 256x256 pixels, following the format assumed by Resnet. However, it is now possible to calculate feature vectors on the fly, allowing for the utilization of images in their original formats. Additionally, feature vectors are stored on disk to avoid redundant vector creation when the program is rerun at a later stage.

Initially, the program only supported Resnet-18, but it has since been extended to include Resnet-50. Furthermore, it would be relatively straightforward to further extend the program to support other CNN architectures.

The visualization aspect has also been enhanced to provide a clearer understanding of the differences between various similarity values and the practical implications of cosine distance.

## Visualization

As mentioned earlier, the similarity between images is determined by comparing their feature vectors using cosine distance. The similarity metric ranges from 0.0 to 1.0, with a higher value indicating a greater similarity between images. However, experimental results suggest that the expected similarity often falls between 0.5 and 1.0. Since similarity is not an exact measurement, it becomes challenging to determine whether two images are identical or clearly different. For instance, an example demonstrates that a cosine similarity score of 0.948 can be obtained for the same picture, while a score of 0.980 can be calculated for different images that share similar patterns.

Figure 1 presents an example where the cosine similarity score is approximately 0.5, and as clearly depicted, the images are quite dissimilar.

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/Low_similarity.png" width="350" title="Picture 1">
  <br>
  Figure 1.
</p>
Figure 2 and 3 depict two sets of images. In Figure 2, the left side showcases an example image along with the four most similar images from the dataset. Similarity metrics close to 0.95 indicate that three of the images are nearly identical, while the metric for the fourth image suggests it is already quite different. On the right side, five images are displayed where similar images are not identified. However, the metric value of 0.87 suggests that only some patterns in the pictures are similar, while the actual images are clearly different. Resnet-18 is used for Figure 2, and Resnet-50 is used for Figure 3, both exhibiting similar behaviour.

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

Figures 4, 5, 6, and 7 serve to illustrate the changes in image similarity as the cosine similarity increases. When the similarity score is close to 0.5, the differences between images are evident, with no recognicable common patterns. As the similarity score increases, common patterns and shapes begin to emerge, and as the score continues to rise, the images appear increasingly similar.

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

Visualizing high-dimensional feature vectors can be challenging due to their complexity. To address this, Principal Component Analysis (PCA) is employed to transform the 512/2048-dimensional feature vectors into a two-dimensional representation while preserving crucial information. This allows for easy plotting and visualization of the results.

Figures 9 and 10 showcase two examples from the complete botanical illustration dataset. One example corresponds to Resnet-18, while the other corresponds to Resnet-50. The plots illustrate the variation of different feature vectors (depicted in blue). The searched image is represented by a black point, while similar images are denoted by red points.

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/scatter_plot_resnet18.png" width="500" title="Figure 9">
<br>
Figure 9. 2-dimensional graph of feature vectors using Resnet-18
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/scatter_plot_resnet50.png" width="500" title="Figure 10">
<br>
Figure 10. 2-dimensional graph of feature vectors using Resnet-50
</p>

Figures 11 and 12 provide visualizations of the cosine distance between the searched image and the search results. The 2-dimensional space represents the relative location of the searched image, and the search results are plotted in the same space. The distance between points reflects the similarity, where closer results indicate higher similarity to the searched image. The threshold used to determine the results is set at 0.94 for both models.

There is a noticeable difference between the two models. In the case of Resnet-18, only one similar image is identified within the threshold, whereas the Resnet-50 based model can identify 10 similar images that meet the threshold.

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/search_image_resnet18.png" width="600" title="Figure 11">
<br>
Figure 11. Results showing the relative distance to searched image (Resnet-18)
</p>

<p align="center">
  <img src="https://github.com/vesalaia/Image_similarity/blob/main/images/search_image_resnet50.png" width="600" title="Figure 12">
<br>
Figure 12. Results showing the relative distance to searched image (Resnet-18)
</p>

## Conclusions

The initial assumption was that the Resnet-50 model would outperform the Resnet-18 model since it captures four times more features from each image. However, this assumption could not be verified during the project as both models produced very similar results. This can be observed, for instance, in Figures 2 and 3 (left-hand side), where the same images are among the four most similar images with almost identical similarity scores. However, upon closer examination, it could be argued that the Resnet-50 model is better at detecting similarities in less similar images, as shown on the right-hand side of the figures, where the most similar image appears almost the same despite being clearly different—the shape and patterns are nearly identical.

Although the similarity scores between images are largely the same for both models, some differences can be noticed when analyzing the full dataset. When examining the four most similar images for the full dataset (Table), it was observed that in 204 cases (1.6%), both models produced exactly the same combination of images, while for 590 images (4.5%), three common images were shared, and for 2246 images (17.1%), two common images were shared. In 5008 cases (38.1%), one image was shared, and in 5103 cases (38.8%), there was no overlap in the shared images. Close reading suggests that if there is a clear similarity between images, both models are capable of detecting it. However, when the images are clearly different, there is more variation in the scores.

By setting the threshold at a level of 0.94 or higher, the results are relatively consistent, and both methods are able to predict close similarity. It is important to note that cosine similarity, being based on extracted features, is not an exact measure, and a high value does not necessarily mean that the images are the same. Instead, it confirms that the images include similar elements, such as patterns and shapes.

<table>
  <tr>
    <th>#images</th>
    <th>Count</th>
  </tr>
  <tr>
    <td>4</td>
    <td>204</td>
  </tr>
  <tr>
    <td>3</td>
    <td>590</td>
  </tr>
  <tr>
    <td>2</td>
    <td>2246</td>
  </tr>
  <tr>
    <td>1</td>
    <td>5008</td>
  </tr>
  <tr>
    <td>0</td>
    <td>5103</td>
  </tr>
</table>
## References

[Korz2020] Maciej D. Korzec. Blog post. https://towardsdatascience.com/recommending-similar-images-using-pytorch-da019282770c

[Good2016] Ian Goodfellow, Yoshua Bengio, Aaron Courville: Deep learning. The MIT Press. 2016

[Greg2021] Gregg, S. (2021). Old Books and Digital Publishing: Eighteenth-Century Collections Online (Elements in Publishing and Book Culture). Cambridge: Cambridge University Press. doi:10.1017/9781108767415

[Xie2017] Xie Saining, Girshick Ross, Dollar Piotr, Tu Zhuowen, He Kaiming. Aggregated Residual Transformations for Deep Neural Networks. Computer Vision
and Pattern Recognition. 2017.

## Data
Early modern illustrations can be found from [Data repository](https://github.com/dhh23/early_modern_data)
