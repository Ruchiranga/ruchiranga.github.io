---
layout: post
section-type: post
title: Feature based face detection with ViolaJones algorithm
category: tech
tags: [ 'computervision' ]
---
![Face detection](/img/posts/violajones/face.jpg)
What you see above is how the ViolaJones algorithm detected my face! This result can be obtained with a couple of lines of code in MATLAB and is not a difficult task with all the powerful features it provide.

In general, the problem addressed in face detection is to classify a given image depending on whether it contains a human face or not. Feature based face detection is one intuitive approach in solving it. The general concept behind this approach is to identify certain interesting features of a given image and depending on the features identified, decide whether the image contains a human face or not. The features can be actual physical features of a face like eyes, nose and mouth or any other interesting points when looked from an image processing perspective.

Not all feature based face detection algorithms utilize machine learning techniques in getting the problem solved. Some approaches utilize image processing techniques to identify interesting features and deduce decision based upon them. Out of the machine learning algorithms used in feature based face detection, the Adaboost algorithm proposed by Paul Viola and Michael Jones (commonly known as the ViolaJones algorithm) is the most popular one.

The specific features used in the ViolaJones algorithm are a set of rectangular patterns called Haar features. Some examples of such Haar features are shown in the following figure.

![Haar Features](/img/posts/violajones/haar.PNG)

These feature masks are laid over the image in every possible manner and a value that represents the amount that particular region in the image matches the feature mask is calculated. The higher the value, the better the region in the image contains that particular feature. The authors of this research have also suggested a very efficient way of performing this process programmatically by creating an intermediate representation of the image known as the ‘Integral image’.

Once we have a feature set and a set of positive and negative training images, the next step is to find the most important set of features that contribute in accurately classifying the images. This is where machine learning techniques are used. Adaboost is one such technique that can be used in selecting the features and training the classifier.

In simple terms consider having n different features and a set of m positive and negative training images. Each feature is evaluated on each of the images and a certain value is obtained. A certain weight is associated with all such values obtained and initially all those weights would have equal values. Then for a certain feature, a threshold is determined considering the distribution of the feature evaluations of each of the training images and their weight values. The images producing a value greater than that threshold with respect to a particular feature are classified as having a face and vise versa. Depending on the threshold value decided, there will almost always be some misclassified images as well. The weight values of all such misclassified images are obtained and the sum of all those is used as the error measure for that particular feature. This process is carried out for all the features and the feature that yields the minimum error measure is chosen to be included in the final classifier. Then before moving on to the next iteration, the weights of misclassified image values for all the features are increased so that they would be given more attention in getting them classified correctly during the threshold determination in the next iteration. This is the machine learning process followed in the Adaboost learning algorithm.

Once the most important features have been selected, the algorithm would assign weights to each of them and a linear combination of them would give out a strong classifier function that can be used to classify a given image determining whether it contains a human face or not.