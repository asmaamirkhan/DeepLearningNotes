---
description: "Training Custom Object Detector Step by Step (under development \U0001F469‍\U0001F52C)"
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
* Model Exporting

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
      |___ eval
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
| 📄 `annotations` | will contain generated `.csv` and `.record` files |
| 👮‍♀️ `eval` | will contain results of evaluation |
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
(tf1) E:\demo>git clone https://github.com/EscVM/OIDv4_ToolKit.git
(tf1) E:\demo>cd OIDv4_ToolKit
(tf1) E:\demo\OIDv4_ToolKit>pip install -r requirements.txt
```

⏬ To start downloading by category:

```bash
# python main.py downloader --classes <OBJECT_LIST> --type_csv <TYPE>
# TYPE: all | test | train | validation 
(tf1) E:\demo\OIDv4_ToolKit>python main.py downloader --classes Apple Orange --type_csv validation
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
(tf1) E:\demo>git clone https://github.com/asmaamirkhan/OpenImagesTool.git
(tf1) E:\demo>cd OpenImagesTool/src
```

### 💻 Applying Organizing

🚀 Now, we will convert images and annotations that we have downloaded and save them to `images` folder

```bash
# under (tf1) E:\demo\OpenImagesTool\src> 
# python script.py -i <INPUT_PATH> -o <OUTPUT_PATH>
python script.py -i E:\pre_trainded_model\OIDv4_ToolKit\OID\Dataset -o E:\pre_trainded_model\images
```

{% hint style="info" %}
👩‍🔬 _OpenImagesTool_ adds validation images to training set by default, if you wand to disable this behavior you can add `-v` flag to the command.
{% endhint %}

### 🏷️ Creating Label Map

* ⛓️ `label_map.pbtxt` is a file that maps object names to corresponded IDs
* ➕ Create `label_map.pbtxt`file under annotations folder and open it in a text editor
* 🖊️ Write your objects names and IDs in the following format

```javascript
item {
    id: 1
    name: 'Hamster'
}

item {
    id: 2
    name: 'Apple'
}
```

{% hint style="info" %}
`👮‍♀️ id:0` is reserved for background, so don' t use it

🐞 Related error: `ValueError: Label map id 0 is reserved for the background label`
{% endhint %}

### 🏭 Generating CSV Files

* 🔄 Now we have to convert `.xml` files to csv file
* 🔻 Download the script [**xml\_to\_csv.py**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/8-objectdetection/xml_to_csv.py)  ****script and save it under `scripts` folder
*  💻 Open CMD and run:

#### 👩‍🔬 Generating train csv file

```bash
# under (tf1) E:\demo\scripts>
python xml_to_csv.py -i E:\demo\images\train -o E:\demo\annotations\train_labels.csv 
```

#### 👩‍🔬 Generating test csv file

```bash
# under (tf1) E:\demo\scripts>
python xml_to_csv.py -i E:\demo\images\test -o E:\demo\annotations\test_labels.csv 
```

### 👩‍🏭 Generating TF Records

* 🙇‍♀️ Now, we will generate tfrecords that will be used in training precess
* 🔻 Download [**generate\_tfrecords.py**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/8-objectdetection/generate_tfrecords.py) script and save it under `scripts` folder

#### 👩‍🔬 Generating train tfrecord

```bash
# under (tf1) E:\demo\scripts>
# python generate_tfrecords.py --label_map=<PATH_TO_LABEL_MAP> 
# --csv_input=<PATH_TO_CSV_FILE> --img_path=<PATH_TO_IMAGE_FOLDER>
# --output_path=<PATH_TO_OUTPUT_FILE>
python generate_tfrecords.py --label_map=E:/demo/annotations/label_map.pbtxt --csv_input=E:\demo\annotations\train_labels.csv --img_path= E:\demo\images\train --output_path=E:\demo\annotations\train.record
```

#### 👩‍🔬 Generating test tfrecord

```bash
# under (tf1) E:\demo\scripts>
python generate_tfrecords.py --label_map=E:/demo/annotations/label_map.pbtxt --csv_input=E:\demo\annotations\test_labels.csv --img_path= E:\demo\images\test --output_path=E:\demo\annotations\test.record
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

