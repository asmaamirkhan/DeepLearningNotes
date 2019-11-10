# 🚩 Region-Based CNNs

## 🔷 R-CNN _(Region Based Convoltional Neural Networks)_
It depends on:
- Selecting huge number of regions
- And then decrease them to 2000 by _selective search_
  - Each region is called a _region proposal_
- Extracting convolutional features from each region
- Finally checking if any object exists

### 👀 Visualization

<img src="../res/RCNN2.png" width="400"  />

<br/>

<img src="../res/RCNN.png" width="400"  />

### 🙄 Disadvantages
- It takes too many time to be trained.
- It can not be impelemented real time.

### 🤔 Why are they slow?
R-CNNs are very slow 🐢 beacause of:
- Extracting 2,000 regions for each image based on selective search
- Extracting features using CNN for every image region. 
  - If we have N images, then the number of CNN features will be N*2000 😢