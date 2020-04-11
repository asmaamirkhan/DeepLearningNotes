---
description: "Building Custom Object Detection Step by Step (under development \U0001F469‍\U0001F52C)"
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

### 👮‍♀️ Directory Structure

* 🏗️ I suppose that you created a structure like:

```graphql
E:
|___ models
|___ demo
      |___ annotations
      |___ images
      |___ inference
      |___ OIDv4_ToolKit
      |___ OpenImagesTool
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
| 🔽 `OIDv4_ToolKit` | the repo [**here**](https://github.com/EscVM/OIDv4_ToolKit) \(_OpenImages_ Downloader\) |
| 👩‍🔧 `OpenImagesTool` | the repo [**here**](https://github.com/asmaamirkhan/OpenImagesTool) \(_OpenImages_ Organizer\) |
| 👩‍🏫`pre_trained_model`  | will contain files of _TensorFlow_ model that we will retrain |
| 👩‍💻 `scripts`  | will contain scripts that we will use for pre-processing and training processes |
| 🚴‍♀️ `training`  | will contain generated check points during training |

### 🚀 OpenImages Dataset

* 🕵️‍♀️ You can get images in various methods 
* 👩‍🏫 I will show process of organizing OpenImages data set
* 🗃️ OpenImages is a huge data set contains annotated images of 600 objects
* 🔍 You can explore images by categories from [**here**](https://storage.googleapis.com/openimages/web/visualizer/index.html?set=train&type=segmentation&r=false&c=%2Fm%2F0420v5) 

{% embed url="https://storage.googleapis.com/openimages/web/index.html" %}

### 🎨 Downloading By Category

\*\*\*\*[**OIDv4\_Toolkit**](https://github.com/EscVM/OIDv4_ToolKit) is a tool that we can use to download OpenImages dataset by category and by set \(test, train, validation\)

💻 To clone and build the project, open CMD and run:

```bash
(tf1) E:\pre_trainded_model>git clone https://github.com/EscVM/OIDv4_ToolKit.git
(tf1) E:\pre_trainded_model>cd OIDv4_ToolKit
(tf1) E:\pre_trainded_model\OIDv4_ToolKit>pip install -r requirements.txt
```

⏬ To start downloading by category:

```bash
# python main.py downloader --classes <OBJECT_LIST> --type_csv <TYPE>
# TYPE: all | test | train | validation 
(tf1) E:\pre_trainded_model\OIDv4_ToolKit>python main.py downloader --classes Apple Orange --type_csv validation
```

{% hint style="warning" %}
👮‍♀️ If object name consists of 2 parts then write it with `'_', e.g.` Bell\_pepper
{% endhint %}

## 🤹‍♀️ Image Organization

### 🔮 OpenImagesTool

* 👩‍💻 [**OpenImagesTool**](https://github.com/asmaamirkhan/OpenImagesTool) is a tool to convert OpenImages images and annotations to _TensorFlow_-friendly structure.
* 🙄 _OpenImages_ provides annotations ad `.txt` files in a format like:`<OBJECT_NAME> <XMIN> <YMIN> <XMAX> <YMAX>` which is not compatible with _TensorFlow_ that requires _VOC_ annotation format
* 💫 To do that synchronization we can do the following  

💻 To clone and build the project, open _CMD_ and run:

```bash
(tf1) E:\pre_trainded_model>git clone https://github.com/asmaamirkhan/OpenImagesTool.git
(tf1) E:\pre_trainded_model>cd OpenImagesTool/src
```

### 💻 Applying Organizing

🚀 Now, we will convert images and annotations that we have downloaded and save them to `images` folder

```bash
# under (tf1) E:\pre_trainded_model\OpenImagesTool\src> 
# python script.py -i <INPUT_PATH> -o <OUTPUT_PATH>
python script.py -i E:\pre_trainded_model\OIDv4_ToolKit\OID\Dataset -o E:\pre_trainded_model\images
```

{% hint style="info" %}
👩‍🔬 _OpenImagesTool_ adds validation images to training set by default, if you wand to disable this behavior you can add `-v` flag to the command.
{% endhint %}

### 🏭 Generating CSV Files

```bash

```

### 👩‍🏭 Generating TF Records

```bash

```

## 🤖 Model Selecting

* 🎉 [**TensorFLow Object Detection Zoo**](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md#coco-trained-models) provides a lot of pre-trained models
* 🕵️‍♀️ Models differentiate in terms of accuracy and speed, you can select the suitable model due to your priorities
* 💾 Select a model, extract it and save it under `pre_trained_model` folder

## 👩‍🔧 Model Configuration

### ⏬ Downloading config File

* 😎 We have downloaded the models \(pre-trained weights\) but now we have to download configuration file that contains training parameters and settings
* 👮‍♀️ Every model in TensorFlow Object Detection Zoo has a configuration file presented [**here**](https://github.com/tensorflow/models/tree/master/research/object_detection/samples/configs)
* 💾 Download the config file that corresponds to the models you have selected and save it under `training` folder

### 👩‍🔬 Updating config File

You have to update the following lines:

```bash

```









