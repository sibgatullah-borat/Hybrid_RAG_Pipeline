# Hybrid_RAG_Pipeline
This is a demo code to build a hybrid RAG pipeline that demonstrate proficiency in advanced LLM architecture and performance optimization.
How the Code Works (Architecture Summary)

The hybrid_rag_pipeline executes a four-stage process to ensure optimal context delivery to the Large Language Model:

Parallel Retrieval (Maximizing Speed):

The system uses Python's asyncio.gather to concurrently execute two distinct search methods:

Dense Retrieval: Finds documents based on semantic meaning using vector embeddings.

Sparse Retrieval: Finds documents based on exact keyword matches (simulated BM25).

Goal: Drastically reduce total retrieval time and maximizes the initial pool of relevant documents (Recall).

Merge & Deduplication:

The results from the two parallel retrievers are combined into a single, deduplicated list. This ensures the system captures documents missed by one method but found by the other.

Cross-Encoder Rerank (Maximizing Precision):

A dedicated, high-fidelity Cross-Encoder Model (a powerful, small transformer) is used to re-score the merged documents based on their true relevance to the query.

Goal: Filters out noisy, low-relevance results, ensuring the LLM receives only the most accurate context (Precision).

LLM Generation with Streaming (Optimizing UX):

The final, high-quality context is fed into the Gemini LLM. The answer is then delivered to the user using a streaming interface, ensuring that the output starts appearing immediately, significantly reducing perceived latency.
