# Building_RAG_Chatbots_for_Technical_Documentation
Implement retrieval augmented generation (RAG) with LangChain to create a chatbot for answering questions about technical documentation.

## Car Manual RAG Assistant: Explaining Dashboard Warnings with LangChain, Chroma & GPT-4o-mini | Python, LLMs

Built a Retrieval Augmented Generation (RAG) assistant that answers car dashboard warning questions from an MG ZS manual instead of relying on the LLM's general knowledge. Given a warning, it retrieves the relevant manual sections and returns a short explanation and recommended action.

# CONTEXT
A car manufacturer scenario: could an LLM guide drivers through warning messages, with answers short enough to be read aloud by text-to-speech? As a proof of concept, I grounded gpt-4o-mini in several pages of the manual covering warnings, meanings and actions.

# MY ROLE
I wrote the retrieval and generation chain. Loading the document and the model setup were provided.

# WHAT I DID
• Split the HTML manual into overlapping chunks (1,000 characters, 200 overlap) with RecursiveCharacterTextSplitter so related instructions stay together (9 docs of 1000-1200 characters)
• Embedded the chunks with OpenAI text-embedding-3-small and stored them in a Chroma vector database
• Created a retriever with default top-k (4) to fetch the most relevant chunks for each query
• Wrote a prompt that restricts answers to retrieved context, tells the model to say "I don't know" when unsure, and caps replies at three sentences
• Composed the pipeline with LangChain (retriever + question, then prompt, then LLM at temperature 0) and tested it on a Gasoline Particulate Filter Full warning

# RESULTS
• The assistant explained the warning and the recommended action in 2 sentences ("The Gasoline Particular Filter Full warning has appeared. What does this mean and what should I do about it?" -> "The Gasoline Particular Filter Full warning indicates that the gasoline particulate filter is full. You should consult an MG Authorised Repairer as soon as possible for assistance."
• The response was relevant and output was concise and suited to voice playback

# TECH STACK
Python, LangChain, OpenAI API (gpt-4o-mini, text-embedding-3-small), Chroma, RAG, prompt engineering
