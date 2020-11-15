---
description: Training Custom Object Detector Step by Step
---

# 🤖 TensorFlow Object Detection API

## 🌱 Introduction

* ✨ _Tensorflow_ object detection API is a powerful tool that allows us to create custom object detectors depending on pre-trained, fine tuned models even if we don't have strong AI background or strong _TensorFlow_ knowledge.
* 💁‍♀️ Building models depending on pre-trained models saves us a lot of time and labor since we are using models that maybe trained for weeks using very strong machines, this principle is called [**Transfer Learning**](../popular-strategies-of-deep-learning/transfer-learning.md)**.**
* 🗃️ As a data set I will show you how to use _OpenImages_ data set and converting its data to _TensorFlow_-friendly format.
* 🎀 You can find this article on [**Medium**](https://medium.com/@asmaamirkhan.am/training-custom-object-detector-step-by-step-5f6f4d75b494) too.

## 🚩 Development Pipeline

1. [👩‍💻 Environment Preparation](tensorflow-object-detection-api.md#environment-preparation)
2. [🖼️ Image acquiring](tensorflow-object-detection-api.md#image-acquiring)
3. [🤹‍♀️ Image Organization](tensorflow-object-detection-api.md#image-organization)
4. [🤖 Model Selecting](tensorflow-object-detection-api.md#model-selecting)
5. [👩‍🔧 Model Configuration](tensorflow-object-detection-api.md#model-configuration)
6. [👶 Training](tensorflow-object-detection-api.md#training)
7. [👮‍♀️ Evaluation](tensorflow-object-detection-api.md#evaluation)
8. [👒 Model Exporting](tensorflow-object-detection-api.md#model-exporting)
9. [📱 Converting to tflite](tensorflow-object-detection-api.md#converting-to-tflite)

{% hint style="info" %}
🤕 While you are applying the instructions if you get errors you can check out [🐞 Common Issues](tensorflow-object-detection-api.md#common-issues) section at the end of the article
{% endhint %}

## 👩‍💻 Environment Preparation

### 🔸 Environment Info

| 💻 Platform | 🏷️ Version |
| :--- | :--- |
| Python version | 3.7 |
| TensorFlow version | 1.15 |

### 🥦 Conda env Setting

#### 🔮 Create new env

* 🥦 Install [**Anaconda**](https://www.anaconda.com/)
* 💻 Open cmd and run:

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

#### 💥 GPU vs CPU Computing

| 🚙 CPU | 🚀 GPU |
| :--- | :--- |
| **Brain** of computer | **Brawn** of computer |
| Very few complex cores | hundreds of simpler cores with parallel architecture |
| single-thread performance optimization | thousands of concurrent hardware threads |
| Can do a bit of everything, but not great at much | Good for math heavy processes |

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

{% tabs %}
{% tab title="💻 Windows" %}
```bash
# under (tf1) E:\models\research>
for /f %i in ('dir /b object_detection\protos\*.proto') do protoc object_detection\protos\%i --python_out=.
```
{% endtab %}

{% tab title="🐧 Linux" %}
```bash
# under /models/research
$ protoc object_detection/protos/*.proto --python_out=.
```
{% endtab %}
{% endtabs %}

#### 📦 Compiling Packages

```bash
# under (tf1) E:\models\research>
python setup.py build
python setup.py install
```

#### 🚩 Setting Python Path Temporarily

{% tabs %}
{% tab title="💻 Windows" %}
```bash
# under (tf1) E:\models\research> or anywhere 😅
set PYTHONPATH=E:\models\research;E:\models\research\slim
```
{% endtab %}

{% tab title="🐧 Linux" %}
```bash
# under /models/research
$ export PYTHONPATH=`pwd`:`pwd`/slim
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
👮‍♀️ Every time you open CMD you have to set `PYTHONPATH` again
{% endhint %}

### 👩‍🔬 Installation Test

🧐 Check out that every thing is done

#### 💻 Command

```bash
# under (tf1) E:\models\research>
python object_detection/builders/model_builder_tf1_test.py
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
| 🤖 `models` | the repo [**here**](https://github.com/tensorflow/models) |
| 📄 `annotations` | will contain generated `.csv` and `.record` files |
| 👮‍♀️ `eval` | will contain results of evaluation |
| 🖼️ `images` | will contain image data set |
| ▶️ `inference` | will contain exported models after training |
| 🔽 `OIDv4_ToolKit` | the repo [**here**](https://github.com/EscVM/OIDv4_ToolKit) \(_OpenImages_ Downloader\) |
| 👩‍🔧 `OpenImagesTool` | the repo [**here**](https://github.com/asmaamirkhan/OpenImagesTool) \(_OpenImages_ Organizer\) |
| 👩‍🏫`pre_trained_model` | will contain files of _TensorFlow_ model that we will retrain |
| 👩‍💻 `scripts` | will contain scripts that we will use for pre-processing and training processes |
| 🚴‍♀️ `training` | will contain generated check points during training |

### 🚀 OpenImages Dataset

* 🕵️‍♀️ You can get images in various methods 
* 👩‍🏫 I will show process of organizing OpenImages data set
* 🗃️ OpenImages is a huge data set contains annotated images of 600 objects
* 🔍 You can explore images by categories from [**here**](https://storage.googleapis.com/openimages/web/visualizer/index.html?set=train&type=segmentation&r=false&c=%2Fm%2F0420v5) 

{% embed url="https://storage.googleapis.com/openimages/web/index.html" caption="" %}

### 🎨 Downloading By Category

[**OIDv4\_Toolkit**](https://github.com/EscVM/OIDv4_ToolKit) is a tool that we can use to download OpenImages dataset by category and by set \(test, train, validation\)

💻 To clone and build the project, open CMD and run:

```bash
# under (tf1) E:\demo>
git clone https://github.com/EscVM/OIDv4_ToolKit.git
cd OIDv4_ToolKit

# under (tf1) E:\demo\OIDv4_ToolKit>
pip install -r requirements.txt
```

⏬ To start downloading by category:

```bash
# python main.py downloader --classes <OBJECT_LIST> --type_csv <TYPE>
# TYPE: all | test | train | validation 
# under (tf1) E:\demo\OIDv4_ToolKit>
python main.py downloader --classes Apple Orange --type_csv validation
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
# under (tf1) E:\demo>
git clone https://github.com/asmaamirkhan/OpenImagesTool.git
cd OpenImagesTool/src
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
* 🔻 Download the script [**xml\_to\_csv.py**](https://github.com/asmaamirkhan/DeepLearningNotes/blob/master/8-objectdetection/xml_to_csv.py)  script and save it under `scripts` folder
* 💻 Open CMD and run:

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
python generate_tfrecords.py --label_map=E:/demo/annotations/label_map.pbtxt --csv_input=E:\demo\annotations\train_labels.csv --img_path=E:\demo\images\train --output_path=E:\demo\annotations\train.record
```

#### 👩‍🔬 Generating test tfrecord

```bash
# under (tf1) E:\demo\scripts>
python generate_tfrecords.py --label_map=E:/demo/annotations/label_map.pbtxt --csv_input=E:\demo\annotations\test_labels.csv --img_path=E:\demo\images\test --output_path=E:\demo\annotations\test.record
```

## 🤖 Model Selecting

* 🎉 [**TensorFLow Object Detection Zoo**](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf1_detection_zoo.md#coco-trained-models) provides a lot of pre-trained models
* 🕵️‍♀️ Models differentiate in terms of accuracy and speed, you can select the suitable model due to your priorities
* 💾 Select a model, extract it and save it under `pre_trained_model` folder
* 👀 Check out my notes [**here**](https://dl.asmaamir.com/8-objectdetection) to get insight about differences between popular models 

## 👩‍🔧 Model Configuration

### ⏬ Downloading config File

* 😎 We have downloaded the models \(pre-trained weights\) but now we have to download configuration file that contains training parameters and settings
* 👮‍♀️ Every model in TensorFlow Object Detection Zoo has a configuration file presented [**here**](https://github.com/tensorflow/models/tree/master/research/object_detection/samples/configs)
* 💾 Download the config file that corresponds to the models you have selected and save it under `training` folder

### 👩‍🔬 Updating config File

You have to update the following lines:

{% hint style="info" %}
🙄 Take a look at [Loss exploding issue]()
{% endhint %}

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
# --pipeline_config_path=<PATH_TO_CONFIG_FILE>
python train.py --train_dir=E:/demo/training --pipeline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config
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
# python eval.py --logtostderr --pipeline_config_path=<PATH_TO_CONFIG_FILE>
# --checkpoint_dir=<DIRECTORY_OF_CHECKPOINTS> --eval_dir=<DIRECTORY_TO_SAVE_EVAL_RESULTS>
python eval.py --pipeline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config --checkpoint_dir=E:/demo/training --eval_dir=E:/demo/eval
```

### 👀 Visualizing Results

* ✨ To see results on charts and images we can use TensorBoard for better analyzing
* 💻 Open CMD and run:

#### 👩‍🏫 Training Values Visualization

* 🧐 Here you can see graphs of loss, learning rate and other values
* 🤓 And much more \(You can investigate tabs at the top\)
* 😋 It is feasable to use it while training \(and exciting 🤩\)

```bash
# under (tf1) E:\>
tensorboard --logdir=E:/demo/tarining
```

#### 👮‍♀️ Evaluation Values Visualization

* 👀 Here you can see images from your test set with corresponded predictions
* 🤓 And much more \(You can inspect tabs at the top\)
* ❗ You must use this after running evaluation script

```bash
# under (tf1) E:\>
tensorboard --logdir=E:/demo/eval
```

* 🔍 See the visualized results on [localhost:6006](http://localhost:6006/) and 
* 🧐 You can inspect numerical values from report on terminal, result example:

```bash
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.708
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 0.984
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 0.868
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = 0.289
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = 0.623
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.767
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 0.779
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 0.781
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 0.781
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = 0.300
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = 0.703
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = 0.824
```

* 🎨 If you want to get metric report for each class you have to change evaluating protocol to _pascal metrics_ by configuring  `metrics_set` in `.config` file:

```javascript
eval_config: {
  ...
  metrics_set: "weighted_pascal_voc_detection_metrics"
  ...
}
```

## 👒 Model Exporting

* 🔧 After training and evaluation processes are done, we have to make the model in such a format that we can use
* 🦺 For now, we have only checkpoints, so that we have to export `.pb` file
* 💻 So, open  CMD and run:

```bash
# under (tf1) E:\models\research\object_detection>
# python export_inference_graph.py --input_type image_tensor 
# --pipeline_config_path <PATH_TO_CONFIG_FILE> 
# --trained_checkpoint_prefix <PATH_TO_LAST_CHECKPOINT>
# --output_directory <PATH_TO_SAVE_EXPORTED_MODEL>
python export_inference_graph.py --input_type image_tensor --pipeline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config --trained_checkpoint_prefix E:/demo/training/model.ckpt-16438 --output_directory E:/demo/inference/ssd_v1_quant
```

* If you are using SSD and planning to convert it to tflite later you have to run

```bash
# under (tf1) E:\models\research\object_detection>
# python export_tflite_ssd_graph.py --input_type image_tensor 
# --pipeline_config_path <PATH_TO_CONFIG_FILE> 
# --trained_checkpoint_prefix <PATH_TO_LAST_CHECKPOINT>
# --output_directory <PATH_TO_SAVE_EXPORTED_MODEL>
python export_tflite_ssd_graph.py --input_type image_tensor --pipeline_config_path=E:/demo/training/ssd_mobilenet_v1_quantized_300x300_coco14_sync.config --trained_checkpoint_prefix E:/demo/training/model.ckpt-16438 --output_directory E:/demo/inference/ssd_v1_quant
```

## 📱 Converting to tflite

* 💁‍♀️ If you want to use the model in mobile apps or tflite supported embedded devices you have to convert `.pb` file to `.tflite` file

### 📙 About TFLite

* 📱 TensorFlow Lite is TensorFlow’s lightweight solution for mobile and embedded devices. 
* 🧐 It enables on-device machine learning inference with low latency and a small binary size.
* 😎 TensorFlow Lite uses many techniques for this such as quantized kernels that allow smaller and faster \(fixed-point math\) models.
* 📍 [**Official site**](https://www.tensorflow.org/lite)

**🍫 Converting Command**

* 💻 To apply converting open CMD and run:

```bash
# under (tf1) E:\>
# toco --graph_def_file=<PATH_TO_PB_FILE>
# --output_file=<PATH_TO_SAVE> --input_shapes=<INPUT_SHAPES>
# --input_arrays=<INPUT_ARRAYS> --output_arrays=<OUTPUT_ARRAYS>
# --inference_type=<QUANTIZED_UINT8|FLOAT> --change_concat_input_ranges=<true|false>
# --alow_custom_ops 
# args for QUANTIZED_UINT8 inference
# --mean_values=<MEAN_VALUES> std_dev_values=<STD_DEV_VALUES> 
toco --graph_def_file=E:\demo\inference\ssd_v1_quant\tflite_graph.pb --output_file=E:\demo\tflite\ssd_mobilenet.tflite --input_shapes=1,300,300,3 --input_arrays=normalized_input_image_tensor --output_arrays=TFLite_Detection_PostProcess,TFLite_Detection_PostProcess:1,TFLite_Detection_PostProcess:2,TFLite_Detection_PostProcess:3 --inference_type=QUANTIZED_UINT8 --mean_values=128 --std_dev_values=128 --change_concat_input_ranges=false --allow_custom_ops
```

## 🐞 Common Issues

### 🥅 nets module issue

`ModuleNotFoundError: No module named 'nets'`

This means that there is a problem in setting `PYTHONPATH`, try to run:

```bash
(tf1) E:\models\research>set PYTHONPATH=E:\models\research;E:\models\research\slim
```

### 🗃️ tf\_slim module issue

`ModuleNotFoundError: No module named 'tf_slim'`

This means that tf\_slim module is not installed, try to run:

```bash
(tf1) E:\models\research>pip install tf_slim
```

### 🗃️ Allocation error

```bash
2020-08-11 17:44:00.357710: I tensorflow/core/common_runtime/bfc_allocator.cc:929] Stats: 
Limit:                 10661327
InUse:                 10656704
MaxInUse:              10657688
NumAllocs:                 2959
MaxAllocSize:           3045064
```

For me it is fixed by minimizing batch\_size in `.config` file, it is related to your computations resources

```javascript
train_config: {
  ....
  batch_size: 128
  ....
}
```

### ❗ no such file or directory error

`train.py tensorflow.python.framework.errors_impl.notfounderror no such file or directory`

* 🙄 For me it was a typo in train.py command
* [📍 Related discussion 1](https://github.com/tensorflow/models/issues/3762)
* [📍 Related discussion 2](https://github.com/tensorflow/models/issues/3954)

### 🤯 LossTensor is inf issue

`LossTensor is inf or nan. : Tensor had NaN values`

* 👀 Related discussion is [**here**](https://github.com/tensorflow/models/issues/1881), it is common that it is an annotation problem
* 🙄 Maybe there is some bounding boxes outside the image boundaries
* 🤯 The solution for me was minimizing batch size in `.config` file

### 🙄 Ground truth issue

`The following classes have no ground truth examples`

* 👀 Related discussion is [**here**](https://github.com/tensorflow/models/issues/1936)
* 👩‍🔧 For me it was a misspelling issue in `label_map` file, 
* 🙄 Pay attention to small and capital letters

### 🏷️ labelmap issue

`ValueError: Label map id 0 is reserved for the background label`

* 👮‍♀️ id:0 is reserved for background, We can not use it for objects
* 🆔 start IDs from 1

### 🔦 No Variable to Save issue

`Value Error: No Variable to Save`

* 👀 Related solution is [**here**](https://ai.yemreak.com/tensorflow-object-detection-api/hata-notlari#value-error-no-variable-to-save)
* 👩‍🔧 Adding the following line to `.config` file solved the problem

```javascript
train_config: {
  ...
  fine_tune_checkpoint_type:  "detection"
  ...
}
```

### 🧪 pycocotools module issue

`ModuleNotFoundError: No module named 'pycocotools'`

{% tabs %}
{% tab title="💻 Windows" %}
* 👀 Related discussion is [**here**](https://github.com/tensorflow/models/issues/3367)
* 👩‍🔧 Applying the downloading instructions provided [**here**](https://github.com/philferriere/cocoapi) solved the problem for me \(on Windows 10\) 
{% endtab %}

{% tab title="🐧 Linux" %}
```bash
$ conda install -c conda-forge pycocotools
```
{% endtab %}
{% endtabs %}

### 🥴 pycocotools type error issue

`pycocotools typeerror: object of type cannot be safely interpreted as an integer.`

* 👩‍🔧 I solved the problem by editing the following lines in `cocoeval.py` script under _pycocotools_ package \(by adding casting\)
* 👮‍♀️ Make sure that you are editting the package in you env not in other env.

```python
self.iouThrs = np.linspace(.5, 0.95, int(np.round((0.95 - .5) / .05)) + 1, endpoint=True)
self.recThrs = np.linspace(.0, 1.00, int(np.round((1.00 - .0) / .01)) + 1, endpoint=True)
```

### 💣 Loss Exploding

```text
INFO:tensorflow:global step 440: loss = 2106942657570782838784.0000 (0.405 sec/step)
INFO:tensorflow:global step 440: loss = 2106942657570782838784.0000 (0.405 sec/step)
INFO:tensorflow:global step 441: loss = 7774169971762292326400.0000 (0.401 sec/step)
INFO:tensorflow:global step 441: loss = 7774169971762292326400.0000 (0.401 sec/step)
INFO:tensorflow:global step 442: loss = 25262924095336287830016.0000 (0.404 sec/step)
INFO:tensorflow:global step 442: loss = 25262924095336287830016.0000 (0.404 sec/step)
```

🙄 For me there were 2 problems:

**First:**

* Some of annotations were wrong and overflow the image \(e.g. xmax &gt; width\)
* I could check that by inspecting `.csv` file
* Example:

| filename | width | height | class | xmin | ymin | xmax | ymax |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 104.jpg | 640 | **480** | `class_1` | 284 | 406 | 320 | **492** |

**Second:**

* Learning rate in `.config` file is too big \(the default value was big 🙄\)
* The following values are valid and tested on `mobilenet_ssd_v1_quantized` \(Not very good 🙄\)

```javascript
learning_rate: {
  cosine_decay_learning_rate {
    learning_rate_base: .01
    total_steps: 50000
    warmup_learning_rate: 0.005
    warmup_steps: 2000
  }
}
```

* [👀 Related Discussion 1](https://github.com/tensorflow/models/issues/3868)
* [👀 Related Discussion 1](https://github.com/tensorflow/models/issues/8423)

### 🥴 Getting convolution Failure

```bash
Error : Failed to get convolution algorithm. This is probably because cuDNN failed to initialize, so try looking to see if a warning log message was printed above.
```

* It may be a _Cuda_ version incompatibility issue
* For me it was a memory issue and I solved it by adding the following line to `train.py` script

```python
os.environ['TF_FORCE_GPU_ALLOW_GROWTH'] = 'true'
```

* [👀 Related discussion](https://github.com/tensorflow/tensorflow/issues/24828)
* [📖 About memory growth](https://www.tensorflow.org/guide/gpu#limiting_gpu_memory_growth)

### 📦 Invalid box data error

```python
raise ValueError('Invalid box data. data must be a numpy array of '
ValueError: Invalid box data. data must be a numpy array of N*[y_min, x_min, y_max, x_max]
```

* 🙄 For me it was a logical error, in `test_labels.csv` there were some invalid values like: **`file123.jpg,134,63,3,0,0,-1029,-615`**
* 🏷 So, it was a labeling issue, fixing these lines solved the problem
* 👀 [Related discussion](https://github.com/tensorflow/models/issues/3527) 

### 🔄 Image with id  added issue

```python
raise ValueError('Image with id {} already added.'.format(image_id))
ValueError: Image with id 123.png already added.
```

* ☝ It is an issue in `.config` caused by giving value to `num_example` that is greater than total number of test image in test directory

```javascript
eval_config: {
  metrics_set: "coco_detection_metrics"
  use_moving_averages: false
  num_examples: 1265 // <--- this value was greater than total test images
}
```

## 🧐 References

* 📖 [Training Custom Object Detector](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html#)
* 📖 [TensorFlow Object Detection API](https://ai.yemreak.com/tensorflow-object-detection-api)
* 📖 [Custom Object Detection using TensorFlow from Scratch](https://towardsdatascience.com/custom-object-detection-using-tensorflow-from-scratch-e61da2e10087)
* 📖 [Supported object detection evaluation protocols](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/evaluation_protocols.md)

