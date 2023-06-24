# GNN的变体与框架

## 基本概念

作为深度学习与图数据结合的代表性方法，`GCN`的出现带动了将神经网络技术运用
于图数据的学习任务中去的一大类方法，为了给出一个涵盖更广范围的定义，一般我们统称这类方法为图神经网络，即`Graph Neural Networks（GNN）`。

## 图数据结构的两种“特征”

graph或者network的数据结构，通常是包含着顶点和边的关系。研究目标聚焦在顶点之上，边诉说着顶点之间的关系。

![preview](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201121617881.jpg)

**当然，除了图的结构之外，每个顶点还有自己的特征 $h_i$（通常是一个高维向量）。**它可以使社交网络中每个用户的个体属性；可以是生物网络中，每个蛋白质的性质；还可以使交通路网中，每个交叉口的车流量。

> **graph上的deep learning方法无外乎就是希望学习上面的两种特征。**

## GCN的局限性

GCN是处理transductive任务的一把利器（transductive任务是指：训练阶段与测试阶段都基于同样的图结构），然而GCN有**两大局限性**是经常被诟病的：

* **无法完成inductive任务，即处理动态图问题。**inductive任务是指：训练阶段与测试阶段需要处理的graph不同。通常是训练阶段只是在子图（subgraph）上进行，测试阶段需要处理未知的顶点。（unseen node）
* **处理有向图的瓶颈，不容易实现分配不同的学习权重给不同的neighbor**。

## GraphSAGE

### 作用

通过训练聚合节点邻居的函数（卷积层），使`GCN`扩展成归纳学习任务，对未知节点起到泛化作用。

> **直推式(transductive)学习**：从特殊到特殊，仅考虑当前数据。在图中学习目标是学习目标是直接生成当前节点的embedding，例如`DeepWalk`、`LINE`，把每个节点`embedding`作为参数，并通过`SGD`优化，又如`GCN`，在训练过程中使用图的拉普拉斯矩阵进行计算，
> **归纳(inductive)学习**：平时所说的一般的机器学习任务，从特殊到一般：目标是在未知数据上也有区分性。

### 区别

`GraphSAGE`从两个方面对`GCN`做了改动，一方面是通过采样邻居的策略将`GCN`由全图`（full batch）`的训练方式改造成以节点为中心的小批量`（mini batch`）训练方式，这使得大规模图数据的分布式训练成为可能；另一方面是该算法对聚合邻居的操作进行了拓展，提出了替换`GCN`操作的几种新的方式。

### 采样邻居

对于很多实际的业务场景数据而言，图的规模往往是十分巨大的，单张显卡的显存容量很难达到一整张图训练时所需的空间，为此采用小批量的训练方法对大规模图数据的训练进行分布式拓展是十分必要的。

而`GraphSAGE`从聚合邻居的操作出发，对邻居进行随机采样来控制实际运算时节点k阶子图的数据规模，在此基础上对采样的子图进行随机组合来完成小批量式的训练。

在GCN模型中知道**节点在第（k+1）层的特征只与其邻居在k层的特征有关**，这种局部性质使得节点在第k层的特征只与自己的k阶子图有关。对于图中的中心节点（橙色节点），假设GCN模型的层数为2，若要想得到其第2层特征，图中所有的节点都需要参与计算。

![image-20210412144738656](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201121617882.png)

虽然根据上述阐述，只需要考虑节点的k阶子图就可以完成对节点高层特征的计算，但是对于一个大规模的图数据来说，直接将此思路迁移过来仍然存在以下的**两个问题**：

1. 子图的节点数存在呈指数级增长的问题。
2. 真实世界中图数据节点的度往往呈现幂律分布，一些节点的度会非常大，并称这样的节点为超级节点，在很多图计算的问题中，超级节点都是比较难处理的对象。在
   这里，由于超级节点本身邻居的数目就很大，再加上子图节点数呈指数级增长的问题，这种类型节点高层特征计算的代价会变得更加高昂。

对于上述两种情况的出现，遍历子图的时间代价、模型训练的计算代价与存储代价都
会变得十分不可控。

为此，`GraphSAGE`使用了非常自然的采样邻居的操作来控制子图发散时的增长率。

