**Developments over time in NLP**
- Language translation 
- Free-text questio answering and text generation 
- GPT-2 (2019) early stepping towards foundation models 
- GPT-4 (2023)
- Today, Ai is very powerful in generating images, videos, and multitasking, but still has many visible problems. 

**Long-term Goal**
- Non-recurrent seq2seq(encoder-decoder) model. 
- Multi-layered attention model that enables lateral information transfer acros an input sequence. 
- Cost function is cross-entropy erorr of decoder. 
- Original model of BERT.

**How do we represent the meaning of a word?**
*meaning*:
- idea represented by a word, phrase, etc. 
- idea that a person wants to express by using words, signs, etc. 
- idea that is expressed in work of writing, art, etc.
Linguistic way of thinking of meaning:
	Signifier(symbol) <=> signified (idea or thing)
![[Pasted image 20260423200003.png]]

**Problems with WordNet**
It cannot capture the complexity of meanings. 
- Eg. the meaning of "proficient" is often listed as a synonym for "good," which is not always suitable for some contexts.
- WordNet is missing the context, only going word by word. 
- A word by itself can have a different meaning even without context! We cannot just connect one word to another singular word. 

**Representing words as discrete symbols**
![[Pasted image 20260423200235.png]]
How do we represent a word in a computer when the computer can only understand binary numbers? 
**Problem**: what if we wanted to search documents containing "hotel" and "motel"?
But, the two vectors above are orthogonal. There is no natural notion of similarity for one-hot-encoded vectors!

**Representing words by their context**
**Distributional Semantics** - a word's meaning is given by the words that frequently appear close-by. "You shall know a word by the company it keeps." One of the most successful ideas of modern statistical NLP.

When a word `w` appears in a text, its context is the set of words that appear nearby (within a fixed-size window).
We use the contexts of `w` to build up a representation of `w`. 
![[Pasted image 20260423200650.png]]

**Word Vectors**
We build a dense vector for each word, chosen so that it is similar to vectors of words that appear in similar contexts, measuring similarity as the vector *dot* (scalar) product. 
![[Pasted image 20260423200846.png]]
Note: word vectors are also called (word) embeddings or (neural) word representations. They are a distributed representation. 

![[Pasted image 20260423201044.png|298]]

## Word2Vec Overview 
Framework for learning word vectors. 
Idea:
- We have a large corpus ()"body") of text: long list of words. 
- Every word in a fixed vocabulary is represented by a vector. 
- Go through each position `t` in the text, which has a center word `c` and context ("outside") words `o`. 
- Use the *similarity of the word vectors* for `c` and`o` to calculate the probability of `o` given `c` (or vice versa)
- Keep adjusting the word vectors to maximize this probability.

**Word2Vec: Overview**
Why do we think this process is recursive? 
A word can repeat in our corpus. ****
![[Pasted image 20260423201518.png|533]]
![[Pasted image 20260423201541.png|533]]

**Word2Vec: Objective Function**
For each position `t= 1, ... T`, predict context words within a window of fixed size `m`, given center word `w_t`. Data likelihood:
![[Pasted image 20260423201724.png|641]]
![[Pasted image 20260423202046.png|642]]
Remember, we are trying to predict the outsiders `o` based on the center word `c`. This representation can be confusing, but this is the comon practice within NLP. 

**Word2Vec: Prediction Function**
![[Pasted image 20260423202121.png]]

**To train the model, Optimize values of parameters to minimize loss**
Gradually adjust parameters to minimize a loss:
- Recall: `theta` represents all the model parmeters, in one long vector. 
- In our case, with d-dimensional vectors and V-many words, we have --> 
![[Pasted image 20260423202726.png]]
- Remember every word has two vectors. 

We optimize these parameters by walking down the gradient (see right figure)
We compute all vector gradients. 

**Optimization: Gradient Descent**
- We have a cost function J(`theta`) we want to minimize. 
- **Gradient Descent** is an algorithm to minimize J(`theta`)
- Idea: for current value of `theta`, calculate gradient of J(`theta`), then take small step in function of negative gradient.
- Repeat. 
![[Pasted image 20260423202925.png]]
Problem: J(`theta`) is the function of all windows in the corpus (potentially billions)
This is very expensive to compute, so instead we want to use **Stochastic Gradient Descent**, so we can repeatedly sample batches of windows, and update after each one. 

**Review: Main Idea of Word2Vec**
- Start with random word vectors
- Iterate through each word position in the whole corpus. 
- Try to predict surrounding words using word vectors
- **Learning**: update vectors so they can predict actual surrounding words better. 
- Doing no more than this, this algorithm learns word vectors that capture well word similarity and meaningful directions in a word space. 

**Word2Vec Algorithm Family**
Why two vectors? Easier optimization, average both at the end. 
	- But can implement the algorithm with just one vector per word... and it helps a bit. 
![[Pasted image 20260423203828.png|581]]

**Skip-gram model with negative sampling**
![[Pasted image 20260423203900.png]]
As we see in the denominator, we are not using everything in the corpus, but we are bounded by the windows. 
![[Pasted image 20260423203949.png]]

Why is it that when we make computations, we only go with the probability? Why do we not just accumulate all the statistics of what words appear near each other? 

It is better to use the iterative process because every single word's meaning is defined by its neighbors. We are therefore trying to adapt the meaning of all the words with respect to all of them together. That's why we cannot just count. 

Building a co-occurrence matrix of `X`.
- 2 options: windows vs. full document
- Window: Similar to word2vec, use windows around each word --> captures some syntactic and semantic information (word space)
- Word-document co-occurrence matrix will give general topics (all sports terms will have similar entries), leading to *Latent Semantic Analysis* (document space)

