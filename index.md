# Satellite Imagery Classification
<br/> 
##### SuLong Zhou, Linhong Lyu  {szhou78, llyu8}@wisc.edu
###### May 4, 2020
<br/> 

## Motivation
<br/>

The interactions between the natural environment and human societies on earth have a long and complex history. Land use and cover change(LUCC) is one of many primary driving factors for the dynamic process. Land use shows how people exploit and utilize the landscape – whether for development, conservation, or mixed uses. Land cover data documents how much of a region is covered by forest, wetland, water or other land types. Since LUCC over time and space in response to evolving economic, social, and biophysical conditions, the study of LUCC is essential to better understand the impacts of the human-nature coupled changing system, such as sustainable development and climate change.

Remote sensing has been the most popular approach to moniter and analyze the LUCC with the help of classification of satellite imagery. There are continuous efforts in progress to research these image process technologies including image segmentation, supervised classfication, and nerual network. However, many challenges remain in dicsussion. For example, how to automatically select a threshold for image segmentation apporach, which classifier should be selected given different scenarios because of time, spatial, and spectral varities of imagery. In our porject, we propose：

1. Optimize the threshold selection of single band method for water detection
2. Re-implement random forest supervised methods for classification
3. Train a simple NN and a CNN model to improve the accuracy
4. Evaluate and compare the accuracy across different classifiers



<br/>

## Platform and Datasets

### Platform
[Google Earth Engine](https://earthengine.google.com) consists of a multi-petabyte satellite imagery data catalog co-located with a high-performance, intrinsically parallel cloud computation service. Users can access through an Internet-accessible application programming interface (API) and an associated web-based interactive development environment (IDE) that enables rapid prototyping and visualization of results. [TensorFlow](https://www.tensorflow.org/) is an open source ML platform that supports advanced ML methods such as deep learning. We ran image segmentation and random forest classifier on GEE while creating and training the NN model on TensorFlow, and then exporting the resutls back to GEE. 

### Datasets

[Landsat series of satellites](https://www.sciencedirect.com/topics/earth-and-planetary-sciences/landsat), launched by NASA and USGS, provides the longest temporal record of space-based surface observations. Landsat 8 OSL is the latest imagery data collection with moderate resolution that consists of 9 spectural bands in the visible, near-infrared, short wave, and thermal infrared. We used its standard Level-1 data products in GEE and selected 6 bands of imagery composite for the classification.

* Band 2 Blue (0.450 - 0.51 µm) 30 m
* Band 3 Green (0.53 - 0.59 µm) 30 m
* Band 4 Red (0.64 - 0.67 µm) 30 m
* Band 5 Near-Infrared (0.85 - 0.88 µm) 30 m
* Band 6 SWIR 1(1.57 - 1.65 µm) 30 m
* Band 7 SWIR 2 (2.11 - 2.29 µm) 30 m

The below figure show an example with true color(R,G,B) and false color(NR,R,G) composite of Landsat 8 imagery centered on city of Madison.    

<center>
<img src="https://raw.githubusercontent.com/MoonSulong/CS766/master/madison.png" />  
</center>
<br/> 

## Workflow

<center>
<img src="https://raw.githubusercontent.com/MoonSulong/CS766/master/FrameWork.png" width = "700" height = "500" />  
</center>
<br/> 


## The Classifiers
<br/>

In this project, the following classifaction algorithms are used:

1. Segmentation
2. Random Forest
3. Simple Neural Network
4. Convolution Neuarl Network

<br/>

### Segmentation

The Otsu Method is an unsupervised method and it was initially designed to select a threshold to separate an object out of its background, through the gray-level histogram of the image. It is equivalent to K-Means Method but the Otsu Method can provide the global optimal solution, while K - Means Method may be trapped in local optimum point.

The main idea of the Otsu Method is to minimize the summation of the inner-variance $V_j$ of all clusters $C_j$, which is called **intra-class variance**. The inner-variance of a cluster shows the summation of squared distance of each element to the center of the cluster as we defined, and the smaller value of the inner-variance presents the closer distance each point toward the center of the cluster, which shows a closer relationship or higher similarity that the elements in this cluster share. Therefore, the best separation of the whole set of elements should group the similar elements in the same cluster as optimally as possible. In mathematics, this is equal to minimize the summation of inner-variance inside each cluster. The objective function is formulated as the follow:

$$
    \min\limits_{C_0, C_1} \sum\limits_{j = 0,1} V_j= \min\limits_{C_0, C_1} \sum\limits_{j = 0,1} \sum\limits_{i\in C_j}p_i\cdot (x_i - \mu_j)^2
    \label{ObjectiveFunc1}
$$

Furthermore, the summation of each cluster's inner-variance and the inter-class variance should be equal to the total-variance of the whole set [23], which is a constant for a fixed data set. 
$$
    V = \sum\limits_{j=0,1} V_j + V_{0,1}
$$
Therefore, the previous objective function \textbf{Equation \ref{ObjectiveFunc1}} is equivalent to maximize the inter-class variance $V_{0,1}$:
$$
    \max\limits_{C_0, C_1}\sum\limits_{j= 0,1} ((\sum\limits_{i\in C_j}p_i)\cdot (\mu_j - \mu)^2)
    \label{ObjectiveFunc2}
$$



### Random Forest

The image below roughly depicts the random forest algorithm.
<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/RF.png" width = "700" height = "540" />  
</center>
<br/> 


### Neural Network

<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/NN.png" width = "500" height = "410" />  
</center>
<br/> 

### Convolution Neural Network

<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/CNN.png" width = "1000" height = "450" />
</center>
<br/> 


## Results
<br/>

### Type 1: 2 Classes


<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/2classes.png" />  
</center>
<br/> 


### Type2: 3 Classes

<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/3classes.png" />  
</center>
<br/>

For test math equations
$$
a^2 + b^2 = c^2
$$




<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


