# Text Readability Project



1. Introduction
2. Executive Summary
3. Next Steps
4. Data Dictionary
5. Technical Appendix


# Introduction

What makes english difficult to read? The concepts can help us understand which resources are appropriate and accessible for different levels of English readers.

For beginner English readers, it is especially important to provide the correct reading material so as the ensure their motivation continues. One example of application in the project is to promote reading for low-income children as a way to close the **[Word Gap](https://en.wikipedia.org/wiki/Word_gap#:~:text=The%20term%2030%2Dmillion%2Dword,Word%20Gap%20by%20Age%203%22.)**.

Current readability models rely on things such as sentence and word length to rank a text’s readability. However, this is not an accurate measurement and it causes variation in results. Additionally, these metrics cannot be used to specialize recommendations based on certain readers’ needs such as a grasp of complex grammar but a low vocabulary, or the opposite.

The readability of English can be linked to both semantic, morphological and syntactic features unique in English as well as features that make any language more or less easy to read. This project will use these features to create a more accurate model that ranks readability and can parse what might be more difficult for some readers but easier for others.

This project was inspired by and based off of the [Kaggle CommonLit Readability Prize](https://www.kaggle.com/c/commonlitreadabilityprize).


# Executive Summary

Ranking readability using semantic, syntactic and morphological features of text to better recommend the correct resources for different levels of English readers. There are a multitude of applications and expansions of this project, from implementation in teaching resources, to independent learners or understanding how text can be more accessible to certain groups in mass-communication.  

**Metrics**

Models were evaluated using MeanSquaredError.

The baseline MSE is 1.05 using the mean. With FleschReadingEase readability metrics as a feature with Linear Regression, the MSE was .918.

With 43 features, PCA was used to reduce the dimensionality by about 35%, accounting for 94% of the total initial features.

Ridge and GradientBoostingRegressors were gridsearched for the best regularization methods. Without PCA, using the original 43 features, Ridge’s alpha was 10, while for GradientBoostingRegressor kept the default values. With PCA, Ridge’s gridesearch returned an alpha of 100.

A sequential neural network was also attempted, however after introducing l2 regularization and early dropout, it still underperformed compared to the best simple linear models and it was not selected as the final model.

**Conclusions:**

Ridge was selected as the final model for PCA data, as it had the lowest MSE, of 0.59, and only a 2% fluctuation in r2 scores in test and training data, of the model accounting for 44% of the variation in the readability score in testing data, and 46% in training.

This model outperformed the baseline and current readability metrics and still has the ability to extract features from text in future advancements.

**Limitations**

Certain features can vary by reader or group. For example, word frequency was determined by the frequency of a word’s use in online text. This may not be accurate frequencies that English readers encounter if they are young readers, without internet access, or are ESL learners.

The group who ranks readability could cause bias towards how text is read and therefore it is important in expansions of the project, to allow analysis of difficult features along with readability to provide more informed recommendations.


## **Next Steps:**


## The model is only accounting for 44% of variability in the readability of text. Extracting additional features are the next steps to improve the model.


## Implementing Nueralcoref to model on pronoun coreference, improving the syntax that the model will use to parse sentences, and creating neural networks that can explain the predictability and cohesiveness of a paragraph's storytelling would be future projects.

It would be ideal to make a model that predicts which features cause the most standard deviation in the readability, as a way of improving recommendations by reader.


##**Data Dictionary:**

Data Source: [Kaggle: CommonLit Readability Prize](https://www.kaggle.com/c/commonlitreadabilityprize/data)


<table>
  <tr>
   <td>Name
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>id
   </td>
   <td>Unique ID for excerpt
   </td>
  </tr>
  <tr>
   <td>url_legal
   </td>
   <td>URL of source - this is blank in the test set.
   </td>
  </tr>
  <tr>
   <td>license
   </td>
   <td>License of source material
   </td>
  </tr>
  <tr>
   <td>target
   </td>
   <td>Readability ranking, from
   </td>
  </tr>
  <tr>
   <td>standard_error
   </td>
   <td>Amount that the readability rating varied from the average
   </td>
  </tr>
  <tr>
   <td>avg_sent_length
   </td>
   <td>The average number of words per sentence
   </td>
  </tr>
  <tr>
   <td>subtree_per_sent
   </td>
   <td>The average number of subtrees per sentence
   </td>
  </tr>
  <tr>
   <td>subtree_len
   </td>
   <td>The average number of words per subtree
   </td>
  </tr>
  <tr>
   <td>subtree_len_by_num
   </td>
   <td>The multiplication of subtree_len and subtree_per_sent
   </td>
  </tr>
  <tr>
   <td>node_types
   </td>
   <td>The number of unique tags starting each node
   </td>
  </tr>
  <tr>
   <td>left(right)(total)_dep
   </td>
   <td>The number of dependencies of subject, root verb, and direct objects in the text. The total number of dependences or to the left, right direction of the word.
   </td>
  </tr>
  <tr>
   <td>left(right)_dep_dist
   </td>
   <td>The number of words between the main word and its dependencies, measuring only subject, root verb, and direct objects in the text. The number words between the left or right children.
   </td>
  </tr>
  <tr>
   <td>dep_dist
   </td>
   <td>The average number of words between the words and all children.
   </td>
  </tr>
  <tr>
   <td>pron_ratio
   </td>
   <td>The number of pronouns used in a text compared to the number of nouns or proper nouns that are the subject, object or prepositional object
   </td>
  </tr>
  <tr>
   <td>UniqueTagTypes
   </td>
   <td>'WRB', 'DT', 'JJ', 'NNS', 'VBD', 'IN', 'NN', 'PRP', 'RB', 'VBN', 'RP', 'CC', 'WDT', 'VBG', 'NNP', 'TO', 'VB', 'MD', 'PRP$', 'VBP', 'EX', 'VBZ', 'PDT', 'JJR', 'NNPS', 'WP', 'POS', 'RBR', 'RBS', 'JJS', 'WP$',
   </td>
  </tr>
  <tr>
   <td>avg_word_freq
   </td>
   <td>The measure of how often a word occurs in the English language, using PyPI’s wordfreq measurements. Only measures verbs, nouns or adjectives and adverbs.
   </td>
  </tr>
  <tr>
   <td>lexical_diversity
   </td>
   <td>The count of a set of lemmatized verb, noun, adverb, adjective words in the text. How diverse is the language that is used in the text.
   </td>
  </tr>
  <tr>
   <td>lexdiv_wordfreq
   </td>
   <td>The interaction between word frequency and lexical diversity.
   </td>
  </tr>
  <tr>
   <td>Topics
   </td>
   <td>'Outdoors', 'Family', 'Science', 'Nature', 'War'
   </td>
  </tr>
</table>



## **Technical Appendix:**



* Compile_Data.ipynb
    * This notebook creates a pickled version of spaCy Doc type from the training data and saves to a local computer.
* Preprocessing.ipynb
    * Loads pickled version of previously parsed NLP training data from AWS S3 server. Performs feature extraction and compiles data for modeling as well as EDA.
*  Model.ipynb
    * Establishes baseline score, final feature selection, and PCA on data before modeling using Ridge. Prepares and exports Kaggle’s test data predictions for submission.  

**Libraries:**



* PyPI: [Wordfreq](https://pypi.org/project/wordfreq/)
    * wordfreq is a Python library for looking up the frequencies of words in many languages, based on many sources of data. [Sources](https://pypi.org/project/wordfreq/#:~:text=Sources%20and%20supported%20languages) for frequency listed
* PyPi: [Lexical-diversity](https://pypi.org/project/lexical-diversity/)
    * Calculates the lexical diversity within a given text.
* PyPI: [Berkeley Neural Parser](https://spacy.io/universe/project/self-attentive-parser)
    * A pretrained constituency parser integrated with spaCy.
* PyPI: [Readability](https://pypi.org/project/readability/)
* spaCy
    * Natural language processing allowing dependency, part of speech and morphology parsing and tagging.
* [AWS S3](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Categories=categories%23storage&trk=ps_a134p000004f2aOAAQ&trkCampaign=acq_paid_search_brand&sc_channel=PS&sc_campaign=acquisition_US&sc_publisher=Google&sc_category=Storage&sc_country=US&sc_geo=NAMER&sc_outcome=acq&sc_detail=aws%20s3&sc_content=S3_e&sc_matchtype=e&sc_segment=468090540619&sc_medium=ACQ-P|PS-GO|Brand|Desktop|SU|Storage|S3|US|EN|Text&s_kwcid=AL!4422!3!468090540619!e!!g!!aws%20s3&ef_id=Cj0KCQjw8vqGBhC_ARIsADMSd1BJPi2bK23guVmyujsvVbVilusVuYDnGGK_D1-HhzwgetYDRkOwCIAaAvu2EALw_wcB:G:s&s_kwcid=AL!4422!3!468090540619!e!!g!!aws%20s3&awsf.Free%20Tier%20Types=*all)
* [Boto3](https://boto3.amazonaws.com/v1/documentation/api/1.9.42/guide/quickstart.html)
* _Sklearn_
* _Pandas_
* _Numpy_
* _Matplotlib and Seaborn_

**Resources**



* [Kaggle CommonLit Readability Prize](https://www.kaggle.com/c/commonlitreadabilityprize).
* [How to generate an LDA Topic Model for Text Analysis](https://medium.com/@yanlinc/how-to-build-a-lda-topic-model-using-from-text-601cdcbfd3a6)
* [Feature Engineering](https://towardsdatascience.com/feature-engineering-combination-polynomial-features-3caa4c77a755)
* [Data Source](https://www.kaggle.com/c/commonlitreadabilityprize/data)
* [Pickled NLP-parsed data](https://s3.console.aws.amazon.com/s3/buckets/picklenlp?region=us-east-2&tab=objects)
