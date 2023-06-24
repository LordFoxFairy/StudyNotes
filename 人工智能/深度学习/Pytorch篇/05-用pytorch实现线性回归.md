# 用pytorch实现线性回归

## 回归

* 线性模型

$$
\hat y = x \times w
$$

* 损失函数

$$
loss = (\hat y -y)^2 =(x\cdot w - y)^2
$$



![image-20210129163810184](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217798.png)

训练步骤：

![image-20210202210522318](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217799.png)

## 数据

在**PyTorch**中，计算图是小批量的，所以$X$和$Y$是$3 \times 1$张量。
$$
\begin{align}
\left[\begin{matrix}
y^{(1)}_{pred} \\
y^{(2)}_{pred} \\
y^{(3)}_{pred} \\
\end{matrix}\right]
= w \cdot \left[\begin{matrix}
x^{(1)} \\
x^{(2)} \\
x^{(3)} \\
\end{matrix}\right] + b
\end{align}
$$


​		

```
import torch
import numpy as np

data = np.array([
    [1.0,2.0],
    [2.0,4.0],
    [3.0,6.0]
])
data = torch.Tensor(data)
x_data,y_data = data[:,:-1],data[:,-1]
x_data,y_data
```

![image-20210202211414029](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217800.png)

## 设计模型

在以前的学习中，重点是求导数，现在学习**pytorch**后，**重点是如何构造计算图**。

```
class LinearModel(torch.nn.Module):
    def __init__(self,):
        super(LinearModel,self).__init__()
        self.linear = torch.nn.Linear(1,1)
        
    def forward(self,x):
        y_pred = self.linear(x)
        return y_pred
    
lm = LinearModel()
```

首先我们的模型类应该继承自`nn.Module`，它是所有神经网络模块的基类。

```
class LinearModel(torch.nn.Module):
	...
```

然后必须实现成员方法`__init__()`和`forward()`

```
class LinearModel(torch.nn.Module):
    def __init__(self,):
        super(LinearModel,self).__init__()
        ...
        
    def forward(self,x):
		...
```

构造[nn.Linear](https://pytorch.org/docs/stable/generated/torch.nn.Linear.html#torch.nn.Linear)对象，类`nn.Linear`包含了权重$w$和偏置$b$。

```
self.linear = torch.nn.Linear(1,1)
```

![image-20210202214515239](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217801.png)

类神经网络。`Linear`实现了神奇的`__call__()`方法，使类的实例可以像函数一样被调用，且通常会调用`forward()`。

```
    def forward(self,x):
        y_pred = self.linear(x) # 里面做了wx+b的运算
        return y_pred
```

## 损失函数和优化器

```
criterion = torch.nn.MSELoss(reduction='sum') # 损失函数
optimizer = torch.optim.SGD(lm.parameters(),lr=0.01) # 优化器
```

* 损失函数

![image-20210202220726331](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217802.png)

* [优化器](https://pytorch.org/docs/stable/optim.html)

![`image-20210202221212780`](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217803.png)

```
torch.optim.Adagrad
torch.optim.Adam
torch.optim.Adamax
torch.optim.ASGD
torch.optim.RMSprop
* torch.optim.Rprop
torch.optim.SGD
```

## 前馈与反馈

```
for epoch in range(100):
    y_pred = lm(x_data)
    loss = criterion(y_pred,y_data)
    print(epoch,loss)
    
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
```

> 注意:由于`.backward()`计算的级将被累积。所以在使用`backward`之前，请记住将`grad`设置为`0` !

* 输出权重与偏置

```
print("w=",lm.linear.weight.item())
print("b=",lm.linear.bias.item())
```

* 测试数据

```
x_test = torch.Tensor([[4.0]])
y_test = lm(x_test)
print("y_pred=",y_test.data)
```

![image-20210208221314294](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217804.png)

