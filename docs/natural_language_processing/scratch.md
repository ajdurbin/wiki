### About 
This wiki is for natural language processing methods and ideas.

### Packages 
  - gensim
  - nltk
  - spacy

### General 
  - text summarization (different algorithms than bag of words)
  - bag of words
  - tf-idf
  - word2vec
  - doc2vec
  - ngram
  - topic modeling
  - topic segmentation
  - lda/lsi
  - text tiling
  - wordclouds
  - keyword/keyphrase extraction
  - Gensim for modeling and named entity stuff. First stream tokenized text and then construct phrases and then from there train a word2vec/doc2vec model
  - gensim phrases model
  - svm text classification on tfidf vectors
  - sklearn has a couple good text articles
  - really good tutorial on text svm classification at https://towardsdatascience.com/machine-learning-nlp-text-classification-using-scikit-learn-python-and-nltk-c52b92a7c73a
  - can also do lds/lsi/neuralnetwork/naive bayes on these results from tfidf, clustering too for unsupervised problems (example on sklearn)
  - gensim has common phrases utility to be included in phrases function, so if we are bigramming and want to to identify words in a common sequence like 'of' in 'secretary of state' without trigramming. 
  - Grid search best topic models from https://www.machinelearningplus.com/nlp/topic-modeling-python-sklearn-examples/
  - Possible method to be used in searching a large corpus of documents for keywords and returning the documents where the probability of certain topics is highest: https://stackoverflow.com/questions/15377290/unsupervised-automatic-tagging-algorithms
  - Looking at most important words in SVM text classification https://medium.com/@aneesha/visualising-top-features-in-linear-svm-with-scikit-learn-and-matplotlib-3454ab18a14d