## Term Frequency - Inverse Document Frequency
Recall how we do basic text classification:
What if the text we have has stop words: "the, and, it, are"
We do not want these words. We can either drop them or *penalize* the frequency of these words: 
$$\text{tf-idf} = tf * idf$$
We want to compute: 
$$tf = \frac{\text{number of times} \space w_{t} \space \text{present in doc d}}{\text{number of terms in doc d}}$$
Suppose we have document d = 1000 terms
"cat" = 3 times in document d
"the" = 20 times in document d
Corpus = 100,000 documents
`"cat" = 3 / 1000` and `"the" = 20 / 1000`

$$idf = \frac{\log\text{number of docs in corpus}}{\text{number of docs in corpus containing} \space w_{t}}$$
How many documents in that corpus of documents contain the word "cat"?
How many documents in that corpus of documents contain the word "the"?
Usually the logarithm is of base 10.

Let us assume a corpus of 100 documents. What would be the tf-idf("cat")?
Using the above values: 
$$tf-idf(\text{cat}) = \frac{3}{1000} * \log \frac{10^5}{10^3 +1} = 2$$
$$tf-idf(\text{the}) = \frac{20}{1000} * \log \frac{10^5}{10^5 + 1} = -0.3$$
The intuition is that the `idf` term is *penalizing* the term frequency. The value for "cat" will be much larger because it is not so frequent, but since the value for "the" is basically in event document d, it will penalize the frequency.

Very frequent occurrences of a given term will not have heavy weight in the classification. 

[Sentiment Analysis using  TF-IDF in Scikit Learn](https://gist.github.com/eitellauria/66a0c58835943cfe259991c29b49e179)



