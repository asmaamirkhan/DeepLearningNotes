---
description: Regular Expressions guide
---

# 🧩 Regex

## 📕 Notebooks

* [**⭐ Regex Examples**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/applied-nlp/2-regex-examples.ipynb)
* [**🐼 String Processing with Pandas**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/applied-nlp/3-strings-in-pandas.ipynb)

## 🚩 Meta Characters

### 🎎 Character Matches

| 🎀 Symbol | 📃 Description |
| :--- | :--- |
| **`.`** | Single character |
| **`^`** | Start of a string |
| **`$`** | End of a string |
| **`[]`** | One of the set of characters within `[]` |
| **`[a-z]`** | One of the range of characters |
| **`[^abc]`** | Not `a`, `b` or `c` |
| **`[ab]`** | `a` or `b` \(`a` and `b` are strings\) |
| **`()`** | Scoping for operators |
| **`(?:<pattern>)`** | Passive grouping \([**details**](https://stackoverflow.com/a/3705852/12784629)\) |
| **`\`** | Escape character |

### 🎇 Character Symbols

| 🎀 Symbol | 📃 Description | 🤯 Equivalent |
| :--- | :--- | :--- |
| **`\b`** | Word boundary |  |
| **`\d`** | Any digit | `[0-9]` |
| **`\D`** | Any non-digit | `[^0-9]` |
| **`\s`** | Any whitespace | `[ \t\n\r\f\v]` |
| **`\S`** | Any non-whitespace | `[^ \t\n\r\f\v]` |
| **`\w`** | Alphanumeric character | `[a-zA-Z0-9_]` |
| **`\W`** | Non-alphanumeric character | `[^a-zA-Z0-9_]` |

### 💫 Repetitions

| 🎀 Symbol | 📃 Description |
| :--- | :--- |
| **`*`** | Zero or more occurrences |
| `+` | One or more occurrences |
| **`?`** | Zero or one occurrences |
| **`{n}`** | Exactly `n` repetitions |
| **`{n,}`** | At least `n` repetitions |
| **`{,n}`** | At most `n` repetitions |
| **`{m,n}`** | At least `m` and at most `n` repetitions |

## 🧐 Useful Examples

| 🧩 Regex | 📜 Description |
| :--- | :--- |
| _`^.*SOME_STRING.*\n`_  | Finds all lines start with specific string |

## 🔗 References

* [📃 Regex Cheat sheet](https://i.pinimg.com/originals/16/33/8d/16338ddd8e8fdea52a50e6c6981451f3.png)
* [🏃‍♀️ Regex quick start](https://www.rexegg.com/regex-quickstart.html)
* 🐛 [Regex debugger](https://regex101.com/)
* [👀 Regex debugger and visualizer](https://www.debuggex.com/)

