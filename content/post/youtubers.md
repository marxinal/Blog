---

title: "Personality Profiling of Youtube Vloggers"
date: 2021-09-25T02:56:48+01:00
draft: false
tags: ["projects"] 
---
Description: Building a model that will predict scores on the Big Five Personality Traits of Youtube Vloggers using different aspects of their videos. 

Data: The YouTube personality dataset consists of a collection of behavorial features, speech transcriptions, and personality impression scores for a set of 404 YouTube vloggers that explicitly show themselves in front of the a webcam talking about a variety of topics including personal issues, politics, movies, books, etc. There is no content-related restriction and the language used in the videos is natural and diverse. For 80 of the 404 vloggers the personality impression scores are missing. The model is used to predict scores for these 80 vloggers.

**Dependent Variable:** _(Big Five Personality Traits)_  
- Extraversion
- Neuroticism
- Conscientiousness 
- Agreeableness
- Openess to Experience


**Predictors:** _(Independent Variables/Features)_

The predictors stemmed from three different aspects:
1) Speech transcripts
2) AudioVisual remarks (behavioural aspects) 
3) Personality scores of other vloggers

Based on the aforementioned, I constructed the following features:

Features derived from the speech transcript texts: 

- Number of times the word "um" is used
  - The first feature is the number of times the words "um", "uhm", and "uh" are used. These are so called filler words to avoid silences. Even though a direct    
    relationship between the use of filler words could not be shown in earlier research (Laserna et al., 2014), they could still indicate difficulty finding words     to say which might be related to for example introversion.
- NRC lexicon
  -The second feature is the NRC. The NRC is a large database that enables us to associate words with 8 common emotions, which are either negative or positive. How    much each emotion occurs in a text might tell us something about the personality of the speaker. In earlier research sentiment analysis using NRC was shown to      be an effective personality predictor (Christian et al. 2021).
- Bing lexicon
  - The third feature is Bing. Bing doesn't allow us to assign emotions to a word but it does let us classify words as positive or negative. The number of words in     a text that are positive or negative might also tell us something about de personality of the speaker. Also since the distribution of postive and negative     
    words is different in Bing than in NRC it seems sensible to use both.
- Count of Syllables 
  - The sixth feature is the number of syllables that each vlogger uses. Earlier research has shown that this is an effective predictor for mainly agreeableness
   (Metha et al., 2020). Even though this study was on written text, this finding might also hold for speech.
- Number of questions
  - The seventh feature is the number of questions in a vlog. Asking questions might for example be related to insecurity and thus introversion or to curiousness   
    and thus opnenness to experience.
- Swear words 
  - The eight feature is the number of swear words that is used. The study of Metha et al. 2020 also showed this was an effective predictor for agreeabless
    Besides that it also intuitively makes sense that the number of swear words would predict agreeableness (the more swear words the lower agreeableness)
    and possibly other big five traits. 
- Number of pauses
  - The ninth feature is the number of pauses for each vlogger. Since there are a lot of ways pauses or silence can be used in speech Kostiuk (2012) so it might       predict personality in different ways. However if there are a lot of pauses this likely indicates difficulty finding words which might be associated with           introversion. 
- Self-Reference/"I" Words 
  - Our tenth feature is the use of self-reference words. Self-reference words are associated with multiple personality traits so their use might be a good
    predictor for the Big Five. Earlier research showed for example an association between the use of the word "I" and neuroticism (Scully & Terry, 2011). 
- Some additional features based on similar reasoning: 
  - "We" Words Relative Frequency 
  - Average Number of characters in a sentence
  - AFINN 
  - Negation frequency
  - Mean Word Count Per Sentence

**Methods and Models employed:** 
- Here I employed a linear model along with stepwise regression methods (using the forward and the hybrid approach). Additionally, an alternative model with non-linear transformations was fitted in order to potentially increase the explained variance, and was thus compared to the primary model that does not violate the assumption of additivity. 

<ins>Model Evaluation and Model Comparison:</ins> 





