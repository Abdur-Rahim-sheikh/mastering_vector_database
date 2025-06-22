## ক্রোমা ইন্সটলেশন গাইড

ক্রোমা একটি ওপেন সোর্স ডেটাবেস যা AI অ্যাপ্লিকেশনগুলির জন্য ডিজাইন করা হয়েছে। এতে প্রয়োজনীয় সব ফিচার বিল্ট-ইন রয়েছে।

### 1. ক্রোমা ইন্সটল করা

```python
pip install chromadb
```

### 2. ক্রোমা ক্লায়েন্ট

```python
from chromadb import Client
client = Client()
```

### 3. ক্রোমা কালেকশন

```python
collection = client.create_collection(name="my_collection")
```

### 4. ডেটা যোগ করা

```python
collection.add(
    documents=["Hello world", "Goodbye world"],
    metadatas=[{"source": "doc1"}, {"source": "doc2"}],
    ids=["id1", "id2"]
)
```

### 5. ডেটা অনুসন্ধান করা

```python
results = collection.query(
    query_texts=["Hello"],
    n_results=2
)
```

### 6. ডেটা আপডেট করা

```python
collection.update(
    ids=["id1"],
    documents=["Hello universe"],
    metadatas=[{"source": "doc1_updated"}]
)
```

### 7. ডেটা মুছে ফেলা

```python
collection.delete(ids=["id1"])
```

### 8. ডেটা ফিল্টার করা

```python
results = collection.query(
    query_texts=["Hello"],
    n_results=2,
    where={"source": "doc1"}
)
```

### Embedding ফাংশন ব্যবহার করা

যেকোন ভেক্টর ডেটাবেসে ডেটা যোগ করার আগে, ডেটাকে এমবেড করা প্রয়োজন। ক্রোমা বিভিন্ন এমবেডিং ফাংশন সাপোর্ট করে। উদাহরণস্বরূপ:

| Provider                                                                                 | Python | Typescript |
| ---------------------------------------------------------------------------------------- | ------ | ---------- |
| [OpenAI](../../integrations/embedding-models/openai)                                     | ✓      | ✓          |
| [Google Generative AI](../../integrations/embedding-models/google-gemini)                | ✓      | ✓          |
| [Cohere](../../integrations/embedding-models/cohere)                                     | ✓      | ✓          |
| [Hugging Face](../../integrations/embedding-models/hugging-face)                         | ✓      | -          |
| [Instructor](../../integrations/embedding-models/instructor)                             | ✓      | -          |
| [Hugging Face Embedding Server](../../integrations/embedding-models/hugging-face-server) | ✓      | ✓          |
| [Jina AI](../../integrations/embedding-models/jina-ai)                                   | ✓      | ✓          |
| [Cloudflare Workers AI](../../integrations/embedding-models/cloudflare-workers-ai)       | ✓      | ✓          |
| [Together AI](../../integrations/embedding-models/together-ai)                           | ✓      | ✓          |
| [Mistral](../../integrations/embedding-models/mistral)                                   | ✓      | -          |

### ডিফল্ট ওপেনসোর্স এমবেডিং

ডিফল্ট এমবেডিং হিসাবে ক্রোমা `sentence-transformers` এর `all-MiniLM-L6-v2` মডেল ব্যবহার করে। এটি একটি ওপেনসোর্স এমবেডিং মডেল যা টেক্সট ডেটাকে ভেক্টরে রূপান্তর করতে ব্যবহৃত হয়।

```python
from chromadb.utils import embedding_functions
default_ef = embedding_functions.DefaultEmbeddingFunction()
# or
ef = embedding_functions.SentenceTransformerEmbeddingFunction(
    model_name="sentence-transformers/embedding_function_name"
)
```

সব সেন্টেন্স ট্রান্সফর্মার মডেল এর তথ্য পেতে
[https://www.sbert.net/](https://www.sbert.net/) দেখুন।
