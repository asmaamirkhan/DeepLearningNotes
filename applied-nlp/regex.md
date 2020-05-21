---
description: Regular Expressions guide
---

# 🧩 Regex

## 🚩 Meta Characters

### 🎎 Character Matches

| 🎀 Symbol | 📃 Description |
| :--- | :--- |
| **`.`** | Single character |
| **`^`** | Start of a string |
| **`$`** | End of a string |
| **`[]`** | One of the set of characters within `[]` |
| **`[a-z]`** | One of the range of characters |
| **`[^abc]`** | Not a,b or c |
| **`a|b`** | a or b \(a and b are strings\) |
| **`()`** | Scoping for operators |
| **`\`** | Escape character |

### 🎇 Character Symbols

| 🎀 Symbol | 📃 Description | 🤯 Equivalent |
| :--- | :--- | :--- |
| **`\b`** | Word boundary |  |
| **`\d`** | Any digit  | `[0-9]` |
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

