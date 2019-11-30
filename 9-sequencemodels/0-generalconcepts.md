# 📚 General Concepts of Sequence Models

## 👩‍🏫 Notation

In the context of text processing \(e.g: Natural Language Processing _NLP_\)

| Symbol | Description |
| :--- | :--- |
| X&lt;t&gt; | The `t`th word in the input sequence |
| Y&lt;t&gt; | The `t`th word in the output sequence |
| X\(i\)&lt;t&gt; | The `t`th word in the `i`th input sequence |
| Y\(i\)&lt;t&gt; | The `t`th word in the `i`th output sequence |
| Tx\(i\) | The length of the `i`th input sequence |
| Ty\(i\) | The length of the `i`th output sequence |

## 🚀 One Hot Encoding

A way to represent words so we can treat with them easily

### 🔎 Example

Let's say that we have a dictionary that consists of 10 words \(🤭\) and the words of the dictionary are:

* Car, Pen, Girl, Berry, Apple, Likes, The, And, Boy, Book.

Our X\(i\) is: **The Girl Likes Apple And Berry**

So we can represent this sequence like the following 👀

```text
Car   -0)  ⌈ 0 ⌉   ⌈ 0 ⌉   ⌈ 0 ⌉   ⌈ 0 ⌉  ⌈ 0 ⌉   ⌈ 0 ⌉ 
Pen   -1)  | 0 |  | 0 |  | 0 |  | 0 |  | 0 |  | 0 |
Girl  -2)  | 0 |  | 1 |  | 0 |  | 0 |  | 0 |  | 0 |
Berry -3)  | 0 |  | 0 |  | 0 |  | 0 |  | 0 |  | 1 |
Apple -4)  | 0 |  | 0 |  | 0 |  | 1 |  | 0 |  | 0 |
Likes -5)  | 0 |  | 0 |  | 1 |  | 0 |  | 0 |  | 0 |
The   -6)  | 1 |  | 0 |  | 0 |  | 0 |  | 0 |  | 0 |
And   -7)  | 0 |  | 0 |  | 0 |  | 0 |  | 1 |  | 0 |
Boy   -8)  | 0 |  | 0 |  | 0 |  | 0 |  | 0 |  | 0 |
Book  -9)  ⌊ 0 ⌋   ⌊ 0 ⌋   ⌊ 0 ⌋   ⌊ 0 ⌋  ⌊ 0 ⌋   ⌊ 0 ⌋
```

By representing sequences in this way we can feed out data to neural networks✨

### 🙄 Disadvantage

* If our dictionary consists of 10,000 words so each vector will be 10,000 dimensional 🤕 

