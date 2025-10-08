## Term Frequency - Inverse Document Frequency
Recall how we do basic text classification:
What if the text we have has stop words: "the, and, it, are"
We do not want these words. We can either drop them or *penalize* the frequency of these words: 
$$\text{tf-idf} = tf * idf$$
We want to compute: 
$$tf = \frac{\text{number of times wt present in doc d}}{\text{terms in doc d}}$$
Suppose we have document d = 1000 terms
"cat" = 3 times in document d
"the" = 20 times in document d
`"cat" = 3 / 1000` and `"the" = 20 / 1000`

$$idf = \frac{\log\text{number of docs in corpus}}{\text{number of docs in corpus containing wt}}$$
How many documents in that corpus of documents contain the word "cat"?
How many documents in that corpus of documents contain the word "the"?

