---
title: "Facial"
date: 2021-11-25T23:58:16+01:00
draft: true
image: "facial.jpeg"
---
Description: Using data extracted from images to build an algorithm that is able to recognize emotions from photographs from facial expressions. 

Data:

1. **Where do the data come from? (To which population will results generalize?)**
- The data came from the CK+ dataset. The obtained results from this statistical analysis will generalize to black & white photos representative of four emotions. Those are sadness, happiness, disgust, and anger. When taking into consideration the actual generalizability of the data, it is arguable that this dataset will not be able to generalize well to children and infants, but also other non Euro-American faces. The reason being that 81% of the dataset contains only Euro-American faces, and only 13% Afro-American and 6% other groups. Likewise, only adult faces were used for training purposes, in particular pariticipants were 18 to 50 years of age (Lucey, et al., 2010).

2. **What are candidate machine learning methods? (models? features?)**
- Possible machine learning algorithms could be QDA, LDA, KNN, Multinomial Regression, Random Forrest, Ridge and Lasso regression. Some of them were used here, and some were left out due to high computational (CPU and RAM) demands.

3. **What is the Bayes' error bound?**  
Literature suggests that Facial Recognition Algorithms can reach almost perfection with a 99.97% accuracy rate. Derived from: https://www.csis.org/blogs/technology-policy-blog/how-accurate-are-facial-recognition-systems-–-and-why-does-it-matter Whereas, if looking specifically at recognizing one of the four aforementioned emotions, Mollahosseini et al. (2016), suggests the inter rater reliability for recognition is 79.6% for happiness, 69.7% for saddnes, 67.6% for disgust, and 62.3% anger among in total 11 facial expressions. So taken together, our Bayes' error bound should probably be somewhere around 85-90% for the present data set.

**Dependent Variable:** _(Four Emotions)_  

- Anger
- Disgust
- Happiness 
- Sadness

**Predictors:** _(Independent Variables/Features)_

Here I use histograms of pixel intensities to compute useful features. Here we mostly focus on histogram edges, in particular vertical, horizontal and diagonal. But also: 

1. **Averages (features that capture a specific region of histogram or descriptives):** 
- Mean 
- Mode 
- Median
- Standard Deviation
- Variance

2. **Distributional measures (specific shapes of histogram):**

- Range 
- Quartiles (25% Quartile Ranges, 75% Quartile Ranges)
- Kurtosis: This measure describes the specific shape of a particular histogram where this shape is identified by measuring the peakedness of the histogram. If it's a normal distribution the peakedness is 3, which means that the most values are in and around the middle of the distribution. If it is not normal distributed the peakedness of the histogram, ans thus the most values are in the sides.
- Skewness: Skewness is measured by identifying asymmetry of a particular histogram. The histogram is balanced when there is zero-value. It is on the left tail when it is negative, and it is on theright tail when it is positive.
- Median Absolute Deviation (MAD): The absolute average distance between the mean and every data point.

3. **Spectral-inspired features:**
* Power: The power is the probability that the test will find a statistically significant difference between the amplitude of the signals. Where it reflects the variance of the amplitude of the signals as well as the squared mean summed.
- Energy: The energy is a measure the localized change of the image. Source:          https://stackoverflow.com/questions/4562801/what-is-energy-in-image-processing
- Full L amplitude: Each point at every (x,y) is called amplitude or intensity of an image. Amplitude image shows how the tip deflected as it encountered sample surface. Images are similar to topography showing the map of the slope of the sample, but Z scale is no in linear units. Using other words, amplitude image is the image of error signal of amf. Source: https://findanyanswer.com/what-is-amplitude-in-image-processing
-Crest factor: Crest factor is a parameter of a waveform, such as alternating current or sound, showing the ratio of peak values to the effective value. In other words, crest factor indicates how extreme the peaks are in a waveform. As such can also be used for analysing histograms of pixel intensity. 
- Spectral peak: The function spectrum() gives an estimation of the spectrum of a function. In order to be able to derive information about the nature of the function and more about the pixels, we estimated statistical features on the spectrum features. In particular we included spectral peak as our feature.

4. **Other strategies:**

-Using edge coordinates (horizontal, vertical, and diagonal)

**Methods and Models employed:** 

Before fitting a model, I first split the data into a training and validation set. Then I compared the accuracies of the following models:

- Random Forest
- Boosted Decision Tree
- Classification Tree
- Support Vector Machine
- Linear Discriminant Analysis
- Quadratic Discriminant Analysis
- Bagging

Based on the accuracies  the SVM performs the best compared to the other methods, so I used that as my final model. Also QDA performs better than LDA which might due to the size of the data set, or due to the non-linear data.

**Results:**

The overall model accuracy employed on a test set was 85%. 
