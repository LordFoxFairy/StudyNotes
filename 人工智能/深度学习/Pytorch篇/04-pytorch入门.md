# 入门

## 安装

官网：[https://pytorch.org/](https://pytorch.org/)

![image-20210124204106500](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217942.png)

根据电脑的配置，自行选择，然后粘贴复制如下命令，进行安装：

```
conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch
```

## 什么是pytorch​？

`PyTorch`​是一个基于`python`​的科学计算包，主要针对两类人群：

- 作为`NumPy`​的替代品，可以利用$GPU$的性能进行计算
- 作为一个高灵活性、速度快的深度学习平台

### 张量

`Tensor`(张量）类似于`NumPy`的`ndarray`，但还可以在$GPU$上使用来加速计算。

```
from __future__ import print_function
import torch
import numpy as np
```

* 创建一个未初始化的$5\times 3$矩阵

```
x = torch.empty(5,3)
x
```

![image-20210124211644271](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217944.png)

* 创建一个随机矩阵

```
x = torch.rand(5,3)
x
```

![image-20210124211707075](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217945.png)

* 创建一个全为$0$，且数据类型为$long$的矩阵

```
x = torch.zeros(5,3,dtype=torch.long)
x
```

![image-20210124211916651](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217946.png)

* 将数据转化为张量

```
data = [
    [5,3],
    [2,6]
]
x = torch.tensor(data)
x
```

![image-20210124211855767](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217947.png)

```
data = np.array([
    [5,3],
    [2,6]
])
x = torch.tensor(data)
x
```

![image-20210124211905981](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217948.png)

* 根据已有的$tensor$建立新的$tensor$，除非用户提供新的值，否则这些方法将重用输入张量的属性

```
x = x.new_ones(5,3,dtype=torch.double) # new_* methods take in sizes
x
```

![image-20210124211947607](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217949.png)

```
x = torch.randn_like(x,dtype=torch.float)
x
```

![image-20210124212003400](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217950.png)

* 获取张量的形状

```
x.size()
```

![image-20210124212030942](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217951.png)

注意，`torch.Size`本质上还是`tuple`，所以支持`tuple`的一切操作。

### 运算

一种运算有多种语法。在下面的示例中，演示加法运算。

* 加法：形式一

```
y = torch.rand(5,3)
x+y
```

![image-20210124212212762](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217952.png)

* 加法：形式二

```
torch.add(x,y)
```

![image-20210124212233927](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217953.png)

* 给定一个输出张量作为参数

```
result = torch.empty(5,3)
torch.add(x,y,out=result)
result
```

![image-20210124212251903](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217954.png)

* 原地进行运算

```
y.add_(x)
y
```

![image-20210124212409762](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217955.png)

任何一个`in-place`改变张量的操作后面都固定一个`_`。例如`x.copy_(y)`、`x.t_()`将更改`x`

* 也可以使用像标准的`NumPy`一样的各种索引操作：

```
x[:,1]
```

![image-20210124212433198](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217956.png)

* 改变形状：如果想改变形状，可以使用`torch.view`

```
x = torch.rand(4,4)
y = x.view(16)
z = x.view(-1,8)
x.size(),y.size(),z.size()
```

![image-20210124212456197](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217957.png)

* 如果是仅包含一个元素的`tensor`，可以使用`.item()`来得到对应的`python`数值

```
x = torch.randn(1)
x,x.item()
```

![image-20210124212518425](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217958.png)

**超过100种tensor的运算操作，包括转置，索引，切片，数学运算， 线性代数，随机数等，具体访问[这里](https://pytorch.org/docs/stable/torch.html)。**

### 张量与`numpy`数组

将一个`Torch`张量转换为一个`NumPy`数组是轻而易举的事情，反之亦然。

`Torch`张量和`NumPy`数组将共享它们的底层内存位置，因此当一个改变时,另外也会改变。

#### 将`torch`的`Tensor`转化为`NumPy`数组

```
a = torch.ones(5)
a
```

![image-20210124212730718](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217959.png)

```
b = a.numpy()
b
```

![image-20210124212742717](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217960.png)

* 看NumPy数组是如何改变里面的值的：

```
a.add_(1)
a,b
```

![image-20210124212807543](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217961.png)

#### 将`NumPy`数组转化为`Torch`张量
看改变`NumPy`数组是如何自动改变`Torch`张量的：

```
a = np.ones(5)
b = torch.from_numpy(a)
np.add(a,1,out=a)
a,b
```

![image-20210124212851937](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217962.png)

`CPU`上的所有张量(`CharTensor`除外)都支持与`Numpy`的相互转换。

#### CUDA上的张量

张量可以使用`.to`方法移动到任何设备(`device`）上：

```
# 当GPU可用时,可以运行以下代码
# 将使用`torch.device`来将tensor移入和移出GPU

if torch.cuda.is_available():
    device = torch.device("cuda") # CUDA设备对象
    y = torch.ones_like(x,device=device) # 直接在GPU上创建tensor
    x = x.to(device) # 或者使用'.to("cuda")'方法
    z = x+y
    print(z)
    print(z.to("cpu",torch.double)) # '.to'也能在移动时改变dtype
```

![image-20210124212940838](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217963.png)

## Autograd：自动求导

`PyTorch`中，所有神经网络的核心是 `autograd` 包。先简单介绍一下这个包，然后训练第一个神经网络。

`autograd` 包为张量上的所有操作提供了自动求导机制。它是一个在运行时定义(define-by-run）的框架，这意味着反向传播是根据代码如何运行来决定的，并且每次迭代可以是不同的.

### 张量

**`torch.Tensor` 是这个包的核心类。如果设置它的属性 `.requires_grad` 为 `True`，那么它将会追踪对于该张量的所有操作。当完成计算后可以通过调用 `.backward()`，来自动计算所有的梯度。这个张量的所有梯度将会自动累加到`.grad`属性.**

**要阻止一个张量被跟踪历史，可以调用 `.detach()` 方法将其与计算历史分离，并阻止它未来的计算记录被跟踪。**

为了防止跟踪历史记录(和使用内存），可以将代码块包装在 `with torch.no_grad():` 中。在评估模型时特别有用，因为模型可能具有 `requires_grad = True` 的可训练的参数，但是我们不需要在此过程中对他们进行梯度计算。

还有一个类对于`autograd`的实现非常重要：`Function`。

`Tensor` 和 `Function` 互相连接生成了一个无圈图(acyclic graph)，它编码了完整的计算历史。每个张量都有一个 `.grad_fn` 属性，该属性引用了创建 `Tensor` 自身的`Function`(除非这个张量是用户手动创建的，即这个张量的 `grad_fn` 是 `None` )。

如果需要计算导数，可以在 `Tensor` 上调用 `.backward()`。如果 `Tensor` 是一个标量(即它包含一个元素的数据），则不需要为 `backward()` 指定任何参数，但是如果它有更多的元素，则需要指定一个 `gradient` 参数，该参数是形状匹配的张量。

```
import torch
import numpy as np
```

* 创建一个张量并设置requires_grad=True用来追踪其计算历史

```
x = torch.ones(2,2,requires_grad=True)
x
```

![image-20210125144530231](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217964.png)

* 对这个张量做一次运算：

```
y = x + 2
y
```

![image-20210125144555667](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217965.png)

* 对y进行更多操作

```
z = y*y*3
out = z.mean()
z,out
```

![image-20210125144657578](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217966.png)

* `.requires_grad_(...) `原地改变了现有张量的 `requires_grad `标志。如果没有指定的话，默认输入的这个标志是 `False`。

```
a = torch.randn(2,2)
a = ((a*3)/(a-1))
print(a.requires_grad)
a.requires_grad_(True)
print(a.requires_grad)
b = (a*a).sum()
print(b.grad_fn)
```

![image-20210125144714008](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217967.png)

### 梯度
现在开始进行反向传播，因为 `out `是一个标量，因此 `out.backward()` 和` out.backward(torch.tensor(1.)) `等价。

```
out.backward()
```

输出导数` d(out)/dx`

```
x.grad
```

![image-20210125144820261](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217968.png)

我们的得到的是一个数取值全部为`4.5`的矩阵。

如上可以得到，$o=\frac{1}{4}\sum_iz_i$，$z_i=3(x_i+2)^2$，因此，$\frac{\partial o}{\partial x_i}=\frac{3}{2}(x_i+2)$。

可以通过将代码块包装在 `with torch.no_grad():` 中，来阻止autograd跟踪设置了 `.requires_grad=True` 的张量的历史记录。

```
print((x**2).requires_grad)
with torch.no_grad():
    print((x**2).requires_grad)
```

![image-20210125145656102](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201070217969.png)

