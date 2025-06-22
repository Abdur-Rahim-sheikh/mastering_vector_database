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
