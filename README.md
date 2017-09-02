# Dogs vs. Cats

[A computation](https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition) from Kaggle and [a graduation project](https://github.com/nd009/capstone/tree/master/dog_vs_cat) for machine learning engineer nanodegree on Udacity 

在 `./output/` 文件夹中为该项目的输出文件，其中：

* `Dogs_vs._Cats.html` 项目代码及文档
* `proposal.pdf` 开题报告
* `report.pdf` 项目报告
* `model.zip` 解压后得到 `model.h5`, 本项目的模型

本项目使用 Python 在 Jupyter Notebook 环境下开发，并用到了如下的库：

```
import os
import random
import cv2
from matplotlib import pyplot
import numpy
from keras.models import Model
from keras.layers import Input, Dense, GlobalAveragePooling2D
from keras.applications.xception import Xception
from IPython.display import SVG
from keras.utils.vis_utils import model_to_dot
from keras.optimizers import Nadam
from keras.callbacks import EarlyStopping
```

其中, `cv2` 来自 OpenCV, 用于图片的读取、缩放等操作; `keras` 用于 CNN 深度学习模型的构建和训练。

用于训练 CNN 的[数据集](https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition/data)来自[猫狗大战](https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition)

在 AWS p2.xlarge 实例中（输出层微调）运行结果如下：

```
Train on 20000 samples, validate on 5000 samples
Epoch 1/10
20000/20000 [==============================] - 99s - loss: 0.3957 - acc: 0.8296 - val_loss: 0.5245 - val_acc: 0.7970
Epoch 2/10
20000/20000 [==============================] - 99s - loss: 0.2875 - acc: 0.8762 - val_loss: 0.6400 - val_acc: 0.7598
Epoch 3/10
20000/20000 [==============================] - 98s - loss: 0.2340 - acc: 0.8972 - val_loss: 0.3772 - val_acc: 0.8406
Epoch 4/10
20000/20000 [==============================] - 98s - loss: 0.1786 - acc: 0.9271 - val_loss: 0.3049 - val_acc: 0.8698
Epoch 5/10
20000/20000 [==============================] - 99s - loss: 0.1345 - acc: 0.9473 - val_loss: 0.4386 - val_acc: 0.8378
Epoch 6/10
20000/20000 [==============================] - 99s - loss: 0.0973 - acc: 0.9642 - val_loss: 0.3451 - val_acc: 0.8762
Epoch 7/10
20000/20000 [==============================] - 98s - loss: 0.0693 - acc: 0.9762 - val_loss: 0.4408 - val_acc: 0.8596
Epoch 8/10
20000/20000 [==============================] - 98s - loss: 0.0509 - acc: 0.9845 - val_loss: 0.4020 - val_acc: 0.8700
```

![](./img/loss.png)

发现训练集损失函数持续下降，但是验证集损失函数开始波动，所以及时停止训练，以防止过拟合。
