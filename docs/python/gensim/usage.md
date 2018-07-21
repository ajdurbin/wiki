# Gensim Usage #

High performance library for natural language processing. Efficiently stream files for processing instead of loading entire corpus into memory. Possible to save existing models, load and continue training on new data without needing to retrain on entire corpus. Tools include bag of words representations, word2vec embeddings with similarity queries, doc2vec embeddings with similarity queries, text summaries, keyword extraction, lsi, lda, hpd, phrases module for identifying phrases like secretary-of-state for preprocessing, lots of preprocessing utilities for cleaning text. Stemming and lemmatization utilities only work with Python 2.7, NLTK will have to be used otherwise. Gensim proclaims their versions of these utilities as being the superior option. Also provides API integration for Scikit-Learn, though we probably won't use those tools often.

# Links #
* <https://radimrehurek.com/gensim/tutorial.html>
* <https://github.com/RaRe-Technologies/gensim/tree/develop/docs/notebooks>
* <https://github.com/RaRe-Technologies/gensim/blob/develop/tutorials.md#tutorials>
* <https://github.com/jxieeducation/DIY-Data-Science/blob/master/frameworks/gensim.md#advanced-features>
* <https://github.com/RaRe-Technologies/gensim/blob/cc74b668ccbbfd558d5a54050c4489e6e06fed3d/docs/notebooks/gensim_news_classification.ipynb>

# general cleaner #
Writes multiple times but this is so we can apply clean/phrase/model fitting.
```
import re

import string

from gensim.parsing.preprocessing import remove_stopwords, strip_numeric, stem_text

from gensim.models import Phrases, Word2Vec

from gensim.models.phrases import Phraser

from gensim.corpora import Dictionary



def write_original_messages(df):

"""original message writing before cleaning"""

with open('original.txt', 'w', encoding = 'utf-8') as outfile:

for message in df['Message']:

outfile.write(' '.join(message.strip().split()) + '\n')

return 1



class OriginalCorpus(object):

"""stream original messages to bigram"""

def __iter__(self):

for line in open('original.txt', 'r', encoding = 'utf-8'):

yield line.split()



def write_bigram_messages(bigram):

"""use existing bigram on original messages and rewrite"""

with open('bigram.txt', 'w', encoding = 'utf-8') as outfile:

for line in open('original.txt', 'r', encoding = 'utf-8'):

outfile.write(' '.join(bigram[line.split()]) + '\n')

return 1



def write_clean_messages():

"""stream messages, clean, and rewrite to another file"""

remove = string.punctuation

remove = remove.replace('_', "")

pattern = r"[{}]".format(remove)

with open('clean.txt', 'w', encoding = 'utf-8') as outfile:

# for message in open('messages.txt', 'r', encoding = 'utf-8'):

for message in open('bigram.txt', 'r', encoding = 'utf-8'):

# alphanum = strip_non_alphanum(message) # punctuation

alphanum = re.sub(pattern, " ", message) # punctuation except for _ for bigrams

nonumeric = strip_numeric(alphanum) # numeric

nostops = remove_stopwords(nonumeric) # stopwords

outfile.write(' '.join(nostops.lower().strip().split()) + '\n')

return 1



class CleanCorpus(object):

"""stream bigram clean messages"""

def __iter__(self):

for line in open('clean.txt', 'r', encoding = 'utf-8'):

yield line.split()



def construct_dictionary():

dictionary = gensim.corpora.Dictionary(line.lower().split() for line in open('clean.txt', 'r', encoding = 'utf-8'))

# stoplist = set('for a of the and to in'.split())

# stop_ids = [dictionary.token2id[stopword] for stopword in stoplist

# if stopword in dictionary.token2id]

once_ids = [tokenid for tokenid, docfreq in iteritems(dictionary.dfs) if docfreq == 1]

# dictionary.filter_tokens(stop_ids + once_ids)

dictionary.filter_tokens(once_ids)

dictionary.compactify()

# print(dictionary)

# print(dictionary.token2id)

# dictionary.save('dictionaryname.dict')



if __name__ == '__main__':

df = load_data()

result = write_original_messages(df)

corpus_stream = OriginalCorpus()

phrases = Phrases(corpus_stream)

bigram = Phraser(phrases)

result = write_bigram_messages(bigram)

result = write_clean_messages()

corpus_stream = CleanCorpus()

model = Word2Vec(corpus_stream, workers = 4)

model.save('w2v_model')

# model.train(another_corpus_stream)

try:

print(model.wv.most_similar('renewal'))

print(model.wv.doesnt_match('renewal rnwl rwlrev rev changed'.split()))

print(model.wv['review'])

# probability of a text under a model

print(model.score(['this house haha'.split()]))

except Exception as e:

print(str(e))
```
