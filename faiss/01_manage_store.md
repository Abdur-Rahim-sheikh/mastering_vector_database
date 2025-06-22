### ল্যাংচেইনের মাধ্যমে FAISS ভেক্টর স্টোর ম্যানেজ করা

```python
from langchain_ollama import OllamaEmbeddings
embeddings = OllamaEmbeddings(model="llama3")
```

```python
import faiss
from langchain_community.vectorstores import FAISS
from langchain_community.docstore.in_memory import InMemoryDocstore

index = faiss.IndexFlatL2(len(embeddings.embed_query("example text")))

vectorstore = FAISS(
    index=index,
    embedding_function=embeddings,
    docstore=InMemoryDocstore(),
    index_to_docstore_id={},
)
```

### ভেক্টর স্টোরে ডেটা যোগ করা

```python
from uuid import uuid4
from langchain_community.schema import Document
documents = [
    Document(page_content="This is a sample document.", metadata={"source": "source1"}),
    Document(page_content="Another document for testing.", metadata={"source": "source2"}),
]

uuids = [str(uuid4()) for _ in documents]
vectorstore.add_documents(documents, ids=uuids)
```

### ভেক্টর স্টোর থেকে ডিলেট করা

```python
vectorstore.delete(ids=uuids[s:t])
```

### ভেক্টর স্টোর থেকে ডেটা খোঁজা

```python
results = vectorstore.similarity_search("sample document", k=2, filter={"source": "source1"})
for result in results:
    print(result.page_content, result.metadata)
```

### কুয়েরি ফিল্টারিং

`$eq`, `$neq`, `$gt`, `$lt`, `$gte`, `$lte`, `$in`, `$nin`, `$and`, `$or` and `$not` অপারেটর ব্যবহার করে কুয়েরি ফিল্টার করা যায়।

```python
results = vectorstore.similarity_search(
    "sample document",
    k=2,
    filter={
        "source": {"$eq": "source1"},
        "metadata": {"$gt": 10},
        "$or": [{"source": {"$eq": "source2"}}, {"metadata": {"$lt": 5}}],
    },
)
for result in results:
    print(result.page_content, result.metadata)
```

- স্কোর সহ অনুসন্ধান করতে `similarity_search_with_score` ব্যবহার করা যায়।

```python
results_with_score = vectorstore.similarity_search_with_score("sample document", k=2)
for result, score in results_with_score:
    print(result.page_content, result.metadata, score)
```

### কুয়েরিকে রিট্রিভার হিসেবে ব্যবহার করা

```python
retriever = vectorstore.as_retriever(
    search_type="mmr",
    search_kwargs={"k": 5, "fetch_k": 10},
)
retriever.invoke("sample document", filter={"source": {"$eq": "source1"}})
```
