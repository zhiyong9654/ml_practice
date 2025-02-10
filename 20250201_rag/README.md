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
```

# 03
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_5_to_9.ipynb
## quick notes 
1. RAG fusion depends on the rank ordering of the documents. But the retriever doesn't have clear documentation to explain whether is it ranked most relevant to least. I would assume so, and through testing, I can see this is the case, but remember to check this.


# 04
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_5_to_9.ipynb
## quick notes 
1. Decomposition makes sense to me, to decompose the question into subquestions, then iterative answer each subquestion to build context. But in the example in the video, they answer each subquestion, but don't do a final loop to answer the original question. Quite strange to me to not answer the original question, so i implemented that instead.
1. Used a more modern approach of structured outputs to guarantee the output questions.

# 05
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_5_to_9.ipynb
## quick notes 
1. In this notebook, i felt there were many unneeded abstractions used in langchain (do i really need a function to help me structure few shot prompting?) Replaced with much more readable and easy to maintain stuff where appropriate.
1. Learnt about the difference between ChatPromptTemplate.from_template) and ChatPromptTemplate.from_messages().
    1. from_template is just basically f-string replacement
    1. from_messages is a more configurable version, where we can dictate 'system', 'user', 'ai'
1. When using LLM models and all these different prompt abstractions, remember to use the specific models role and proper prompt templates. Don't just copy the prompt_template script blindly. E.g. llama3.2 uses system/user/assistant, not system/user/ai.

# 06
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_5_to_9.ipynb
## quick notes 
1. HyDE as a concept seems really interesting to me. I think in real world applications, I would like to benchmark the similarity scores of the documents retrieved by HyDE vs retrieved by non-hyde. Can probably do an average of similarity scores as a metric in real world.

# 07
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_10_and_11.ipynb
## quick notes 
1. Idea is quite simple, use an LLM to decide what DB to use for retrieval. Use an LLM to decide what prompts to use. No issues.

# 08
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_10_and_11.ipynb
## quick notes 
1. [Remember to pass pydantic definition into the prompt!] I was wondering, when we use pydantic models to constrain the LLM output. I know that we constrain the probabilities for LLM output to be bias to follow our schema, but I wasn't sure if our pydantic model definition is given to the LLM in the prompt. Looking through the debug for langchain, it doesn't seem like the pydantic model definition is passed into the prompt, hence I observed better performance if i specified in the prompt, what's the expected pydantic output model that i wanted.

# 09
## Link
https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_10_and_11.ipynb
## quick notes 
1. I think this method addresses one of the issues i had with vanilla rag and the chunking of docs, in that the retrieved documents are disjointed and don't follow a coherent flow, which may be confusing to the LLM. This method, which has an LLM summarize the doc, and stores the summarized embeddings, but retrieves the full doc, helps with this perfectly, in making sure we retrieve the full docs, without worrying about chunking making the docs unreliable/disjointed. But this methods relies on your LLM having a long context length.
1. This notebook also shows that we are able to use MultiVectorRetriever, to retrieve paired items (in this case vector, document, id)
