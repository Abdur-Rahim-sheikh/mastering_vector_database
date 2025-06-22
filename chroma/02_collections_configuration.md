## কালেকশন কনফিগারেশন

প্রথমে এক্সাম্পল কালেকশন কনফিগারেশন দেখুন:

```python
collection = client.create_collection(
    name="my_collection_complete",
    configuration={
        "hnsw": {
            "space": "cosine",
            "ef_search": 100,
            "ef_construction": 100,
            "max_neighbors": 16,
            "num_threads": 4
        },
        "embedding_function": embedding_function_name
    }
)
```

### কালেকশন কনফিগারেশন অপশন

- `hnsw` কনফিগারেশন:
  - `space`: ভেক্টর স্পেস, যেমন `cosine`, `l2`, `ip` ইত্যাদি।
  - `ef_search`: সার্চের জন্য `ef` মান, যা সার্চের গুণগত মান নির্ধারণ করে।
  - `ef_construction`: ইনডেক্স নির্মাণের জন্য `ef` মান।
  - `max_neighbors`: সর্বাধিক প্রতিবেশী সংখ্যা।
  - `num_threads`: মাল্টি-থ্রেডিং এর জন্য থ্রেড সংখ্যা।
- `embedding_function`: ভেক্টর তৈরি করার জন্য ব্যবহৃত ফাংশন।

### কালেকশনের কিছু দরকারি মেথড

- `peek`: কালেকশনের প্রথম ১০টি ভেক্টর দেখায়।
- `count`: কালেকশনে মোট ভেক্টরের সংখ্যা রিটার্ন করে।
- `modify`: কালেকশনের নাম পরিবর্তন করে।
