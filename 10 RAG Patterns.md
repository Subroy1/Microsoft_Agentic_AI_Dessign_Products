# 10 RAG Patterns

| Architecture                                | Core Idea                                                                                        | Strengths                                            |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **Simple RAG**                              | Retrieve top-k documents from a vector DB and feed them directly to the LLM.                     | Easy to implement, fast, widely supported.           |
| **RAG with Memory**                         | Adds memory (short-term or long-term) to persist dialogue context or user history.               | Natural multi-turn conversations, better continuity. |
| **Branched RAG**                            | Retrieves from multiple sources (semantic, keyword, structured DBs), then merges.                | Better recall, robust against retrieval gaps.        |
| **HyDE (Hypothetical Document Embeddings)** | Generates a hypothetical document/query expansion before retrieval.                              | Boosts recall when queries are vague or sparse.      |
| **Adaptive RAG**                            | Dynamically chooses retrieval strategies (e.g., dense vs. sparse, multi-hop) based on the query. | Flexible, context-sensitive retrieval, better efficiency. |
| **Corrective RAG**                          | LLM critiques retrieval results and corrects errors before generation.                           | Improves factuality, reduces irrelevant/incorrect content. |
| **Self-RAG**                                | Model self-checks retrieved passages (critic + generator loop).                                  | Improves reliability, reduces hallucinations.        |
| **Agentic RAG**                             | Retrieval is embedded in a multi-agent workflow (planner, retriever, generator, critic).         | Strong reasoning, task decomposition, autonomous workflows. |
| **Multimodal RAG**                          | Retrieves from multimodal stores (text, image, video, audio, code).                              | Enables cross-modal reasoning, richer context.       |

> Source: Converted from file `10 RAG Patterns` in the repository.


<img width="1729" height="946" alt="image" src="https://github.com/user-attachments/assets/43faf18a-9e3c-4edb-84ad-ee144f744a22" />