具体做法如下：

**采样**的阶段首先选取一个点，然后随机选取这个点的一阶邻居，再以这些邻居为起点随机选择它们的一阶邻居。例如下图中，要预测 0 号节点，因此首先随机选择 0 号节点的一阶邻居 2、4、5，然后**随机**选择 2 号节点的一阶邻居 8、9；4 号节点的一阶邻居 11、12；5 号节点的一阶邻居 13、15。

![img](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201121617883.png)

### 聚合邻居

* 平均/加和聚合算子

$$
Agg^{sum} = \sigma(SUM\{Wh_j+b,\forall v_j\in N(v_i)\})
$$

* 池化聚合算子

$$
Agg^{pool} = MAX\{\sigma(Wh_j+b),\forall v_j\in N(v_i)\}
$$

### 算法过程

输入：$图G=（V，E）$；输入特征$\{x_v，∀v∈B\}$；层数$K$；权重矩阵$W^{(k)}$，$∀k∈\{1，…，K\}$；非线性函数$σ$；聚合操作$Agg^{(k)}$，$∀k∈\{1，…，K\}$；邻居采样函数$N^{(k)}：v→2^v，∀k∈\{1，…，K\}$。

输出：所有节点的向量表示$z_v$ ,$v∈B$。

![image-20210412151131387](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201121617884.png)

## GAT

### 作用

图神经网络 `GNN `把深度学习应用到图结构` (Graph) `中，其中的图卷积网络 `GCN `可以在 `Graph `上进行卷积操作。但是 `GCN `存在一些缺陷：依赖拉普拉斯矩阵，不能直接用于有向图；模型训练依赖于整个图结构，不能用于动态图；卷积的时候没办法为邻居节点分配不同的权重。

因此 2018 年图注意力网络` GAT (Graph Attention Network) `被提出，解决 `GCN `存在的问题。

`GAT `采用了 `Attention `机制，可以为不同节点分配不同权重，训练时依赖于成对的相邻节点，而不依赖具体的网络结构，可以用于 `inductive `任务。

### 注意力系数

如何计算注意力系数（attention coefficient）：对于顶点$i$，逐个计算它的所有邻居$(j \in N_i)$和它自己之间的相似系数，即$e_{ij}=a([Wh_i||Wh_j]),j\in N_i$。

其中，一个共享参数$W$的线性映射对于顶点的特征进行了增维（一种常见的特征增强方法）；$[\cdot][\cdot]$对于顶点$i,j$的变换后的特征进行了拼接；最后$a(\cdot)$把拼接后的高维特征映射到一个实数上。

显然学习顶点$i,j$之间的相关性，就是通过可学习的参数$W$和映射$a(\cdot)$完成的。

对于注意力系数进行归一化：
$$
\alpha_{ij} = \frac{\exp(LeakyReLU(e_{ij}))}{\sum_{k\in N_i}exp(LeakyReLU(e_{ik}))}
$$

### 加权求和

**根据计算好的注意力系数，把特征加权求和（aggregate）一下。**
$$
h'_i = \sigma(\sum_{j\in N_i}\alpha_{ij}Wh_j)
$$
其中，$h'_i$就是`GAT`输出的对于每个顶点$i$的新特征（融合了领域信息），$\sigma(\cdot)$是激活函数。

### 多注意头/multi-head attention