```javascript
// number of classes
num_classes: 1 // set it to total number of classes you have

// path of pre-trained checkpoint
fine_tune_checkpoint: "E:/demo/pre_trained_model/ssd_mobilenet_v1_quantized_300x300_coco14_sync_2018_07_18/model.ckpt"

// path to train tfrecord
tf_record_input_reader {
    input_path: "E:/demo/annotations/train.record"
}

// number of images that will be used in evaluation process
eval_config: {
  metrics_set: "coco_detection_metrics"
  use_moving_averages: false
  // I suggest setting it to total number of testing set to get accurate results
  num_examples: 11193
}

eval_input_reader: {
  tf_record_input_reader {
    // path to test tfrecord
    input_path: "E:/demo/annotations/test.record"
  }
  // path to label map
  label_map_path: "E:/demo/annotations/label_map.pbtxt"
  // set it to true if you want to shuffle test set at each evaluation   
  shuffle: false
  num_readers: 1
}
```

{% hint style="info" %}
🤹‍♀️ If you give the whole test set to evaluation process then shuffle functionality won't affect the results, it will only give you different examples on TensorBoard
{% endhint %}

## 👶 Training

* 🎉 Now we have done all preparations
* 🚀 Let the computer start learning
* 💻 Open CMD and run:

```bash
# under (tf1) E:\models\research\object_detection\legacy> 
# python train.py --train_dir=<DIRECTORY_TO_SAVE_CHECKPOINTS> 
# --pipline_config_path=<PATH_TO_CONFIG_FILE>
python train.py --train_dir=E:/demo/training --pipline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config
```

* 🕐 This process will take long \(You can take a nap 🤭, but a long nap 🙄\)
* 🕵️‍♀️ While model is being trained you will see loss values on CMD
* ✋ You can stop the process when the loss value achieves a good value \(under 1\)  

## 👮‍♀️ Evaluation

### 🎳 Evaluating Script

* 🤭 After training process is done, let's do an exam to know how good \(or bad 🙄\) is our model doing
* 🎩 The following command will use the model on whole test set and after that print the results, so that we can do error analysis.
* 💻 So that, open CMD and run:

```bash
# under (tf1) E:\models\research\object_detection\legacy> 
# python eval.py --logtostderr --pipline_config_path=<PATH_TO_CONFIG_FILE>
# --checkpoint_dir=<DIRECTORY_OF_CHECKPOINTS> --eval_dir=<DIRECTORY_TO_SAVE_EVAL_RESULTS>
python eval.py --pipline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config --checkpoint_dir=--pipline_config_path=E:/demo/training --eval_dir=--pipline_config_path=E:/demo/eval
```

###  👀 Visualizing Results

* ✨ To see results on charts and images we can use TensorBoard for better analyzing
*  💻 Open CMD and run:

```bash
# under (tf1) E:\>
tensorboard --logdir=E:/demo/eval
```

## 👒 Model Exporting

* 🔧 After training and evaluation processes are done, we have to make the model in such a format that we can use
* 🦺 For now, we have only checkpoints, so that we have to export `.pb` file
* 💻 So, open  CMD and run:

```bash
# under (tf1) E:\models\research\object_detection>
# python export_inference_graph.py --input_type image_tensor 
# --pipline_config_path <PATH_TO_CONFIG_FILE> 
# --trained_checkpoing_prefix <PATH_TO_LAST_CHECKPOINT>
# --output_directory <PATH_TO_SAVE_EXPORTED_MODEL>
python export_inference_graph.py --input_type image_tensor --pipline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config --trained_checkpoing_prefix E:/demo/training/model.ckpt-16438 --output_directory E:/demo/inference/ssd_v1_quant  
```

* If you are using SSD and planning to convert it to tflite later you have to run

```bash
# under (tf1) E:\models\research\object_detection>
# python export_tflite_ssd_graph.py --input_type image_tensor 
# --pipline_config_path <PATH_TO_CONFIG_FILE> 
# --trained_checkpoing_prefix <PATH_TO_LAST_CHECKPOINT>
# --output_directory <PATH_TO_SAVE_EXPORTED_MODEL>
python export_tflite_ssd_graph.py --input_type image_tensor --pipline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config --trained_checkpoing_prefix E:/demo/training/model.ckpt-16438 --output_directory E:/demo/inference/ssd_v1_quant  
```

## 🐞 Common Issues

#### 🥅 nets module issue

`ModuleNotFoundError: No module named 'nets'`

This means that there is a problem in setting `PYTHONPATH`, try to run:

```bash
(tf1) E:\models\research>set PYTHONPATH=E:\models\research;E:\models\research\slim
```

#### 🤯 LossTensor is inf issue

\`\`[`LossTensor is inf or nan. : Tensor had NaN values`](https://github.com/tensorflow/models/issues/1881)

 



