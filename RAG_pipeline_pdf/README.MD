## Introduction: Project objective and relevance of RAG

To showcase the RAG AI framework to improve LLM accuracy in a single agent solution that creates in memory vector stores from an open source embedding model on user provided document(s). Key benefits of RAG include but are not limited to reducing hallucinations and augmented responses from LLMs by combining privately sourced data and hence avoiding expensive model retraining.

In this specific example, we provide 2 pdf documents which explain Data Monetization capabilities within an organization i.e. to create value capture from enterprise data and list its benefits plus various channels and mechanisms around monetization efforts.

## Implementation overview: Summary of the pipeline and tools used

At a high level , the workflow follows a 3 step process - Document chunking , embedding and Vector search.

After installing and importing all of the Langchain dependencies(language model integration) providing pdf loading, splitting , chunking and retrieval operations.

An azure openAI key is initialized to be used for the embedding model for preparing the vector datastore in memory using FAISS which keeps its entire vector index loaded in RAM for fast similarity searches in real time AI applications hence serving as core retrieval engine though not a memory system of its own . The vector store is prepared using FAISS from the embeddings and pdfs.

Next comes the llm declaration using azure openai end point with the model as gpt-5-mini and furthermore a RAG chain is declared leveraging the llm and the vectorstore as retriever.

Upon a quick test on the retrieval by similarity search found to be working , a utility function is created to aid the response to be in a clear text void of any new lines etc for a clean output.

A couple of sample questions are asked to ensure that the result from the single agent system matches the content in the provided pdf and it is grounded in the retrieved source.

## Metrics: Total chunks, average chunk size, and a sample query output

Total relevant chunks retrieved: 12
Average chunk size: 448.50 characters (49.42 words)

The recursive character splitter was initialized with a desired chunk size of 500 which is taken as a max limit however the splitter prioritizes the semantic coherence by splitting at natural breaks such as new line or paras etc . Hence, for better context preservation, the splitter kept the average size at 448.5 which is very close to the expected value causing some necessary overlaps.

## Conclusion: Insights gained, issues faced, and possible improvements

Before querying the vector store with a few queries , first the embedding space inside the FAISS vector store is checked for semantic similarity (vectorstrore.similarity_search) by providing a simple query to check for factual correctness of the relevant content . which prints the documents and the content snippet that is matched against the retrieved document .

### Issues faced -

When provided with a prompt like - “What examples are existing in the RAG store with respect to Data monetization?”

the model tried to be extra helpful by taking the literal meaning of the RAG store as an external entity and returned a response like

Result1 :I don’t have access to your RAG store, so I can’t list the exact items it contains. Below I’ll instead (A) define practical data categories by their transformational value, and (B) give concrete examples you would commonly see in a RAG/store context mapped to direct and indirect data-monetization approaches. If you want, I can then help you scan or map your actual RAG store items against these categories — tell me how you can share the inventory.

This indicates that the LLM did use the knowledge base while answering but again proves the fact that adversarial inputs pushes the agent to the point of hallucinations. Hence, it is imperative to give structured, clear and unambiguous queries for RAG based fetched results.

For the other queries, the agent responded well with sources quoted directly from the uploaded pdfs and hence from the vector store as provided in the notebook responses.
