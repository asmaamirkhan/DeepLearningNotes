---
description: "Custom Object Detection Notes (under development \U0001F469‍\U0001F52C)"
---

# 🤖 TensorFlow Object Detection API

## 🚩 Development Pipeline

* Environment Preparation
* Image acquiring
* Image Organization
* Model Selecting
* Model Configuration
* Training
* Evaluation

## 👩‍💻 Environment Preparation

### 🔸 Environment Info

| 💻 Platform | 🏷️ Version |
| :--- | :--- |
| Python version | 3.7 |
| TensorFlow version | 1.15 |

### 🥦 Conda env Setting

#### 🔮 Create new env

💻 Open cmd and run:

```bash
# conda create -n <ENV_NAME> python=<REQUIRED_VERSION>
conda create -n tf1 python=3.7
```

#### ▶️ Activate the new env

```bash
# conda activate <ENV_NAME>
conda activate tf1
```

### 🔽 Install Packages

#### 🚀  Installing TensorFlow

{% tabs %}
{% tab title="🚀 GPU" %}
```bash
conda install tensorflow-gpu=1.15 
```
{% endtab %}

{% tab title="🚙 CPU" %}
```bash
conda install tensorflow=1.15 
```
{% endtab %}
{% endtabs %}

#### 📦 Installing other packages

```bash
conda install pillow Cython lxml jupyter matplotlib
```

```bash
conda install -c anaconda protobuf
```

### 🤖 Downloading models repository

#### 🤸‍♀️ Cloning from GitHub

* A repository that contains required utils for training and evaluation process
* Open CMD and run in `E` disk and run:

```bash
# note that every time you open CMD you have 
# to activate your env again by running: 
# E:\>conda activate tf1
(tf1) E:\>git clone https://github.com/tensorflow/models.git
(tf1) E:\>cd models/research
```

{% hint style="warning" %}
🧐 I assume that you are running your commands under `E` disk, 
{% endhint %}

#### 🔃 Compiling Protobufs

```bash
(tf1) E:\models\research>for /f %i in ('dir /b object_detection\protos\*.proto') ^do protoc object_detection\protos\%i --python_out=.
```

#### 📦 Compiling Packages

```bash
(tf1) E:\models\research>python setup.py build
(tf1) E:\models\research>python setup.py install
```

#### 🚩 Setting Python Path

```bash
(tf1) E:\models\research>set PYTHONPATH=E:\models\research;E:\models\research\slim
```

### 👩‍🔬 Installation Test

#### 💻 Command

```bash
(tf1) E:\models\research>python object_detection/builders/model_builder_test.py
```

#### 🎉 Expected Output

```bash
Ran 17 tests in 0.833s

OK (skipped=1)
```

## 🖼️ Image Acquiring 

#### 👮‍♀️ Directory Structure

* 🏗️ I suppose that you created a structure like:

```graphql
E:
|___ models
|___ demo
      |___ annotations
      |___ images
      |___ inference
      |___ pre_trainded_model
      |___ scripts
      |___ training
```

| 📂 Folder | 📃 Description |
| :--- | :--- |
| 🤖 `models` | the repo [**here**](https://github.com/tensorflow/models)\*\*\*\* |
| 📄 `annotations` | will contain generated `.csv` and `.tfrecord` files |
| 🖼️ `images` | will contain image data set |
| ▶️ `inference` | will contain exported models after training |
| 👩‍🏫`pre_trained_model`  | will contain files of TensorFlow model that we will retrain |
| 👩‍💻 `scripts`  | will contain scripts that we will use for pre-processing and training processes |
| 🚴‍♀️ `training`  | will contain generated check points during training |

#### 🚀 OpenImages Dataset

* 🕵️‍♀️ You can get images in various methods 
* 👩‍🏫 I will show process of organizing OpenImages data set
* 🗃️ OpenImages is a huge data set contains annotated images of 600 objects

{% embed url="https://storage.googleapis.com/openimages/web/index.html" %}

#### 





