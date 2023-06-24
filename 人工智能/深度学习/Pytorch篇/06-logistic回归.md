# logistic回归

## 数据集

* 手写数字数据集

![image-20210226164852513](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070219173.png)

这个数据集：训练集有60000个样本，测试集有10000个样本，类别有10个。

```
import torchvision

# torchvision 是一个数据集集合的模块
## root设置数据集存放的路径，train表示是否下载训练集，download表示是否进行下载
train_set = torchvision.datasets.MNIST(root="./数据集/mnist",
					train=True,download=True)
test_set = torchvision.datasets.MNIST(root="./数据集/mnist",
					train=False,download=True)
```



* CIFAR-10 数据集

![image-20210226165735229](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070219175.png)

这个数据集：训练集有50000个样本，测试集有10000个样本，类别有10个。

```
import torchvision

# torchvision 是一个数据集集合的模块
## root设置数据集存放的路径，train表示是否下载训练集，download表示是否进行下载
train_set = torchvision.datasets.CIFAR10(root="./数据集/cifar10",
						train=True,download=True)
test_set = torchvision.datasets.CIFAR10(root="./数据集/cifar10",
						train=False,download=True)
```

## 激活函数

* sigmoid函数

$$
\sigma(x) = \frac{1}{1+e^{-x}}
$$

分类的结果是概率，结果需要在$[0,1]$中

其他的一些激活函数：
$$
\begin{align}
& 1.\ \ \mathbb{erf}(\frac{\sqrt{\pi}}{2}x) \\
& 2.\ \ \frac{x}{\sqrt{1+x^2}} \\
& 3.\ \ \tanh(x) \\
& 4.\ \ \frac{2}{\pi}\arctan(\frac{\pi}{2}x) \\
& 5.\ \ \frac{2}{\pi}\mathbb{gd}(\frac{\pi}{2}x) \\
& 6.\ \ \frac{x}{1+|x|}\\
\end{align}
$$

## logistic回归模型

* 定义模型

$$
\hat y = x*w + b
$$

* 逻辑回归模型

$$
\hat y = \sigma(x*w+b)
$$

* 线性单元

![image-20210226172204981](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070219176.png)

* 逻辑回归单元

![image-20210226172228412](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070219177.png)

## 损失函数

* 线性函数损失函数

$$
loss = (\hat y - y)^2 = (x*w-y)^2
$$

* 二分类损失函数

$$
loss = -(y\log{\hat y}+(1-y)\log{(1-\hat y)})
$$

* 小批量损失函数

$$
loss = -\frac{1}{N}\sum\limits_{n=1}^Ny_n\log{\hat y_n} + (1-y_n)\log{(1-\hat y_n)}
$$

## 对比

* 线性

![image-20210226173657175](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070219178.png)

```
import torch

class LinearModel(torch.nn.Module):
    
    def __init__(self,):
        super(LinearModel,self).__init__()
        self.linear = torch.nn.Linear(1,1)
        
    def forward(self,X):
        y_pred = self.linear(x)
        return y_pred
```

* 逻辑回归

```
class LogisticRegressionModel(torch.nn.Module):
    
    def __init__(self,):
        super(LogisitcRegressionModel,self).__init__()
        self.linear = torch.nn.Linear(1,1)
        
    def forward(self,X):
    	# 调用sigmoid激活函数
        y_pred = torch.sigmoid(self.linear(X))
        return y_pred
```

## 实现

* 步骤

1. 预处理数据
2. 设计模型并使用类`torch.nn.Module`
3. 构造损失函数和优化器
4. 训练数据

* 代码

```
x_data = torch.Tensor([
    [1.0],[2.0],[3.0]
])
y_data = torch.Tensor([
    [0],[0],[1]
])


class LogisticRegressionModel(torch.nn.Module):
    
    def __init__(self,):
        super(LogisticRegressionModel,self).__init__()
        self.linear = torch.nn.Linear(1,1)
        
    def forward(self,X):
        y_pred = torch.sigmoid(self.linear(X))
        return y_pred
    
    def fit(self,X,y):
        criterion = torch.nn.BCELoss(reduction='sum')
        optimizer = torch.optim.SGD(self.parameters(),lr=0.01)
        
        for epoch in range(1000):
            y_pred = self.forward(x_data)
            loss = criterion(y_pred,y)
            print(epoch,loss.item())
            
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()

model = LogisticRegressionModel()
model.fit(x_data,y_data)
```

* 测试

```
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,10,200)
x_t = torch.Tensor(x).view((200,1))
y_t = model(x_t)
y = y_t.data.numpy()

plt.plot(x,y)
plt.plot([0,10],[0.5,0.5],c='r')
plt.xlabel("Hours")
plt.ylabel("Probability of Pass")
plt.grid()
plt.show()
```

![image-20210227113654374](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070219179.png)

