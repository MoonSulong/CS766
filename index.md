# Satellite Imagery Classification
<br/> 
#### SuLong Zhou, Linhong Lyu  {szhou78, llyu8}@wisc.edu
#### May 4, 2020
<br/> 

## Motivation

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
<img src="https://raw.githubusercontent.com/MoonSulong/CS766/master/Workflow.png" width = "700" height = "500" />  
</center>
<br/> 


## The Classifiers

In this project, the following classifaction algorithms are used:

1. Segmentation
2. Random Forest
3. Simple Neural Network
4. Convolution Neuarl Network
<br/>

### Segmentation

The Otsu Method is an unsupervised method and it was initially designed to select a threshold to separate an object out of its background, through the gray-level histogram of the image. It is equivalent to K-Means Method but the Otsu Method can provide the global optimal solution, while K - Means Method may be trapped in local optimum point.

The main idea of the Otsu Method is to minimize the summation of the **intra-class variance** $V_j$ of all clusters $C_j$, while maximizing **inter-class variance** $V_{0,1}$. The intra-variance of a cluster shows the summation of squared distance of each element to the center of the cluster as we defined, and the smaller value of the inner-variance presents the closer distance each point toward the center of the cluster, which shows a closer relationship or higher similarity that the elements in this cluster share. Therefore, the best separation of the whole set of elements should group the similar elements in the same cluster as optimally as possible. In mathematics, this is equal to minimize the summation of inner-variance inside each cluster. The objective function is formulated as the follow:

$$
    \min\limits_{C_0, C_1} \sum\limits_{j = 0,1} V_j= \min\limits_{C_0, C_1} \sum\limits_{j = 0,1} \sum\limits_{i\in C_j}p_i\cdot (x_i - \mu_j)^2
$$

Furthermore, the summation of each cluster's inner-variance and the inter-class variance should be equal to the total-variance of the whole set, which is a constant for a fixed data set. 

$$
    V = \sum\limits_{j=0,1} V_j + V_{0,1}
$$

Therefore, this is equivalent to maximize the inter-class variance $V_{0,1}$:

$$
    \max\limits_{C_0, C_1}\sum\limits_{j= 0,1} ((\sum\limits_{i\in C_j}p_i)\cdot (\mu_j - \mu)^2)
$$


