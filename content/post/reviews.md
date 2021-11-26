---
title: "Customer Satisfaction from Amazon Reviews"
date: 2021-10-13T00:41:53+01:00
draft: false
tags: ["projects"]
image: "amazon.jpeg"
---

Description: Here I tried to build a classifier that automatically recognizes customer satisfaction from textual reviews of baby products that were sold on Amazon.com. 

Data: Reviews and 5 star ratings were collected by Amazon on their site by inviting customers to enter a review of a product that had bought. The extracted data from Amazon contains: the item described, the review text as a (long) string, and a numeric rating. Customers are assumed the be "satisfied" if the numeric rating is greater than the midpoint of the scale.

**Dependent Variable:** _(Satisfaction)_  

Level of satisfaction of customers, ranging from 1 to 5.

**Predictors:** _(Independent Variables/Features)_

Features were extracted from tokenized (words) text transcripts.

_Actual Feature Engineering_

#### Term Frequency - Inverse Document Frequency Features
- The **TF-IDF based on single words**, without filtering for the stopwords
- The **TF-IDF based on bigrams**, which we also did not filter on stopwords. We found this to be a very useful feature for sentiment analysis (Tan, Wang & Lee, 2002). 
- The **TF-IDF based on trigrams** also without filtering for the stopwords. Again, trigrams were also found to be useful feature for sentiment analysis (Wu, Li, & Xu, 2006). 

The following process was employed: 

- **document occurence**: 
    > 0-1 encoding of the presence or absence of a token _t_ in a document _n_(here: review)
    
- **token counts**: 
    > simple counts of each token _t_ within documents (resulting in a document by   term matrix, or DTM)

- **term frequency (TF)**: 
    > then calculate the relative frequency of a token _t_ within a document _n_ 

- **inverse document frequency (IDF)**: 
    > inverse the relative frequency with which a term occurs among the _N_
documents, expressed on a log scale (a measure of 'surprise') calculated by dividng the number of documents that contain the token _t_over the number of total number of
documents (N). 
- **the TFIDF**: 
    > the product of TF and IDF
    
The motivation for TF is simply that the more often a token _t_ occurs in a document, the more likely it is that the topic of the document is closely related to that token. A problem of TF is that it does not take into account that certain words simply occur more frequently because of their role in language (such as 'a', 'but', etc.). 

The motivation for the IDF_t is that the more wide spread the use of a token _t_ is among all documents, the less likely it conveys information about the topic of any particular document. Hence, the more surprising a word is, the more likely it conveys information about the topic of the document in which it is found. 

Thus, the TFIDF banks on both of these ideas and quantifies the important of a term for a given document.

#### Features regarding counts of the Reviews
- **Word Count** per Review
- **Sentence Count** per Review
(Ren & Hong, 2017)

#### Sentiment Features
- _The NRC sentiment score_
   - Lists associations of words with eight emotions (anger, fear, anticipation, trust, surprise, sadness, joy, and disgust) and two sentiments (negative and positive)
- _The Bing sentiment score_ 
  - The bing lexicon categorizes words in a binary fashion into positive and negative categories. 
- _The Afinn sentiment score_ 
  - The Afinn lexicon assignes words with a score between -5 and 5, where negative scores indicate a negative sentiment and positive scores indicate a positive sentiment.

#### Features of specific sentiment words 
- _Swear Words_
  - Another valid linguistic correlate of sentiments is swearing (Hashimi, Hafez &
Mathkour, 2015)
- _Negation Words Feature_
  - Negations are words like no, not, and never. When people want to express the opposite meaning of a particular word or sentence, this is done by inserting a specific negation. Negating words have a correlation with other words in that sentence and we assume they are useful for predicting the sentiments. 
- _Function Words (Functors) Feature_ T
  - These are words that have little lexical meaning or that have ambiguous meaning which express grammatical relationships among other words within a sentence, or specify the attitude or mood of the speaker. Therefore we assumed this to be a feature of use. 
- _Pronouns Feature_
  - A pronoun is a word that takes the place of a noun. So words like: "I", "me", "he", "she", "herself", "you", "everybody" etc.
- _Preposition Feature_
  - These are words or a group of words that are used before a noun, pronoun, or noun phrase to show direction, time, place, location, spatial relationships, or to introduce an object. These are words like "in," "at," "on," "of," and "to etc. 
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
