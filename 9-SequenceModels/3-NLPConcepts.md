# 💬 Basic Concepts of NLP
Basic concepts of Natural Language Processing

## 👒 Word Representation
- [One Hot Encoding](./0-GeneralConcepts.md#-one-hot-encoding)
- Featurized Representation (Word Embedding)

### 🎎 Word Embedding
- Representing words by associating them with features such as gender, age, royal, food, cost, size.... and so on 
- Every feature is represented as a range between [-1, 1] 
- Thus, every word can be represented as a vector of these features
  - The dimension of each vector is related to the number of features that we pick

#### 🎀 Advantages
- Similarity of words that have similar features will be evident
- Vectors are smaller than vectors in one hot representation


> TODO: Subtracting vectors of oppsite words