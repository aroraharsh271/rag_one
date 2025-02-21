# rag_one
This repository is about building a raw RAG  solution with Python + AWS Bedrock [Meta Llama 3 70B] + AWS Open search.

What is RAG? RAG stands for Retrieval-Augmented Generation. It is the process of optimizing the output response of the large language model by referring to the authoritative knowledge base outside of its training data sources before generating a response. In other words, LLM generates a response by using its capability of answering the queries, but based on the information retrieved from this knowledge base instead of using its own trained knowledge to answer the query.

![image](https://github.com/user-attachments/assets/1e2df742-acf0-49b9-aaef-458839009ef4)
Thanks to AWS: AWS RAG Image
The following diagram shows the conceptual flow of using RAG with LLMs.

Steps of building RAG:
1. You should have this Authoritative Knowledge Base from where you want your LLM to refer before generating a response for the query. This depends upon your use case for the RAG, let's say you are building an RAG Chatbot that will answer Insurance queries OR Health related queries 
OR it can be specific to an organization and able to answer queries related to the organization, for these cases the Knowledge Base must be related to these domains.

2. When a user raises a query or we can say, we prompt the RAG Chatbot, this query will be passed to the Knowledge Base to find the most relevant information related to it and this information will be passed to the LLM to frame the answer for the query/prompt.

The key consideration here is the way we store this dedicated information or we can say the knowledge base, it should be stored in a way that is compatible with the LLM approach.

For this to be understood we should first understand how search works...