**multi-head attention也可以理解成用了ensemble的方法，毕竟convolution也得靠大量的卷积核才能大显神威！**
$$
h'_i(K) =  \underset{k=1}{\overset{K}{\parallel}} \sigma(\sum_{j\in N_i}\alpha_{ij}^kW^kh_j)
$$
![img](https://cdn.jsdelivr.net/gh/TheFoxFairy/ImgStg/202201121617885.jpg)

### GraphAttentionLayer

```
import numpy as np
import torch
import torch.nn.functional as F


class GraphAttentionLayer(torch.nn.Module):
    """
    简单的GAT layer
    """
    def __init__(self,in_features,out_features,dropout,alpha,concat=True):
        super(GraphAttentionLayer,self).__init__()
        
        self.in_features = in_features # 节点表示向量的输入特征维度
        self.out_features = out_features # 节点表示向量的输出特征维度
        self.dropout = dropout # dropout参数
        self.alpha = alpha # leakyrelu激活的参数
        self.concat = concat # 如果为true，在进行elu激活
        
        # 定义可训练参数，即论文中的W和a
        self.W = torch.nn.Parameter(torch.zeros(size=(in_features,out_features)))
        torch.nn.init.xavier_uniform_(self.W.data,gain=1.414)# xavier初始化
        
        self.a = torch.nn.Parameter(torch.zeros(size=(2*out_features,1)))
        torch.nn.init.xavier_uniform_(self.a.data,gain=1.414)# xavier初始化
        
        # relu的变体
        self.leakyrelu = torch.nn.LeakyReLU(self.alpha)
    
    def forward(self, h, adj):
        """
        h: h [N, in_features]  in_features表示节点的输入特征向量元素个数
        adj: 图的邻接矩阵  [N, N] 非零即一，数据结构基本知识
        """
        Wh = torch.mm(h, self.W)  # h.shape: (N, in_features), Wh.shape: (N, out_features)
        a_input = self._prepare_attentional_mechanism_input(Wh)  # (N,N,2*out_featues)
        e = self.leakyrelu(torch.matmul(a_input, self.a).squeeze(2))  # (N,N,1) => (N,N)
        
        zero_vec = -1e15 * torch.ones_like(e)  # 将没有连接的边置为负无穷
        attention = torch.where(adj > 0, e, zero_vec) # (N,N)
        # 表示如果邻接矩阵元素大于0时，则两个节点有连接，该位置的注意力系数保留，
        # 否则需要mask并置为非常小的值，原因是softmax的时候这个最小值会不考虑。
        attention = F.softmax(attention, dim=1)  # softmax形状保持不变 [N, N]，得到归一化的注意力权重！
        attention = F.dropout(attention, self.dropout, training=self.training)  # dropout，防止过拟合
        h_prime = torch.matmul(attention, h)  # [N, N].[N, out_features] => [N, out_features]
        if self.concat:
            return F.elu(h_prime)
        else:
            return h_prime

            
    def _prepare_attentional_mechanism_input(self,Wh):
        N = Wh.size()[0]
            
        # Wh_repeated_in_chunks.shape == Wh_repeated_alternating.shape == (N * N, out_features)
        Wh_repeated_in_chunks = Wh.repeat_interleave(N,dim=0)
        Wh_repeated_alternating = Wh.repeat(N,1)
            
        all_combinations_matrix = torch.cat([Wh_repeated_in_chunks,Wh_repeated_alternating],dim=1)
            
        return all_combinations_matrix.view(N,N,2*self.out_features)
```

### GAT

```
class GAT(torch.nn.Module):
    def __init__(self,nfeat,nhid,nclass,dropout,alpha,nheads):
        """Dense version of GAT
        n_heads 表示有几个GAL层，最后进行拼接在一起，类似self-attention
        从不同的子空间进行抽取特征。
        """
        super(GAT,self).__init__()
        self.dropout = dropout
        
        # 定义multi_head的图注意力层
        self.attentions = [GraphAttentionLayer(nfeat,nhid,dropout=dropout,
                                               alpha=alpha,concat=True) 
                           for _ in range(nheads)]
        for i,attention in enumerate(self.attentions):
            self.add_module('attention_{}'.format(i),attention)# 加入pytorch的Module模块
            
        # 输出层，也通过图注意力层来实现，可实现分类、预测等功能
        self.out_attention = GraphAttentionLayer(nhid*nheads,nclass,dropout=dropout,alpha=alpha,concat=False)
        
        
    def forward(self,x,adj):
        x = F.dropout(x,self.dropout,training=self.training) # dropout，防止过拟合
        x = torch.cat([att(x,adj) for att in self.attentions],dim=1) # 将每个head得到的表示进行拼接
        x = F.dropout(x,self.dropout,training=self.training) # dropout，防止过拟合
        x = F.elu(self.out_attention(x,adj)) # 输出并激活
        return F.log_softmax(x,dim=1)
```

### 参数配置

```
# Training settings

from types import SimpleNamespace


args = {
    'seed':42,
    'no_cuda':True,
    'fastmode':False, # Validate during training pass.
    'epochs':10000, # 步长
    'lr':0.005, # 学习率
    'weight_decay':5e-4, # 权重衰减（L2惩罚）（默认: 0）
    'hidden':8, # 隐藏层
    'dropout':0.5,
    'alpha':0.2,
    'nheads':8,
    'sparse':0,
}
# 将字典转换为对象
args = SimpleNamespace(**args)
# 检查cuda是否可用
args.cuda = not args.no_cuda and torch.cuda.is_available()
args
```

### 选择合适的GAT模型

```
model = None
# 模型和优化器
if args.sparse:
    model = SpGAT(nfeat=features.shape[1],
                    nhid=args.hidden,
                    nclass=labels.max().item()+1,
                    dropout=args.dropout,
                    nheads=args.nheads,
                    alpha=args.alpha
                   )
else:
    model = GAT(nfeat=features.shape[1],
                nhid=args.hidden,
                nclass=labels.max().item()+1,
                dropout=args.dropout,
                nheads=args.nheads,
                alpha=args.alpha
               )

optimizer = torch.optim.Adam(model.parameters(),
                          lr=args.lr,weight_decay=args.weight_decay)
```

### 迁移数据

```
if args.cuda: # 对model自身进行的内存迁移
    """
    model = model.cuda() 
    <=>
    model.cuda() 
    """
    model.cuda()
    features = features.cuda()
    adj = adj.cuda()
    labels = labels.cuda()
    idx_train = idx_train.cuda()
    idx_val = idx_val.cuda()
    idx_test = idx_test.cuda()
```

### 训练/测试

```
import time
import torch.nn.functional as F

# 准确率
def accuracy(output, labels):
    preds = output.max(1)[1].type_as(labels)
    correct = preds.eq(labels).double()
    correct = correct.sum()
    return correct / len(labels)

def train(epoch):
    t = time.time()
    """
    model.eval()，pytorch会自动把BN和DropOut固定住，不会取平均，而是用训练好的值。不然的话，一旦test的batch_size过小，很容易就会被BN层导致生成图片颜色失真极大；在模型测试阶段使用

    model.train() 让model变成训练模式，此时 dropout和batch normalization的操作在训练q起到防止网络过拟合的问题
    """
    model.train()
    optimizer.zero_grad()
    output = model(features,adj)
    loss_train = F.nll_loss(output[idx_train],labels[idx_train])
    acc_train = accuracy(output[idx_train],labels[idx_train])
    loss_train.backward()
    optimizer.step()
    
    
    if not args.fastmode:
        # Evaluate validation set performance separately,
        # deactivates dropout during validation run.
        model.eval()
        output = model(features, adj)
    
    loss_val = F.nll_loss(output[idx_val],labels[idx_val])
    acc_val = accuracy(output[idx_val],labels[idx_val])
    
    print('Epoch: {:04d}'.format(epoch+1),
          'loss_train: {:.4f}'.format(loss_train.item()),
          'acc_train: {:.4f}'.format(acc_train.item()),
          'loss_val: {:.4f}'.format(loss_val.item()),
          'acc_val: {:.4f}'.format(acc_val.item()),
          'time: {:.4f}s'.format(time.time() - t))
    
    return loss_val.data.item()


def test():
    model.eval()
    output = model(features,adj)
    loss_test = F.nll_loss(output[idx_test],labels[idx_test])
    acc_test = accuracy(output[idx_test],labels[idx_test])
    print("Test set results:",
          "loss= {:.4f}".format(loss_test.item()),
          "accuracy= {:.4f}".format(acc_test.item()))
    
t_total = time.time()
for epoch in range(args.epochs):
    train(epoch)
    test()

print("Optimization Finished!")
print("Total time elapsed: {:.4f}s".format(time.time() - t_total))
```

## 扩展阅读

* https://baidu-pgl.gz.bcebos.com/pgl-course/lesson_4.pdf
* https://qiniu.swarma.org/public/file/ppt/20190411102414.pdf
* [DGL博客|深入理解图注意力机制](https://zhuanlan.zhihu.com/p/57168713)

