---
description: ⛓ ‍Basics of Sequence Models
---

# 🌱 Introduction

## ⛓ Sequence Models In General
- Sequences are data structures where each example could be seen as a **series** of data points, for example 🧐:

|  Task                         | Input **X**        | Output **Y**          | Type                   |
| ----------------------------- | ------------------ | --------------------- | ---------------------- |
| 💬 Speech Recognition         | Wave sequence      | Text sequence         | Sequence-to-Sequence   |
| 🎶 Music Generation           |  Nothing / Integer | Wave Sequence         | One-to_Sequence        |
| 💌 Sentiment Classification   | Text Sequence      | Integer Rating (1➡5) | Sequence-to-One        |
| 🔠 Machine Translation        | Text Sequence      | Text Sequence         | Sequence-to-Sequence   |
| 📹 Video Activity Recognition | Video Frames       | Label                 | Sequence-to-One        |

> - Since we have labeled data **X** and **Y** so all of these tasks are addressed as _Supervised Learning_ 👩‍🏫
> - Even in Sequence-to-Sequence tasks lengths of input and output can be different ❗

## 🤔 Why Do We Need Sequence Models?
- Machine learning algorithms typically require the text input to be represented as a fixed-length vector 🙄
- Thus, to model sequences, we need a specific learning framework able to:
  - ✔ Deal with variable-length sequences
  - ✔ Maintain sequence order
  - ✔ Keep track of long-term dependencies rather than cutting input data too short
  - ✔ Share parameters across the sequence (so not **re-learn** things across the sequence)

## 👩‍💻 My Codes
- [💬 Text Classification](A-TextClassification.ipynb)