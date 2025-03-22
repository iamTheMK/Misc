Power Automate Flow 1 (Embeddings Generation)

Q1: Why did we choose text-embedding-ada-002 for generating embeddings instead of other models?

✅ text-embedding-ada-002 was chosen because:

It is optimized for embeddings, unlike GPT models that focus on text generation.

It provides high-quality 1536-dimensional vectors for semantic search.

It is cost-effective and faster compared to using GPT models for embeddings.

Q2: Why not use GPT-4 or another model for embeddings?

❌ GPT-4 is not suitable for embeddings because:

It is not optimized for vector representation.

It is much more expensive and slow for embedding generation.

It would create embeddings in a different structure, making retrieval inefficient.

🔹 Power Automate Flow 2 (Query Embeddings & Retrieval)

Q3: Why did we use text-embedding-ada-002 again for query embeddings?

✅ The same model must be used for both stored document embeddings and query embeddings because:

It ensures that both exist in the same vector space, enabling accurate similarity search.

Different embedding models might generate vectors of different dimensions, causing mismatches.

🔹 GPT-4 Turbo for Answer Generation

Q4: Why did we use GPT-4 Turbo for augmentation and generation instead of another model?

✅ GPT-4 Turbo was chosen because:

It can synthesize, structure, and generate natural language responses.

Embedding models like text-embedding-ada-002 only generate numerical vectors, not text.

GPT-4 Turbo allows prompt customization using hyperparameters (temperature, top-p, etc.).

🔹 Hyperparameters in GPT-4 Turbo

Q5: What are the key hyperparameters that influence GPT-4 Turbo’s output?

HyperparameterEffect

TemperatureHigher = More creativity, Lower = More deterministic

Top-P (Nucleus Sampling)Controls response diversity (lower = more predictable)

Max TokensLimits response length

Presence PenaltyEncourages new words (higher = more variety)

Frequency PenaltyPrevents excessive repetition

🔹 Alternative Models for Embeddings in AI Foundry

Q6: Apart from text-embedding-ada-002, what other models could we use in AI Foundry for embeddings?

ModelProviderVector DimensionalityNotes

text-embedding-3-smallOpenAI512Cheaper, lower quality

text-embedding-3-largeOpenAI3072More accurate, more expensive

BGE-M3Microsoft AI Foundry1024Optimized for multi-modal embeddings

all-MiniLM-L6-v2Hugging Face384Faster but lower quality

mpnet-base-v2Hugging Face768Better accuracy than MiniLM

e5-large-v2Hugging Face1024Good for retrieval tasks

✅ Best choice? text-embedding-ada-002 remains the best unless you need cheaper (text-embedding-3-small) or higher accuracy (text-embedding-3-large or e5-large-v2).

🔹 Final Takeaways

1️⃣ Flow 1: text-embedding-ada-002 is used because it is optimized for embeddings.

2️⃣ Flow 2: The same model is reused for query embeddings to maintain consistency.

3️⃣ GPT-4 Turbo is used for answer generation because it can understand and synthesize retrieved text.

4️⃣ Hyperparameters (temperature, top-p, etc.) control the style and variability of GPT responses.

5️⃣ Other embedding models (OpenAI, AI Foundry, Hugging Face) exist, but text-embedding-ada-002 is the best choice for now.

Would you like me to add any missing details or refine this further?