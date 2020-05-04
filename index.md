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

<center>
<img src="https://raw.githubusercontent.com/MoonSulong/CS766/master/madison.png" />  
</center>
<br/> 

## Frame Work

<center>
<img src="https://raw.githubusercontent.com/LydiaLyu/CS766/master/FrameWork.png" width = "700" height = "500" />  
</center>
<br/> 


## The Classifiers
<br/>

In this project, the following classifaction algorithms are used:

1. Histogram
2. Random Forest
3. Neural Network
4. Convolution Neuarl Network

<br/>


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


