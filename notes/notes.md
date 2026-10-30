# Building a LLM from scratch : Sebastian Raschka

## 0. Introduction
- A foundation model is a model that is trained on a large amount of data and it performs reasonably well on various different tasks but it isn't specialized for a particular application. We can perform fine-tuning on this model, thus, giving it "expertise" in a particular task, where it can perform exceptionally well, i.e., classification, chatbot, etc.

## 1. Understanding LLMs
- An LLM is a neural network designed to understand, generate and respond to human-like text. These NN are trained on large amount of text data.
- The parameters of these models are optimized to predict the next word in the sequence, which exploits the inherent sequential nature of language to understand the context, structure and relationship within text.
- LLMs use the transformer architecture which allows them to pay attention to various parts of the sentence to predict the next word. This ability to pay attention enables transformers to handle nuances and complexities embedded within human language.
- Pretraining an LLM means training the model on a large, diverse and general dataset to develop a broad understanding of language, which makes the LLM foundational. After pretraining, the model can be trained on a narrower dataset for a particular task, which is called fine-tuning. This approach made up of pretraining and fine-tuning is shown below:

![alt text](image.png)

- A pretrained LLM (foundation model) can have few-shot capabilities, which means it can perform new tasks based on only a few examples, instead of needing extensive training data.
- The pretraining is done in a self-supervised manner, where the model learns to predict the next word. When we want a specific objective, we can fine-tune the model, which means training it on labeled data, specific to the objective.
- Two most popular fine tuning categories are instruction and classification. 
- In instruction fine tuning, the labeled dataset contains instruction and answer pairs, eg., a query to translate a text and the correctly translated text.
- In classification fine tuning, the labeled dataset contains texts and associated class labels, eg., an email and a spam label.
- At the heart of an LLM sits the transformer architecture, which is shown below:

![alt text](image-1.png)

- The transformer consists of two integral parts, an encoder and a decoder.
- The encoder converts the input information into a numerical representations or vectors that contain the contextual information of the input.
- The decoder takes the vectors and coverts them back to text.
- For example, in a translation task, the encoder can convert english text into a latent representation (aka vector) and the decoder can decode these vectors to generate text in german.
- Both the encoder and decoder contains many layers connected by an attention mechanism. The self-attention mechanism allows the model to rank the importance of different words (aka tokens) in a sequence to each other. This mechanism enables the model to capture long-range dependencies and contextual relationships in the input data, enhancing the model's capability to generate coherent and contextually relevant output.
- **NOTE:** GPT like models are great at zero-shot and few-shot learning tasks. Zero-shot learning refers to the ability to generalize to completely unseen tasks without any prior training, while, few-shot learning refers to the ability to learn from a small examples.

![alt text](image-2.png)

- GPT like models use only he decoder to generate text by predicting one word at a time, and are called auto-regressive. An autoregressive model incorporate its previous outputs as inputs for the next prediction. This auto-regressive nature improves the coherence of the resulting text. This property is shown in the following image:

![alt text](image-3.png)

- **NOTE:** GPT like models consisting of only the decoder block were aimed at next word prediction, can perform translation as well which wasn't the intended outcome. This ability to perform task that the model wasn't trained for is called an emergent behavior which is a consequence of the fact that it had exposure to vast multilingual data in diverse contexts. The model learns the translation patterns between languages and can perform translation. This means, that we can perform a variety of tasks with a single model instead of training one model for each task.
- The LLM can be built in three stages: 

![alt text](image-4.png)

## 2. Working with text data
- Now we will see how to prepare input text for training LLMs. This includes splitting the text into individual word/subword tokens which can be converted into vector representations. We'll see advanced tokenization techniques, like, BPE which is used in GPT.
- Text is categorical, which means it is qualitative in nature, representing properties which can't be quantified or turned into "numbers", thus, mathematics can't be performed on them. NNs requires numbers to work on them, thus, we transform raw text into continuous valued vectors, on which LLMs can work their magic.
- The concept of turning categorical data into vectors is called embeddings. We can embed different types of data (audio, video, text, etc.) using a NN layer to another pretrained NN.

![alt text](image-5.png)

- Embedding is a mapping from discrete objects (words, images) to points in a continuous vector space. Thus, converting nonnumeric data into a format that the NNs can process.
- Many algorithms exist for generating word embeddings, with Word2Vec being the most famous. The main idea behind it is that words that appead in similar contexts tend to have similar meanings. When seen in a 2D projection, these words exist close to each other.

![alt text](image-6.png)

- We can either use a pretrained network to produce embeddings or have the embedding generation as a part of the input layer, which is updated during training. The benefit of using it as a part of the LLM is that the embeddings are optimized for the specific task we're doing.
- The embedding space is the vector-space where the word embeddings live. It is usually a very high dimensional space, where each coordinate of the embedding represents a certain feature/property (abstract semantic properties) of the corresponding word. Higher the dimension, richer the embedding is, albeit leading to higher computing costs and this dimension scales with the model depth.
- The process of generating embeddings includes: splitting text into words, turning words into tokens (which could be individual words/subwords/punctuation marks/special characters) and turning tokens into embedding vectors.

![alt text](image-7.png)

- We will be tokenizing the short story "The Verdict" present in [the-verdict.txt](../notebooks/ch2tokenization/the-verdict.txt) into individual words and special characters.
- We perform an illustrative [splitting](../notebooks/ch2tokenization/02_text_tokenization.ipynb) using the python library re (regular expression), later we will use pre-built tokenizers.