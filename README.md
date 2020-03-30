# CORD-19-SeVeN

This repository contains pre-trained relation embeddings (nearly 100k) trained using the SeVeN pipeline on the CORD-19 (https://pages.semanticscholar.org/coronavirus-research) dataset. Download links at the bottom of this README.

## Semantic Vector Networks

SeVeN is a dedicated vector space for relational knowledge. In practice, this means a word embedding space where each vector corresponds to a _pair of words_. These pairs are pre-selected based on PPMI scores.

SeVeN paper: Espinosa-Anke, L. & Schockaert, S. (2018). SeVeN: Augmenting Word Embeddings with Unsupervised Relation Vectors. In Proceedings of the 27th International Conference on Computational Linguistics (pp. 2653-2665). https://www.aclweb.org/anthology/C18-1225/
SeVeN blog post: https://medium.com/voice-tech-podcast/seven-semantic-vector-networks-9b0329383a78
SeVeN code: https://bitbucket.org/luisespinosa/seven

### Querying the CORD-19-SeVeN space

Simply load the relation vectors using the amazing `gensim` library (https://github.com/RaRe-Technologies/gensim). Then, you can check whether the space contains relation vectors for a query word:

```bash
In [40]: [k for k in m.vocab if 'pregnant__' in k]
Out[40]: 
['pregnant__lactating',
 'pregnant__women',
 'pregnant__postpartum',
 'pregnant__trimester',
 'pregnant__breastfeeding',
 'pregnant__cows',
 'pregnant__fetuses',
 'pregnant__heifers',
 'pregnant__immunocompromised',
 'pregnant__abortion']
```

Same as with traditional word embeddings, proximity in the space correlates with similar meaning. In this case this extends to _relational similarity_. A good use case for these embeddings is inspire new research questions or search queries on the CORD-19 corpus. For example, similar vectors to the pair `<patients,received>` show other Subject-Object relationships which are semantically similar:

```bash
In [41]: m100.most_similar('patients__received')
Out[41]: 
[('patients__underwent', 0.973887026309967),
 ('subjects__received', 0.9730947017669678),
 ('people__died', 0.9486745595932007),
 ('travelers__visited', 0.9454649686813354),
 ('pilgrims__attended', 0.9416547417640686),
 ('nurses__worked', 0.9391869306564331),
 ('donors__blood', 0.9385848045349121),
 ('pts__received', 0.9371707439422607),
 ('people__ill', 0.9370725154876709),
 ('persons__infected', 0.9353940486907959)]
```

The cluster around `<pertussis,pneumophila>` shows several similar `<disease,bacteria>` bacteria relations.

```bash
In [39]: m100.most_similar('pertussis__pneumophila')
Out[39]: 
[('catarrhalis__influenzae', 0.9747452735900879),
 ('enteroviruses__adenoviruses', 0.9711717963218689),
 ('influenzae__meningitidis', 0.9699296951293945),
 ('pneumoniae__catarrhalis', 0.9684340357780457),
 ('bocavirus__adenovirus', 0.9670071601867676),
 ('aureus__influenzae', 0.9663506746292114),
 ('aureus__pyogenes', 0.9656254053115845),
 ('coccidiosis__cryptosporidiosis', 0.9653065204620361),
 ('influenzae__catarrhalis', 0.9651409387588501),
 ('pneumoniae__pneumophila', 0.9643831849098206)]
```

### Downloading CORD-19-SeVeN embeddings

There are relation embeddings of three different sizes: 10, 100 and 200 dimensions. The smaller the dimensionality, the more abstract the semantic similarities are. The examples in this README are from the 100d space.

[https://drive.google.com/drive/folders/1VblKWwdZqB5Qot6M5hH8rq_dFgA8VlMy?usp=sharing!](DOWNLOAD HERE)
