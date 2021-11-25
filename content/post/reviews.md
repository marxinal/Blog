---
title: "Reviews"
date: 2021-11-26T00:41:53+01:00
draft: false
tags: ["projects"]
image: "amazon.jpeg"
---

### Title: Facial Expression Recognition from Images

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

## Fifth Project

### Title: Customer Satisfaction from Amazon Reviews

Description: Here I tried to build a classifier that automatically recognizes customer satisfaction from textual reviews of baby products that were sold on Amazon.com. 

Data: Reviews and 5 star ratings were collected by Amazon on their site by inviting customers to enter a review of a product that had bought. The extracted data from Amazon contains: the item described, the review text as a (long) string, and a numeric rating. Customers are assumed the be "satisfied" if the numeric rating is greater than the midpoint of the scale.

**Dependent Variable:** _(Satisfaction)_  

Level of satisfaction of customers, ranging from 1 to 5.

**Predictors:** _(Independent Variables/Features)_

Features were extracted from tokenized (words) text transcripts.

_Actual Feature Engineering_

# Term Frequency - Inverse Document Frequency Features
- The **TF-IDF based on single words**, without filtering for the stopwords
- The **TF-IDF based on bigrams**, which we also did not filter on stopwords. We found this to be a very useful feature for sentiment analysis (Tan, Wang & Lee, 2002). 
- The **TF-IDF based on trigrams** also without filtering for the stopwords. Again, trigrams were also found to be useful feature for sentiment analysis (Wu, Li, & Xu, 2006). 

The following process was employed: 

- **document occurence**: 
    > 0-1 encoding of the presence or absence of a token in a document (here: review)
    
- **token counts**: 
    > simple counts $n_{t,d}$ of each token $t$ within documents $d$ (resulting in a document by term matrix, or DTM)

- **term frequency ($TF_{d,t}$)**: 
    > the relative frequency of a term within a document $\displaystyle {n_{d,t} \over  \sum_t n_{d,t}}$

- **inverse document frequency ($IDF_t$)**: 
    > inverse the relative frequency with which a term occurs among the $N$ documents, expressed on a log scale (a measure of 'surprise') as  $-\log\left({DF_t \over N}\right)$ Here $DF_t$ is the number of documents that contain the token $t$.

- **the $TFIDF_{d,t}$**: 
    > the product of TF and IDF

- **vector space embeddings**: 
    > advanced features like factor loadings (eigen vectors) from a PCA of the DTM, or "word2vec" representations of words, sentences, and paragraphs (not discussed here), usually obtained by training neural networks on a very large corpus


The motivation for $TF_{d,t}$ is simply that the more often a token $t$ occurs in a document, the more likely it is that the topic of the document is closely related to that token. A problem of $TF_{d,t}$ is that it does not take into account that certain words simply occur more frequently because of their role in language (such as 'a', 'but', etc.). 

The motivation for the $IDF_t$ is that the more wide spread the use of a token $t$ is among all documents, the less likely it conveys information about the topic of any particular document. Hence, the more surprising a word is, the more likely it conveys information about the topic of the document in which it is found. 

# Features regarding counts of the Reviews
- **Word Count** per Review
- **Sentence Count** per Review
(Ren & Hong, 2017)

# Sentiment Features
- **The NRC sentiment score**: Lists associations of words with eight emotions (anger, fear, anticipation, trust, surprise, sadness, joy, and disgust) and two sentiments (negative and positive)
- **The Bing sentiment score**: The bing lexicon categorizes words in a binary fashion into positive and negative categories. 
- **The Afinn sentiment score**: The Afinn lexicon assignes words with a score between -5 and 5, where negative scores indicate a negative sentiment and positive scores indicate a positive sentiment.

# Features of specific sentiment words 
- **Swear Words**: Another valid linguistic correlate of sentiments is swearing (Hashimi, Hafez & Mathkour, 2015)
- **Negation Words Feature**: Negations are words like no, not, and never. When people want to express the opposite meaning of a particular word or sentence, this is done by inserting a specific negation. Negating words have a correlation with other words in that sentence and we assume they are useful for predicting the sentiments. 
- **Function Words (Functors) Feature**: These are words that have little lexical meaning or that have ambiguous meaning which express grammatical relationships among other words within a sentence, or specify the attitude or mood of the speaker. Therefore we assumed this to be a feature of use. 
- **Pronouns Feature**: A pronoun is a word that takes the place of a noun. So words like: "I", "me", "he", "she", "herself", "you", "everybody" etc.
- **Preposition Feature**: These are words or a group of words that are used before a noun, pronoun, or noun phrase to show direction, time, place, location, spatial relationships, or to introduce an object. These are words like "in," "at," "on," "of," and "to etc. 
(Liang, Sun, Sun, & Gao, 2017)

**Methods and Model employed:**

Here Lasso and Ridge Regression were used. And they were compared based on their
_accuracy_, _sensitivity_, and _specificity_. 

**Model Comparison**
I decided to keep the Lasso Model, since it has the highest scores on both accuracy and sensitivity. Although ridge has a somewhat similar accuracy and a better specificity, the difference in sensitivity is much higher in favour of the lasso model. Thus, based on this analysis and the one before with the features and their weights I decided to use the lasso model. 

**Results:**

The overall model accuracy employed on a test set was 85%. 



References

** **
Tan, C. M., Wang, Y. F., & Lee, C. D. (2002). The use of bigrams to enhance text categorization. Information Processing & Management, 38(4), 529–546. https://doi.org/10.1016/s0306-4573(01)00045-0

Hashimi, H., Hafez, A., & Mathkour, H. (2015). Selection criteria for text mining approaches. Computers in Human Behavior, 51, 729–733. https://doi.org/10.1016/j.chb.2014.10.062

Wu, S. T., Li, Y., & Xu, Y. (2006). Deploying Approaches for Pattern Refinement in Text Mining. Sixth International Conference on Data Mining (ICDM’06). Published. https://doi.org/10.1109/icdm.2006.50

Liang, H., Sun, X., Sun, Y., & Gao, Y. (2017). Text feature extraction based on deep learning: a review. EURASIP Journal on Wireless Communications and Networking, 2017(1). https://doi.org/10.1186/s13638-017-0993-1

Ren, G., & Hong, T. (2017). Investigating Online Destination Images Using a Topic-Based Sentiment Analysis Approach. Sustainability, 9(10), 1765. https://doi.org/10.3390/su9101765

Zhang, L., Hua, K., Wang, H., Qian, G., & Zhang, L. (2014). Sentiment Analysis on Reviews of Mobile Users. Procedia Computer Science, 34, 458–465. https://doi.org/10.1016/j.procs.2014.07.013
