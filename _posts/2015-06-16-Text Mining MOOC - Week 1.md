---
title: "Text Mining MOOC - Week 1"
author: "sameer"
date: "June 16, 2015"
output: html_document
layout: post
tags: [Text Mining]
permalink: textminingweek1
comments: yes
---

I am taking the [Text Mining and Analytics MOOC](https://www.coursera.org/course/textanalytics). The first week, we learned about mining paradigmatic and syntagmatic relations.

- Paradigmatic relations are between words which are of the same class (i.e. cat, dog). These can be found by finding those words which have the most similar contexts (words on the right, words on the left).

- Syntagmatic relations are between words whose meaning can be related to one another (i.e. cat, eats). These relations are mined by searching for co-occuring elements.  

The most technical part of this discussion arises when trying to measure the similarity of two documents using simply Term Frequency to represent the components of a document vector $$d = (x_1,x_2,\dots,x_n)$$, where _n_ reprsents the size of the vocabulary, and $$x_i$$ are the normalized counts of term _i_ in that document. The main issue if we define the similarity between two documents as simply the scalar product between two document vectors is that
there is a bias towards matching more words that occur more frequently, instead of matching more distinct terms (think how much students use the word _force_ in their rationales, often in very different ways). Hence two concepts are introduced:

- Sublinear Term Frequency transformations  
  + \\(TF = 0\\) or \\(TF=1\\) (only record presence of word, but no change if word appears many times)
  + \\(TF=\log(1+x)\\) where x is the raw word count
  + BM25, where in \\(TF = \frac{(k+1)x}{x+k}\\). \\(k\\) is a parameter, such that the upper bound of even the most frequent words max's out at \\(k+1\\)
  
- Inverse Document Frequency  
  + \\(IDF(w)=log[\frac{M+1}{k}]\\), where \\(M\\) is the total number of documents, and \\(k\\) is the number of documents that contain the term \\(w\\)
 
Next, the idea of conditional entropy is introduced as a means of mining for syntagmatic relations (or co-occuring terms). Entropy measures the randomess of a random variable
\\[H(X_w) = \sum_{v\in(0,1)} -p(X_w=v)\cdot\log_2[p(X_w=v)]\\]

An entropy maximum of 1 means that the random variable X is hard to predict, while an entropy of 0 means that the random variable is certain (and hence very easy to predict). The random variable $$X_w$$ defined as 1 if the word $$w$$ is in the document, and 0 if it is not.

Conditional entropy has the same form, except the probabilities are conditioned on knowledge of one of the two words. 
\\[ H(X_{w_1}|X_{w_2}) = \sum_{u\in(0,1)}\lbrace p(X_{w_2}=u)\cdot H(X_{w_1}|X_{w_2}=u)\rbrace \\]
\\[ = \sum_{u\in(0,1)}\lbrace p(X_{w_2}=u)\cdot [\sum_{v\in(0,1)} -p(X_{w_1}=v|X_{w_2=u})\cdot\log_2[p(X_{w_1}=v|X_{w_2=u})]] \rbrace \\]

If a pairs of words have low conditional entropy, the knowledge of one increases our ability to predict the other, and hence the words may have a semantic relation.  

The issue brought up is that conditional entropies cannot be compared unless we are looking at the same root word, i.e.

\\( H(X_{w_1}|X_{w_2}) \\)
and 
\\( H(X_{w_1}|X_{w_3}) \\)
are comparable; 
\\( H(X_{w_1}|X_{w_2}) \\)
and 
\\( H(X_{w_2}|X_{w_3}) \\)
are not.

This is where the idea of Mutual Information is introduced, which measures the reduction of entropy of the root word with knowledge of some second term. 
\\[I(X_{w_1};X_{w_2})= H(X_{w_1}) - H(X_{w_1}|X_{w_2})\\]

Mutual Information (MI) is symmetric, and can be compared across different term pairs to determine stronger semantic/syntagmatic relations. MI can also be written in term of KL-divergence:

\\[ I(X_{w_1};X_{w_2}) = \sum_{u\in(0,1)}\sum_{v\in(0,1)} p(X_{w_1}=v,X_{w_2}=u) \cdot
\log_2 \frac{p(X_{w_1}=v,X_{w_2}=u)}{p(X_{w_1}=v)p(X_{w_2}=u)}
\\]

The ratio in this expression of MI is of the _observed joint distribution_ of the two words, to the _expected distribution_ of the two words _if they were independant_.
