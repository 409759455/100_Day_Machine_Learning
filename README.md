
### 此处为个人机器学习入门汇总
### 跟随100天机器学习计划安排
### 其中图片及代码
### English Edition请移步[Avik-Jain](https://github.com/Avik-Jain/100-Days-Of-ML-Code)
### 汉化版翻译小组请见[这里](https://github.com/MachineLearning100/100-Days-Of-ML-Code)

# 目录
- 有监督学习
  - [数据预处理](#数据预处理--第1天)
  - [简单线性回归](#简单线性回归--第2天)
  - [多元线性回归](#多元线性回归--第3天)
  - [逻辑回归](#逻辑回归--第4天)
  - [k近邻法(k-NN)](#k近邻法k-nn--第7天)
  - [支持向量机(SVM)](#支持向量机svm--第12天)
  - [决策树](#决策树--第23天)
  - [随机森林](#随机森林--第33天)
- 无监督学习
  - [K-均值聚类](#k-均值聚类--第43天)

## 数据预处理 | 第1天

<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%201.jpg">
</p>


如图所示，通过6步完成数据预处理。

## 第1步：导入库
```Python
import numpy as np
import pandas as pd
```
## 第2步：导入数据集
```python
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : , 3].values
```
## 第3步：处理丢失数据
```python
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = "NaN", strategy = "mean", axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
```
## 第4步：解析分类数据
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])
```
### 创建虚拟变量
```python
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
labelencoder_Y = LabelEncoder()
Y =  labelencoder_Y.fit_transform(Y)
```
## 第5步：拆分数据集为训练集合和测试集合
```python
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X , Y , test_size = 0.2, random_state = 0)
```
## 第6步：特征量化
```python
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.fit_transform(X_test)
```

## 简单线性回归模型 | 第2天

<p align="center">
  <img src="https://github.com/wengJJ/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%202.jpg">
</p>

# 第一步：数据预处理
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

dataset = pd.read_csv('studentscores.csv')
X = dataset.iloc[ : ,   : 1 ].values
Y = dataset.iloc[ : , 1 ].values

from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X, Y, test_size = 1/4, random_state = 0) 
```

# 第二步：训练集使用简单线性回归模型来训练
 ```python
 from sklearn.linear_model import LinearRegression
 regressor = LinearRegression()
 regressor = regressor.fit(X_train, Y_train)
 ```
 # 第三步：预测结果
 ```python
 Y_pred = regressor.predict(X_test)
 ```
 
 # 第四步：可视化 
 ## 训练集结果可视化
 ```python
 plt.scatter(X_train , Y_train, color = 'red')
 plt.plot(X_train , regressor.predict(X_train), color ='blue')
 plt.show()
 ```
 ## 测试集结果可视化
 ```python
 plt.scatter(X_test , Y_test, color = 'red')
 plt.plot(X_test , regressor.predict(X_test), color ='blue')
 plt.show()
 ``` 


## 多元线性回归 | 第3天

<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%203.png">
</p>

## 第1步: 数据预处理

### 导入库
```python
import pandas as pd
import numpy as np
```
### 导入数据集
```python
dataset = pd.read_csv('50_Startups.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : ,  4 ].values
```

### 将类别数据数字化
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder = LabelEncoder()
X[: , 3] = labelencoder.fit_transform(X[ : , 3])
onehotencoder = OneHotEncoder(categorical_features = [3])
X = onehotencoder.fit_transform(X).toarray()
```

### 躲避虚拟变量陷阱
```python
X = X[: , 1:]
```

### 拆分数据集为训练集和测试集
```python
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size = 0.2, random_state = 0)
```
## 第2步： 在训练集上训练多元线性回归模型
```python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, Y_train)
```

## Step 3: 在测试集上预测结果
```python
y_pred = regressor.predict(X_test)
```

## 逻辑回归 | 第4天
<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%204.jpg">
</p>

## 逻辑回归 | 第5天
深入研究逻辑回归到底是什么，以及它背后的数学是什么。学习如何计算代价函数，以及如何使用梯度下降法来将代价函数降低到最小。<br>


## 逻辑回归 | 第6天
[逻辑回归实现](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Code/Day%206_Logistic_Regression.md)

### 步骤1 | 数据预处理
#### 导入库

```python
import numpy as numpy
import matplotlib.pyplot as plt
import pandas as pd
```

#### 导入数据集
[这里](https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/datasets/Social_Network_Ads.csv)获取数据集 

```python
dataset = pd.read_csv('Social_Network_Ads.csv')
X = dataset.iloc[:, [2, 3]].values
Y = dataset.iloc[:,4].values
```

#### 将数据集分成训练集和测试集

```python
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, Y, test_size = 0.25, random_state = 0)
```

#### 特征缩放

```python
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.transform(X_test)
```

### 步骤2 | 逻辑回归模型

该项工作的库将会是一个线性模型库，之所以被称为线性是因为逻辑回归是一个线性分类器，这意味着我们在二维空间中，我们两类用户（购买和不购买）将被一条直线分割。然后导入逻辑回归类。下一步我们将创建该类的对象，它将作为我们训练集的分类器。

#### 将逻辑回归应用于训练集

```python
from sklearn.linear_model import LogisticRegression
classifier = LogisticRegression()
classifier.fit(X_train, y_train)
```

### 步骤3 | 预测

#### 预测测试集结果
```python
y_pred = classifier.predict(X_test)
```

### 步骤4 | 评估预测

我们预测了测试集。 现在我们将评估逻辑回归模型是否正确的学习和理解。因此这个混淆矩阵将包含我们模型的正确和错误的预测。

#### 生成混淆矩阵

```python
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_test, y_pred)
```

#### 可视化

![](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Other%20Docs/LR_training.png?raw=true)
![](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Other%20Docs/LR_test.png?raw=true) 


## K近邻法(k-NN) | 第7天
<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%207.jpg">
</p>

## 逻辑回归背后的数学 | 第8天
逻辑回归，Saishruthi Swaminathan的<a href = "https://towardsdatascience.com/logistic-regression-detailed-overview-46c4da4303bc">这篇文章</a><br>

它给出了逻辑回归的详细描述。请务必看一看。

## 支持向量机(SVM) | 第9天
直观了解SVM是什么以及如何使用它来解决分类问题。

## 支持向量机和K近邻法 | 第10天
了解更多关于SVM如何工作和实现knn算法的知识。

## K近邻法(k-NN) | 第11天

代码练习

## 导入相关库
```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
```

## 导入数据集
```python
dataset = pd.read_csv('Social_Network_Ads.csv')
X = dataset.iloc[:, [2, 3]].values
y = dataset.iloc[:, 4].values
```

## 将数据划分成训练集和测试集
```python
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 0)
```
## 特征缩放
```python
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test = sc.transform(X_test)
```
## 使用K-NN对训练集数据进行训练
```python
from sklearn.neighbors import KNeighborsClassifier
classifier = KNeighborsClassifier(n_neighbors = 5, metric = 'minkowski', p = 2)
classifier.fit(X_train, y_train)
```
## 对测试集进行预测
```python
y_pred = classifier.predict(X_test)
```

## 生成混淆矩阵
```python
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_test, y_pred)
```


## 支持向量机(SVM) | 第12天
<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%2012.jpg">
</p>

## 支持向量机(SVM) | 第13天
[SVM实现](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Code/Day%2013_SVM.md)

## 支持向量机(SVM)的实现 | 第14天
今天我在线性相关数据上实现了SVM。使用Scikit-Learn库。在scikit-learn中我们有SVC分类器，我们用它来完成这个任务。将在下一次实现时使用kernel-trick。Python代码见[此处](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Code/Day%2013_SVM.py),Jupyter notebook见[此处](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Code/Day%2013_SVM.ipynb)。

## 朴素贝叶斯分类器(Naive Bayes Classifier)和黑盒机器学习(Black Box Machine Learning) | 第15天
学习不同类型的朴素贝叶斯分类器同时开始<a href="https://bloomberg.github.io/foml/#home">Bloomberg</a>的课程。课程列表中的第一个是黑河机器学习。它给出了预测函数，特征提取，学习算法，性能评估，交叉验证，样本偏差，非平稳性，过度拟合和超参数调整的整体观点。

## 通过内核技巧实现支持向量机 | 第16天
使用Scikit-Learn库实现了SVM算法以及内核函数，该函数将我们的数据点映射到更高维度以找到最佳超平面。

## 在Coursera开始深度学习的专业课程 | 第17天
在1天内完成第1周和第2周内容以及学习课程中的逻辑回归神经网络。

## 继续Coursera上的深度学习专业课程 | 第18天
完成课程1。用Python自己实现一个神经网络。

## 学习问题和Yaser Abu-Mostafa教授 | 第19天
开始Yaser Abu-Mostafa教授的Caltech机器学习课程-CS156中的课程1。这基本上是对即将到来的课程的一种介绍。他也介绍了感知算法。

## 深度学习专业课程2 | 第20天
完成改进深度神经网络第1周内容：参数调整，正则化和优化。

## 网页搜罗 | 第21天
观看了一些关于如何使用Beautiful Soup进行网络爬虫的教程，以便收集用于构建模型的数据。

## 学习还可行吗? | 第22天
完成Yaser Abu-Mostafa教授的Caltech机器学习课程-CS156中的课程2。学习Hoeffding不等式。

## 决策树 | 第23天
<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%2023%20-%20Chinese.jpg">
</p>

## 统计学习理论的介绍 | 第24天
Bloomberg ML课程的第3课介绍了一些核心概念，如输入空间，动作空间，结果空间，预测函数，损失函数和假设空间。

## 决策树 | 第25天
[决策树实现](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Code/Day%2025_Decision_Tree.md)

## 跳到复习线性代数 | 第26天
发现YouTube一个神奇的频道[3Blue1Brown](https://www.youtube.com/channel/UCYO_jab_esuFRV4b17AJtAw)，它有一个播放列表《线性代数的本质》。看完了4个视频，包括了向量，线性组合，跨度，基向量，线性变换和矩阵乘法。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)。

## 跳到复习线性代数 | 第27天
继续观看了4个视频，内容包括三维变换、行列式、逆矩阵、列空间、零空间和非方矩阵。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)。

## 跳到复习线性代数 | 第28天
继续观看了3个视频，内容包括点积和叉积。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)。

## 跳到复习线性代数 | 第29天
观看了剩余的视频12到14，内容包括特征向量和特征值，以及抽象向量空间。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)。

## 微积分的本质 | 第30天
完成上一播放列表后，YouTube推荐了新内容《微积分的本质》，今天看完了其中的3个视频，包括导数、链式法则、乘积法则和指数导数。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr)。

## 微积分的本质 | 第31天
观看了2个视频，内容包括隐分化与极限。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr)。

## 微积分的本质 | 第32天
观看了剩余的4个视频，内容包括积分与高阶导数。

播放列表在[这里](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr)。

## 随机森林 | 第33天
<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%2033.png">
</p>

## 随机森林 | 第34天
[随机森林实现](https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Code/Day%2034_Random_Forests.md)

## K-均值聚类 | 第43天
转到无监督学习，并研究了聚类。可在[作者网站](http://www.avikjain.me/)查询。发现一个奇妙的[动画](http://shabal.in/visuals/kmeans/6.html)有助于理解K-均值聚类。
<p align="center">
  <img src="https://github.com/MachineLearning100/100-Days-Of-ML-Code/blob/master/Info-graphs/Day%2043.jpg">
</p>