### Random Forest
[Random forests](https://en.wikipedia.org/wiki/Random_forest) are an ensemble learning method, which concludes a multitude of decision trees. Random forests give outputs by the mode of classes or mean predictions of individual trees. They improve the performance of a single tree by reducing the problem of overfitting using bagging and feature randomness. 

Random forests mainly have the following advantages: 
1. Random forests could be efficient since it could be trained parallelly. 
2. Random forests have high tolerance for missing features
3. Random forests generate outputs with comparing high accuracy.

The image below roughly depicts the random forest algorithm.
<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/RF.png" width = "700" height = "540" />  
</center>
<br/> 


### Neural Network
[A neural network](https://en.wikipedia.org/wiki/Neural_network) is a network or circuit of neurons, connecting by weighted edges. Generally, a neural network has hidden layers, and activation functions on those hidden nodes to generate outputs. To train the weights of edges, neural works should define forward functions, loss functions and calculate backward functions to update the weights. 

A simple neural network is shown as below. A dense layer means fully connections. Besides, the method of dropout is also used here to reduce overfitting by randomly ignoring some nodes during training process. 


<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/NN.png" width = "500" height = "410" />  
</center>
<br/> 


### Convolution Neural Network
[A Convolutional Neural Network]( https://en.wikipedia.org/wiki/Convolutional_neural_network) is a Deep Learning algorithm. CNN’s networks use convolution in place of general matrix multiplication in at least one of their layers. One advantages of CNN is that, instead of fully connected, only sparse interaction is used here. This significantly reduce the complexity of calculations while maintain equivariant representations. Besides, CNN requires lower pre-process and has the ability to learn the filters/characters itself.  In a word, CNN is suitable to capture the Spatial and Temporal dependencies in an image, which means that CNN could be trained to understand the sophistication of the image well.

In this project, two layers of CNN and one dense layer are used.


<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/CNN.png" width = "1000" height = "450" />
</center>
<br/> 


## Classification Results
### Two Classes with Segmentation and Random Forest
We classified the imagery into 2 categories, water and non-water. With segmentation using Otsu algorithm, the histogram was computed and a threshold at value of 2016.13 was selected. 

<center>
<img src="https://raw.githubusercontent.com/MoonSulong/CS766/master/hist.png" />  
</center>

The figure below shows the results with segmentation on the left and with random forest on the right. The difference is significant, the left has more blue pixels that represent water.
<center>
<img src="https://raw.githubusercontent.com/MoonSulong/CS766/master/2classes.png" />  
</center>
<br/> 

### Three Classes with Rnadom Forest, Simple NN and CNN
We classified the imagery into 3 categories: water(blue), vegetation(gree), and bare(yellow). 10 trees were set for the random forest algorithm. 1 hidden fully connected layer was set for the simple NN model while 3 hidden layer (2 CNN and 1 Dense) were set for the CNN model. 

The figure below shows the results with segmentation on the left, with a simple NN in the middle, and with a CNN on the right. The difference is not easy to catch, so we circled some of them in shapes. The red circles show the difference between random forest and simple NN while the red rectangles show the difference between simple NN and CNN.  
<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/3classes.png" />  
</center>
<br/>

## Accuracy assessment
We used confusion matrix to evaluate the accuracy for segmentation and random forest, and used cross-entropy loss to evaluate the NN model. For counfusion matrix, we randomly selected 200 test points, and generated tables below. For cross-entropy loss, we set drop out in case of overfit, divided training into 10 epochs and then check the accuracy on both the training and test sets.  

For 2 classes classification, the overall accuracy of segmentation can only reach 87% while the overall accuarcy of RF outperforms with 97%.

For 3 classes classification, the overall accuracy of random forest still performs well with 96%. The NN shows close but lower total accuracy with 92% and 95% respectively. In addition, there is a gap between training accuracy and test accuracy for NN models. Although it shows very high accuracy in training set for both NN models, 98% and 99%, they drop on the test sets.      

### Confusion Matrix

Actual\Predict       | Non-water            | Water                | Total           
:------------------: | :------------------: | :------------------: | :------------------:
Non-water            | 80                   | 10                   | 90             
Water                | 16                   | 94                   | 110  
Total                | 96                   | 104                  | 200
Overall accuracy = (80 + 94) / 200 = 87%
<br/>

Actual\Predict       | Non-water            | Water                | Total           
:------------------: | :------------------: | :------------------: | :------------------:
Non-water            | 93                   | 2                    | 95             
Water                | 4                    | 101                  | 105  
Total                | 97                   | 103                  | 200
Overall accuracy = (93 + 101) / 200 = 97%
<br/>

Actual\Predict       | Bare                 | Vegetation           | Water               | Total
:------------------: | :------------------: | :------------------: | :------------------:|:------------------:
Bare                 | 41                   | 3                    | 0                   | 44        
Vegetation           | 2                    | 50                   | 2                   | 54
Water                | 0                    | 1                    | 101                 | 102
Total                | 43                   | 54                   | 103                 | 200
Overall accuracy = (41 + 51 + 101) / 200 = 96%
<br/>

### Cross-entropy Loss

Training 

```
Epoch 1/10
3376/3376 [==============================] - 12s 4ms/step - loss: 0.0724 - accuracy: 0.9925
Epoch 2/10
3376/3376 [==============================] - 13s 4ms/step - loss: 0.1053 - accuracy: 0.9862
Epoch 3/10
3376/3376 [==============================] - 12s 4ms/step - loss: 0.0566 - accuracy: 0.9900
Epoch 4/10
3376/3376 [==============================] - 13s 4ms/step - loss: 0.0487 - accuracy: 0.9922
Epoch 5/10
3376/3376 [==============================] - 12s 4ms/step - loss: 0.0166 - accuracy: 0.9964
Epoch 6/10
3376/3376 [==============================] - 12s 4ms/step - loss: 0.0050 - accuracy: 0.9983
Epoch 7/10
3376/3376 [==============================] - 12s 4ms/step - loss: 0.0012 - accuracy: 0.9997
Epoch 8/10
3376/3376 [==============================] - 12s 4ms/step - loss: 5.6251e-04 - accuracy: 0.9997
Epoch 9/10
3376/3376 [==============================] - 12s 4ms/step - loss: 5.4370e-04 - accuracy: 0.9998
Epoch 10/10
3376/3376 [==============================] - 13s 4ms/step - loss: 8.1000e-04 - accuracy: 0.9997
```

Test
```
11509/11509 [==============================] - 28s 2ms/step - loss: 0.2928 - accuracy: 0.9534
```




<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>


## Discussion


## Future Work

## Reference

1. Mahmon, N.A. & Ya'acob, N. (2014) A review on classification of satellite image using Artificial Neural Network (ANN).
2. Joshi, N. etc. (2015) A Review of the Application of Optical and Radar Remote Sensing Data Fusion to Land Use Mapping and Monitoring
3. Phiri, D. & Morgenroth, J.(2017) Developments in Landsat Land Cover Classification Methods: A Review
4. Vala, H. J., Baxi, A. (2013). A review on Otsu image segmentation algorithm.
5. Gorelick, N., Hancher, M., Dixon, M., Ilyushchenko, S., Thau, D., Moore, R. (2017). Google Earth Engine:Planetary-scale geospatial analysis for everyone

