# rag_one
This repository is about building a raw RAG  solution with Python + AWS Bedrock [Meta Llama 3 70B] + AWS Open search.

What is RAG? RAG stands for Retrieval-Augmented Generation. It is the process of optimizing the output response of the large language model by referring to the authoritative knowledge base outside of its training data sources before generating a response. In other words, LLM generates a response by using its capability of answering the queries, but based on the information retrieved from this knowledge base instead of using its own trained knowledge to answer the query.

![image](https://github.com/user-attachments/assets/1e2df742-acf0-49b9-aaef-458839009ef4)
Thanks to AWS: AWS RAG Image
The following diagram shows the conceptual flow of using RAG with LLMs.

Steps of building RAG:
1. You should have this Authoritative Knowledge Base from where you want your LLM to refer before generating a response for the query. This depends upon your use case for the RAG, let's say you are building an RAG Chatbot that will answer Insurance queries OR health-related queries 
OR it can be specific to an organization and able to answer queries related to the organization, for these cases the Knowledge Base must be related to these domains.

2. When a user raises a query or we can say, we prompt the RAG Chatbot, this query will be passed to the Knowledge Base to find the most relevant information related to it and this information will be passed to the LLM to frame the answer for the query/prompt.

The key consideration here is how we store this dedicated information, or the knowledge base. It should be stored in a way that is compatible with the LLM approach.

For this to be understood, we should first understand how search works...

1. **Lexical Search:** Lexical search for unstructured text works directly with language by decomposing blocks of the text into words and matching those words to text from a query. It involves various steps to process the query text:
  MATCHING:
    Segmenting: When the engine segments terms, it removes punctuation and lowercases terms, so that Run. matches run.
    Stemming: Language-specific stemming rules remove common inflections; this means Run matched run,runs and running.
    Stop-word filtering: A stop-word filter removes common terms like articles: a, an, the and the like. These terms appear in almost every document so they have low value for matching.
    Synonym matching: Finally, it adds synonyms so that terms can match across common groupings. For example, the engine might use begin and initiate as synonyms for start.

   MERGING:
    If the application wants to match all terms in the query, it will use an AND operator for the query. In most cases, the application will use an OR operator.

   RANKING:
     The final phase of the search is ranking. A search engine for lexical search employs a ranking algorithm called TERM FREQUENCY INVERSE DOCUMENT FREQUENCY [TF-IDF].

     In this, Rare Terms get high scores, and common terms get low scores. A document's score for a particular query is the sum of the scores for the terms that match, multiplied by the number
      times they occur. During the ranking phase, the engine sorts all matching documents by score to produce a final search result.

Lexical search is about extracting as much meaning as possible from raw words to match and rank them by intent and meaning, but Lexical search will not help in context matching, which is needed to get good results in terms of LLMs and the RAGs, for this we need context matching approaches, this we will achive via SEMANTIC vertor based search.

**2. Vectors: Representing Semantic Information:**

