<h1>TECHNOLOGIES AND INFRASTRUCTURE FOR BIG DATA COURSE PROJECT</h1>

Author: <a href='https://github.com/mdvdv'>Anatoly Medvedev</a>

Group: J4322c

<h2>TOOLS</h2>

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)

<h2>MAIN</h2>

1. We used `PyTorch` framework to load and fine-tune pretrained model, `Catalyst` framework to speed up the model training process and `FlickrAPI` to connect to the www.flickr.com database API.  We also used `PySpark` interface to access `Pandas` API through `Apache Spark` framework. This allowed us to store, access and pre-process data with high speed and optimization.

```python
from catalyst import dl
import flickrapi
import torch
import torch.nn as nn
from torch.utils.data import Dataset
import torchvision
import pyspark.pandas as ps

import numpy as np
import pandas as pd
import pylab
from sklearn.model_selection import train_test_split
import seaborn as sns
import time
from tqdm import tqdm
import urllib.request
from skimage import io, transform
```

2. Before we start parsing data, we have received key and secret code to connect to the API. You can get your own key in the Developers section of www.flickr.com or use ours.

```python
API_KEY = '809322371031dd7403805902a5aaddd1'
API_SECRET = '01590df66d97c93d'
```

3. We bring to your attention solution to the problem of classifying land transport in 10 categories: `bicycle`, `bus`, `car`, `excavator`, `motorbike`, `scooter`, `snowmobile`, `train`, `truck`, `wagon`. To begin with, we created a directory in which our data set will be located.

The final directory looks like this:
```
dataset/
       |
       bicycle/
       |      |
       |      0.jpg
       |      ...
       bus/
       ...
```

4. We used `ResNet-18` model pre-trained on ImageNet dataset. To work with it, we frozed model layers, except for the batch normalization and the last two convolutional layers. This allowed us to use the experience of ImageNet training and at the same time to teach model to find high-frequency features on our images. The output of model is 10 neurons.

In order to increase the efficiency of training, we used augmentation close to ImageNet. We applied image resizing to 224×224 size and normalization of pixel intensity values. The size of the training and test samples were 75% and 25% of the total set, respectively.

5. We validated model on the first batch of the test set and visualized prediction of the model. The final accuracy of the model after 25 training epochs was `99.9%` on the training set and `94.8%` on the test one.

![image](https://user-images.githubusercontent.com/83948828/179053138-badbe70e-be8d-475b-a7be-d1d8673d4490.png)
