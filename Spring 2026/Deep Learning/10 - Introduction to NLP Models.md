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
**Problem**: what if we wanted to search a document 