## Document Processing with GPT and LangChain 

In this project, I aim to deepen my understanding of GPT and LangChain by building a program that accesses and processes documents stored in a folder on my laptop. This program will be able to retrieve information from these documents to fulfill user requests, providing hands-on experience with both GPT and LangChain.

Below, I’ll document key learning points from this project, which may be helpful for casual readers interested in exploring similar topics.

### Purpose of Langchain

* LangChain simplifies working with AI models by addressing two key aspects:

   * **Data-aware** - It enables your LLMs to access and utilize external data, such as files, APIs, and other applications.
   * **Agentic** - It empowers your LLMs to interact with their environment and make decisions about the next steps to take, allowing for dynamic decision-making.

LangChain helps you combine complex components into a structured workflow. Instead of manually managing embeddings, vector stores, and search processes, LangChain provides tools to set up and manage each step in a way that feels more intuitive.

### Neural Networks and ChatGPT 

GPT is a neural network—more specifically, it's a Transformer-based neural network. Here’s a breakdown of what that means and how it works in the context of natural language processing (NLP).

#### What is a Neural Network?
A neural network is a series of algorithms that mimic the human brain's way of learning and processing information. In simple terms, it’s a set of interconnected layers of "neurons" (nodes) that process data and learn patterns by adjusting the "weights" of these connections based on feedback. Neural networks are particularly useful in tasks where identifying complex patterns in data is essential, like image recognition or natural language understanding.

Here's a [video](https://www.youtube.com/watch?v=aircAruvnKk) from 3Blue1Brown that gives a good overview of neural networks. 

#### GPT as a Transformer Neural Network
GPT (Generative Pre-trained Transformer) is a specific type of neural network architecture called a Transformer. This architecture is particularly suited for sequence data, like text, where the order of elements matters.

* Key Features of the Transformer Architecture: 
   * Self-Attention: The most important feature of the Transformer architecture is its self-attention mechanism. Self-attention allows the model to "pay attention" to different parts of a sentence, even if the words are far apart. For example, in the sentence "The cat, which had been hiding under the bed, finally came out," the Transformer can understand that "cat" is connected to "came out" despite the distance between them in the text.
   * Positional Encoding: Since Transformers process all words in a sentence at once, they need a way to understand the order of words. Positional encodings are added to each word's embedding to give it a sense of position in the sentence.
   *Layers of Processing: Transformers are built with multiple layers of these self-attention and feed-forward neural network blocks. Each layer refines the representation of the text, capturing increasingly abstract patterns as you go deeper in the model.

#### How GPT Uses This Architecture
GPT is based on the Transformer architecture but is trained in a way that’s optimized for generating human-like text. Here’s a high-level look at how it works:

* Pre-training: GPT is trained on massive amounts of text data from the internet. During pre-training, it learns the general structure of language, grammar, facts about the world, and some reasoning abilities. This is an unsupervised phase, where it predicts the next word in a sentence over and over, learning patterns in language along the way.

* Fine-tuning (Optional): Sometimes, GPT is fine-tuned on specific types of text or with specific instructions to make it better at tasks like answering questions, generating code, or summarizing text. This step can be supervised, where the model learns from examples that show the correct behavior.

* Generation: When you interact with GPT, you provide a prompt (like a question or sentence), and the model generates a continuation by predicting one word at a time. Each word generated is based on both the input prompt and the previous words it has generated.

![Basic Structure](./Structure_basic.png)

### Processing and loading Documents into Vector Store 

Steps in processing document: 

1. Loading and Splitting Documents

* The process begins with document files (like PDFs)
* Neural networks perform optimally with smaller segments of text, so we will split these files into manageable chunks (similar to tokenization)

2. Preprocessing and embedding creation

* Each chunk of text is preprocessed (cleaned and prepared in a way the AI model can understand)
* Then, each chunk is fed into OpenAI’s embedding model (or another embedding model), which transforms the text into a numerical format, called an embedding. This embedding is a mathematical representation of the text’s meaning, capturing its semantic (meaning-based) information.

3. Storing Embeddings in a Vector Store

* Once the text chunks are embedded, these embeddings are stored in a vector store (like Pinecone or FAISS).
* The vector store is crucial because it allows for fast retrieval of embeddings based on their similarity. Essentially, it can find related or similar embeddings to a given query, which is helpful for locating relevant document chunks when a user asks a question.

Think of the vector store as a specialized database optimized to quickly find "semantically similar" embeddings. This means it’s able to find parts of documents that are similar in meaning to the user's query, even if they use different words.

### Using User Queries to Search and Retrieve Answers

1. Converting the User Query into an Embedding

* When a user asks a question, that question is converted into an embedding as well, using the same model (like OpenAI).
* This query embedding captures the meaning of the user’s question.

2. Semantic Search

* The query embedding is then sent to the vector store.
* Using a technique called semantic search, the vector store compares the query embedding to the document embeddings it has stored and retrieves the most relevant chunks. This allows the system to locate pieces of text that are most likely to answer the question.

3. Ranking and Answer Generation

* The retrieved chunks are ranked based on their relevance to the query.
* These top-ranked results are then sent to the Language Model (LLM) (like GPT) to generate an answer. The LLM can use these document chunks to craft a detailed, contextually accurate response for the user.

4. Delivering the Answer

Finally, the system sends the generated answer back to the user.

### Why Each Part Matters
* Embeddings: These are the foundation, as they capture the "meaning" of each text chunk in a way that allows for effective comparisons. Think of embeddings as a way of turning words into "coordinates" in a high-dimensional space, where similar meanings are close to each other.

* Vector Store: This component lets the system quickly search through massive amounts of text to find relevant information without having to search word-by-word. Instead, it searches based on meaning.

* LLM (Language Model): Once the relevant chunks are identified, the language model uses this information to form a coherent answer that feels natural and relevant.


