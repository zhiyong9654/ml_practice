https://www.youtube.com/watch?v=sVcwVQRHIc8

# 01
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_1_to_4.ipynb
## quick notes 
No issues with this notebook. Pretty straightforward.

# 02 
## Link 
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_5_to_9.ipynb
## quick notes
1. For multiquery, i think a better way to generate_queries is to use structured response, instead of blindly doing a new line split of the return from LLM. Doing it without structured response has the following issues:
    1. Brittle, because you cannot guarantee LLM output, as LLM may spit out non-newline delimited responses.
    1. Irrelevant text being sent to retriever. E.g. My LLM responded with the below. Splitting it naively by newline causes the first line and last line, which are irrelevant to the question to be sent to retriever, which has confounding effects."
1. There seems to be a new function built into langchain that supports it directly. See MultiQueryRetriever.
1. I had a small misconception, for multiquery, remember that multiquery only alters the prompt for retrieval. The prompt for generation remains unchanged.
```python
"""Here are five alternative versions of the original question to retrieve relevant documents from a vector database:

1. Can you explain the concept of task decomposition in large language model (LLM) agents and its applications?
2. How does task decomposition work in LLMs, and what benefits does it bring to these models?
3. What is the role of task decomposition in improving the performance of LLM agents on complex tasks?
4. Can you provide an overview of the different approaches to task decomposition for LLM agents, including their strengths and weaknesses?
5. How can task decomposition be used to enhance the flexibility and adaptability of LLM agents in various domains?

These alternative questions cover different aspects of the original question, such as explaining the concept, understanding its applications, and exploring its benefits and limitations. By asking these questions, you can retrieve a broader range of relevant documents from the vector database."""

# 03
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_5_to_9.ipynb
## quick notes 
1. RAG fusion depends on the rank ordering of the documents. But the retriever doesn't have clear documentation to explain whether is it ranked most relevant to least. I would assume so, and through testing, I can see this is the case, but remember to check this.
