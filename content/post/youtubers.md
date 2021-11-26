---

title: "Personality Profiling of Youtube Vloggers"
date: 2021-09-25T02:56:48+01:00
draft: false
tags: ["projects"]
image: "youtubers.jpeg" 
---
Description: Building a model that will predict scores on the Big Five Personality Traits of Youtube Vloggers using different aspects of their videos. 

Data: The YouTube personality dataset consists of a collection of behavioral features, speech transcriptions, and personality impression scores for a set of 404 YouTube vloggers that explicitly show themselves in front of the a webcam talking about a variety of topics including personal issues, politics, movies, books, etc. There is no content-related restriction and the language used in the videos is natural and diverse. For 80 of the 404 vloggers the personality impression scores are missing. The model is used to predict scores for these 80 vloggers.

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

#### Features derived from the speech transcript texts: 

- _Number of times the word "um" is used_
  - The first feature is the number of times the words "um", "uhm", and "uh" are used. These are so called filler words to avoid silences. Even though a direct relationship between the use of filler word     could not be shown in earlier research (Laserna et al., 2014), they could still indicate difficulty finding words to say which might be related to for example introversion.
- _NRC lexicon_
  - The second feature is the NRC. The NRC is a large database that enables us to associate words with 8 common emotions, which are either negative or positive.
   How much each emotion occurs in a text might tell us something about the personality of the speaker. In earlier research sentiment analysis using NRC was shown to be an effective personality predictor 
   (Christian et al. 2021).
- _Bing lexicon_
  - The third feature is Bing. Bing doesn't allow us to assign emotions to a word but it does let us classify words as positive or negative. The number of words in a text that are positive or negative
    might also tell us something about the personality of the speaker. Also since the distribution of positive and negative words is different in Bing than in NRC it seems sensible to use both.
- _Count of Syllables_ 
  - The sixth feature is the number of syllables that each vlogger uses. Earlier research has shown that this is an effective predictor for mainly agreeableness (Metha et al., 2020). Even though this
    study was on written text, this finding might also hold for speech.
- _Number of questions_
  - The seventh feature is the number of questions in a vlog. Asking questions might for example be related to insecurity and thus introversion or to curiousness and thus opnenness to experience.
- _Swear words_
  - The eight feature is the number of swear words that is used. The study of Methaet al. 2020 also showed this was an effective predictor for agreeabless. Besides that it also intuitively makes sense 
    that the number of swear words would predict agreeableness (the more swear words the lower agreeableness) and possibly other big five traits. 
- _Number of pauses_
  - The ninth feature is the number of pauses for each vlogger. Since there are a lot of ways pauses or silence can be used in speech Kostiuk (2012) so it might predict personality in different ways.
    However if there are a lot of pauses this likely indicates difficulty finding words which might be associated with introversion. 
- _Self-Reference/"I" Words_
   - The tenth feature is the use of self-reference words. Self-reference words are associated with multiple personality traits so their use might be a good predictor for the Big Five. 
     Earlier research showed for example an association between the use of the word "I" and neuroticism (Scully & Terry, 2011). 
- Some additional features based on similar reasoning: 
  - _"We" Words Relative Frequency_
  - _Average Number of characters in a sentence_
  - _AFINN_
  - _Negation frequency_
  - _Mean Word Count Per Sentence_

**Methods and Models employed:** 

  Features with high correlation with other features (collinearity) and those with non-zero variance were removed.

  Here I employed a linear model along with stepwise regression methods (using the forward and the hybrid approach) predicting the combined output variable consisting of all scores on the Big Five 
  Personality Traits. Additionally, an alternative model with non-linear transformations was fitted in order to potentially increase the explained variance, and was thus compared to the primary model that  does not violate the assumption of additivity.
 
**Model Evaluation and Model Comparison:** 

 The simple model with no non-linear transformations had the highest explained variance, thus this model was used for prediction purposes.

**Results:**

  My model explained 76% of the variance in Big Five Personality Traits scores using a test set. 



References

** ** 

Christian, H., Suhartono, D., Chowanda, A., & Zamli, K. Z. (2021). Text based personality prediction from multiple social media data sources using pre-trained language model and model averaging. Journal of Big Data, 8(1). https://doi.org/10.1186/s40537-021-00459-1 <br/><br/>

Lee, C. H., Kim, K., Seo, Y. S., & Chung, C. K. (2007). The Relations Between Personality and Language Use. The Journal of General Psychology, 134(4), 405–413. https://doi.org/10.3200/genp.134.4.405-414 <br/><br/>

Laserna, C. M., Seih, Y. T., & Pennebaker, J. W. (2014). Um . . . Who Like Says You Know. Journal of Language and Social Psychology, 33(3), 328–338. https://doi.org/10.1177/0261927x14526993 <br/><br/>

Mehta, Y., Fatehi, S., Kazameini, A., Stachl, C., Cambria, E., & Eetemadi, S. (2020). Bottom-Up and Top-Down: Predicting Personality with Psycholinguistic and Language Model Features. 2020 IEEE International Conference on Data Mining (ICDM). Published. https://doi.org/10.1109/icdm50108.2020.00146 <br/><br/>

Scully, I. D., & Terry, C. P. (2011). Self-Referential Memory for the Big-Five Personality Traits. Psi Chi Journal of Psychological Research, 16(3), 123–128. https://doi.org/10.24839/1089-4136.jn16.3.123



