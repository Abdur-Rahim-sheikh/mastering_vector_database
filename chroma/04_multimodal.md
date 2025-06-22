### মাল্টিমোডাল এমবেডিং ফাংশন

ক্রোমা মাল্টিমোডাল এমবেডিং ফাংশন সমর্থন করে, যা টেক্সট, ইমেজ (ভবিষ্যৎ অডিও, ভিডিও) এমবেডিং তৈরি করতে পারে।

`OpenCLIP` ফাংশনটি ক্রোমার বিল্টিন আছে।

```python
from chromadb.utils.embedding_functions import OpenCLIPEmbeddingFunction
embedding_functions = OpenCLIPEmbeddingFunction()
```

### ডাটা লোডারস

ক্রোমা ডাটা লোডারস সমর্থন করে এতে ইমেজ অন্য কোথাও থাকে, আর ক্রোমাকে URI প্রদান করা হয়। ক্রোমা ডাটা সেভ করবে না, বরং URI সেভ করবে এবং ডাটা লোডার ব্যবহার করে ডাটা লোড করবে।

```python
from chromadb.utils.data_loaders import ImageLoader
image_loader = ImageLoader()
```

এখন সাধারণ যেকোন কুয়েরির সাথে `query_images`, `query_texts`, ব্যবহার করা যাবে।

এই কোলাব [মাল্টিমোডাল ডেমো](https://colab.research.google.com/github/chroma-core/chroma/blob/main/examples/multimodal/multimodal_retrieval.ipynb) দেখুন।
