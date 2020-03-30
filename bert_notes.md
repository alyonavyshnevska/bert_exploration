# Bert notes

### Background 
2018 was a breakthrough year in NLP. Transfer learning, particularly models like Allen AI’s ELMO, OpenAI’s Open-GPT, and Google’s BERT allowed researchers to beat NLP benchmarks with minimal task-specific fine-tuning.  The pretrained could easily (with less data and less compute time) be fine-tuned and implemented to produce state of the art results. 

NLP models such as LSTMs or CNNs require inputs in the form of numerical vectors, and this typically means translating features like the vocabulary and parts of speech into numerical representations

In the past, words have been represented either as uniquely indexed values (one-hot encoding), or more as neural word embeddings where vocabulary words are matched against the fixed-length feature embeddings that result from models like Word2Vec or Fasttext. 

BERT produces 'context-informed' word representations: represenattions that are dynamically informed by the words around them.


### What is BERT? 

Bidirectional Encoder Representations from Transformers (BERT) was released in late 2018 by Google. BERT can be used to extract high quality language features, namely word and sentence embedding vectors from text data. The pretrained model can also be fine-tuned on a specific task (classification, entity recognition, question answering, etc.) with new data to produce state of the art predictions. 


### Applications of BERT

What can we do with these word and sentence embedding vectors? 

1. The embeddings are useful for keyword/search expansion, semantic search and information retrieval
    - e.g.: match customer searches against already answered searches: BERT representations accurately retrieve results matching the customer’s intent and contextual meaning, even if there’s no keyword or phrase overlap.

    
2. The embedding vectors are used as high-quality feature inputs to downstream models. 


### Advantage of BERT over Word2Vec-like models

BERT offers an advantage over models like Word2Vec, because while each word has a fixed representation under Word2Vec regardless of the context within which the word appears, BERT produces word representations that are dynamically informed by the words around them. 

For example, given two sentences, where the word bank is polysemous. 

- “The man was accused of robbing a bank.”  
- “The man went fishing by the bank of the river.”

Word2Vec and similar models produce the same word embedding for the word “bank” in both sentences. 
BERT produces different word embeddings for “bank” for each sentence.

Aside from a solution for polysemy, the context-informed word embeddings capture further syntanctic and semantic features of words or sentences.

### Implementation 

Hugging Face has a pytorch interface for BERT

### Input

BERT expects input data in a specific format: 

1. special tokens to mark the beginning ([CLS]) and separation/end of sentences ([SEP])
2. tokens that conform with the fixed vocabulary used in BERT
3. token IDs from BERT’s tokenizer
4. mask IDs to indicate which elements in the sequence are tokens and which are padding elements
5. segment IDs used to distinguish different sentences
6. positional embeddings used to show token position within the sequence

The HuggigFace interface takes care of some of these input specifications for us.   
Bert tokenizer tokenised sentences. 

#### WordPiece Model

The word "embedding" becomes  `['em', '##bed', '##ding', '##s']`.

The two hash signs preceding some of these subwords are the tokenizer’s way to denote that this subword or character is part of a larger word and preceded by another subword. So, for example, the `‘##bed’` token is separate from the `‘bed’` token; the first is used whenever the subword ‘bed’ occurs within a larger word and the second is used explicitly for when the standalone token ‘thing you sleep on’ occurs.


Vocabulary limit size of the BERT tokenizer model is 30,000.
The WordPiece model generated a vocabulary that contains all English characters plus the most common words and subwords found in the English language corpus the model is trained on. First, the tokenizer checks if the whole word is in vocal. If not, then checks for subwords. At he very least, the word is represented as a collecti0n of tokens.

- Whole words 
- Subwords occurring at the beginning of a word or in isolation (“em” as in “embeddings” is assigned the same vector as the standalone sequence of characters “em” as in “go get em” )
- Subwords not at the beginning of a word, which are preceded by ‘##’ to denote this case
- Individual characters

### Command-line Tool to get Bert embeddings
Mapping a variable-length sentence to a fixed-length vector using BERT model [Link](https://github.com/hanxiao/bert-as-service)



# SpanBERT

# RoBERTa
