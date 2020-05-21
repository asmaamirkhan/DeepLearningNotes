---
description: Handling texts using Python's built-in functions
---

# 🙌🏻 Handling texts

## 📕 Notebooks

* \*\*\*\*[**💠 Python built-in functions**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/applied-nlp/1-handling-texts.ipynb)\*\*\*\*
* \*\*\*\*[**🐼 String Processing with Pandas**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/applied-nlp/3-strings-in-pandas.ipynb)\*\*\*\*

## 💠 Python built-in functions

### 📏 Length of a string

#### 🔢 Number of characters

```python
text = "Beauty always reserved in details, don't let the big picture steal your attention!"
len(text)
# 82
```

#### 🧾 Number of words

```python
text = "Beauty always reserved in details, don't let the big picture steal your attention!"
words = text.split(' ')
len(words)
# 13
```

#### 4️⃣ Getting words have length greater than 4

```python
text = "Beauty always reserved in details, don't let the big picture steal your attention!"
words = text.split(' ')
moreThan4 = [w for w in words if len(w) > 4]
# ['Beauty', 'always', 'reserved', 'details,', "don't", 'picture', 'steal', 'attention!']
```

### 🎒 Words properties

#### 🔠 Getting capitalized words

```python
text = "Beauty Always reserved in details, Don't let the big picture steal your attention!"
words = text.split(' ')
capitalized = [w for w in words if w.istitle()]
# ['Beauty', 'Always']
# "Don't" is not found 🙄
```

#### 🔚 Getting words end with specific end

* or specific start `.startswith()`

```python
text = "You can hide whatever you want to hide but your eyes will always expose you, eyes never lie."
words = text.split(' ')
endsWithEr = [w for w in words if w.endswith('er')]
# ['whatever', 'never']
```

### 🐥 Upper and lower

```python
"ESMA".isupper() # True
"Esma".isupper() # False
"esma".isupper() # False

"esma".islower() # True
"ESMA".islower() # False
"Esma".islower() # False
```

#### 🤵 Membership test

```python
'm' in 'esma' # True
'es' in 'esma' # True
'ed' in 'esma' # False
```

### 🕵️‍♀️ Unique Words

#### 🔍 Case sensitive

```python
text = "To be or not to be"
words = text.split(' ')
unique = set(words)
# {'be', 'To', 'not', 'or', 'to'}
```

#### ✖️ 🔍 Ignore case

```python
text = "To be or not to be"
words = text.split(' ')
unique = set(w.lower() for w in words)
# {'not', 'or', 'be', 'to'}
```

### 👮‍♀️ Checking Ops

#### Is Digit?

```python
'17'.isdigit() # True
'17.7'.isdigit() # False
```

#### Is Alphabetic?

```python
'esma'.isalpha() # True
'esma17'.isalpha() # False
```

#### Is alphabetic or number?

```python
'17esma'.isalnum() # True
'17esma;'.isalnum() # False
```

### 🔤 String Ops

```python
"Esma".lower() # esma
"Esma".upper() # ESMA
"EsmA".title() # Esma
```

### 🧵 Split & Join

#### Split due to specific character

```python
text = "Beauty,Always,reserved,in,details,Don't,let,the,big,picture,steal,your,attention!"
words = text.split(',')
# ['Beauty', 'Always', 'reserved', 'in', 'details', "Don't", 'let', 'the', 'big', 'picture', 'steal', 'your', 'attention!']
```

#### Join by specific character

```python
text = "Beauty,Always,reserved,in,details,Don't,let,the,big,picture,steal,your,attention!"
words = text.split(',')
joined = " ".join(words)
# Beauty Always reserved in details Don't let the big picture steal your attention!
```

