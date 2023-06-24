## Pandas

### 什么是Pandas？

基于 NumPy 的一种工具，该工具是为了解决数据分析任务而创建的。Pandas 纳入了大量库和一些标准的数据模型，提供了高效地操作大型数据集所需的工具。

### 与Numpy的区别？

* Pandas是专门为处理表格和混杂数据设计的

* NumPy更适合处理统一的数值数组数据

### 数据结构

Pandas中的主要数据结构有两个：`Series`和`DataFrame`

* Series是一种类似于一维数组（Python中的list）的对象，由一组数据和一组索引（下标）两部分组成。Series可以保存任何数据类型。
* DataFrame是一个二维的表格型数据结构，可以把它想象成是一个Excel表格来理解，既有行索引，也有列索引。其中每列可以是不同的值类型。
* Index也是比较常见的数据结构，虽然没有前两者那么重要，但也是必不可少的。

### 创建数据结构对象

#### Series

##### 初步

* 由相同元素类型构成的一维数据结构
* 具有列表和字典的特点

In [1]:

```
import numpy as np
import pandas as pd
from pandas import Series
from pandas import DataFrame
```

In [2]:

```
data = [i for i in range(1,6)]
index = ['a','b','c','d','f']
s = Series(data,index=index)
s
```

Out[2]:

```
a    1
b    2
c    3
d    4
f    5
dtype: int64
```

In [3]:

```
s.index
```

Out[3]:

```
Index(['a', 'b', 'c', 'd', 'f'], dtype='object')
```

In [4]:

```
s.name
```

In [5]:

```
s.values
```

Out[5]:

```
array([1, 2, 3, 4, 5], dtype=int64)
```

In [6]:

```
s.shape
```

Out[6]:

```
(5,)
```

##### 创建

```
Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)
```

###### 无索引创建

* data为ndarray或list，则其缺少Series需要索引信息
* 提供index，必须与data长度相同
* 若不提供，则Series会自动生成默认数值索引range(0,data.shape[0])

In [7]:

```
data1 = [1,2,3]
data2 = np.array([1,2,3])
index = ['a','b','c']

s1 = Series(data1,index=index)
s2 = Series(data2,index=index)
s3 = Series(data1)
```

In [8]:

```
s1
```

Out[8]:

```
a    1
b    2
c    3
dtype: int64
```

In [9]:

```
s2
```

Out[9]:

```
a    1
b    2
c    3
dtype: int32
```

In [10]:

```
s3
```

Out[10]:

```
0    1
1    2
2    3
dtype: int64
```

###### 有索引创建

* 如果 data 为 **Series 或 dict** ，那么其已经提供了 Series 需要的索引信息，所以 index 项是不需要提供的
* 如果额外提供了 index 项，那么其将对当前构建的Series进行覆盖

In [11]:

```
data = {
    'a':1,
    'b':2,
    'c':3,
}
index = ['e','f','g']

s1 = Series(data=data)
```

In [12]:

```
s1
```

Out[12]:

```
a    1
b    2
c    3
dtype: int64
```

In [13]:

```
s1.index = index
```

In [14]:

```
s1
```

Out[14]:

```
e    1
f    2
g    3
dtype: int64
```

#### DataFrame

##### 初步

* 具有共同索引的Series按排列构成（二维矩阵）
* 类似于Excel表格

In [15]:

```
data = [
    [1,2,3],
    [4,5,6]
]
index = ['a','b']
columns = ['A','B','C']
df = DataFrame(data=data,index=index,columns=columns)
df
```

Out[15]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

In [16]:

```
df.index # 行索引
```

Out[16]:

```
Index(['a', 'b'], dtype='object')
```

In [17]:

```
df.columns # 列索引
```

Out[17]:

```
Index(['A', 'B', 'C'], dtype='object')
```

In [18]:

```
df.values
```

Out[18]:

```
array([[1, 2, 3],
       [4, 5, 6]], dtype=int64)
```

In [19]:

```
df.shape
```

Out[19]:

```
(2, 3)
```

In [20]:

```
df.dtypes # 数据类型
```

Out[20]:

```
A    int64
B    int64
C    int64
dtype: object
```

##### 创建

```
DataFrame(data=None, index=None, columns=None)
```

> 函数由多个参数，主要参数：data,index和columns

###### data无行索引、无列索引

- 如果 data 为 **ndarray(2D) or list(2D)**，那么其缺少 DataFrame 需要的行、列索引信息
- 如果提供 index 或 columns 项，其必须和data的行 或 列长度相同
- 如果不提供 index 或 columns 项，那么其将默认生成数值索引range(0, data.shape[0])) 或 range(0, data.shape[1])。

In [21]:

```
data = np.array([
    [1,2,3],
    [4,5,6]
])
index = ['a','b']
columns = ['A','B','C']
df = DataFrame(data,index=index,columns=columns)
df
```

Out[21]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

###### data无 行索引，有 列索引

- 如果data为 **dict of ndarray(1D) or list(1D)**，所有ndarray或list的长度必须相同。且dict的key为DataFrame提供了需要的columns信息，缺失index
- 如果提供 index 项，必须和list的长度相同
- 如果不提供 index，那么其将默认生成数值索引range(0, data.shape[0]))
- 如果还额外提供了columns项，那么其将对当前构建的DataFrame进行 **列重索引**

In [22]:

```
data = {'A':[1,4],'V':[4,5],'C':[6,7]}
index = ['a','b']
columns = ['A','B','C']
df = DataFrame(data,)
df
```

Out[22]:

|      |    A |    V |    C |
| ---: | ---: | ---: | ---: |
|    0 |    1 |    4 |    6 |
|    1 |    4 |    5 |    7 |

In [23]:

```
df.columns = columns
df
```

Out[23]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    0 |    1 |    4 |    6 |
|    1 |    4 |    5 |    7 |

###### data有 行索引，有 列索引

- 如果data为 **dict of Series or dict**，那么其已经提供了DataFrame需要的所有信息
- 如果多个Series或dict间的索引不一致，那么取并操作（pandas不会试图丢掉信息），缺失的数据填充NaN
- 如果提供了index项或columns项，那么其将对当前构建的DataFrame进行 重索引（reindex，pandas内部调用接口）

In [24]:

```
data1 = {'A':pd.Series([1,4],index=['a','b']),'V':pd.Series([4,5],index=['a','b']),'C':pd.Series([6,7],index=['a','c'])}
df1 = pd.DataFrame(data1)
df1
```

Out[24]:

|      |    A |    V |    C |
| ---: | ---: | ---: | ---: |
|    a |  1.0 |  4.0 |  6.0 |
|    b |  4.0 |  5.0 |  NaN |
|    c |  NaN |  NaN |  7.0 |

In [25]:

```
data2 = {'A':{'a':1,'b':2},'V':{'a':4,'b':5},'C':{'a':7,'':8}}
df2 = pd.DataFrame(data2)
df2
```

Out[25]:

|      |    A |    V |    C |
| ---: | ---: | ---: | ---: |
|    a |  1.0 |  4.0 |  7.0 |
|    b |  2.0 |  5.0 |  NaN |
|      |  NaN |  NaN |  8.0 |

#### 读取文件

##### CSV文件

```
pd.read_csv(filepath_or_buffer, sep=',', header='infer', names=None, index_col=None, encoding=None )
```

- filepath_or_buffer：路径和文件名不要带中文，带中文容易报错
- sep: csv文件数据的分隔符，默认是','，根据实际情况修改
- header：如果有列名，那么这一项不用改
- names：如果没有列名，那么必须设置header = None， names为列名的列表，不设置默认生成数值索引
- index_col：int型，选取这一列作为索引
- encoding：根据你的文档编码来确定，如果有中文读取报错，试试encoding = 'gbk'

这里采用手动创建数据

```
import pandas as pd

# 初始数据集: 婴儿名字和出生率
names = ['Bob','Jessica','Mary','John','Mel']
births = [968, 155, 77, 578, 973]

BabyDataSet = list(zip(names, births))

df = pd.DataFrame(data = BabyDataSet, columns=['Names', 'Births'])
df
```

Out[1]:

|      |   Names | Births |
| ---: | ------: | -----: |
|    0 |     Bob |    968 |
|    1 | Jessica |    155 |
|    2 |    Mary |     77 |
|    3 |    John |    578 |
|    4 |     Mel |    973 |

###### 导出数据为csv格式

```
df.to_csv(filename, index, header)
```

> 将这两个参数设置为 `False` 将会防止索引(index)和列名(header names)被导出到文件中

In [2]:

```
df.to_csv('birthday.csv', index=False, header=False) # 将数据转化为csv文件
```

###### 导入csv数据

In [3]:

```
df = pd.read_csv('./birthday.csv') 
df
```

Out[3]:

|      |     Bob |  968 |
| ---: | ------: | ---: |
|    0 | Jessica |  155 |
|    1 |    Mary |   77 |
|    2 |    John |  578 |
|    3 |     Mel |  973 |

> 会发现列名不正确，是错误的，需要进行调整，将header设置为None即可，想要设置自定义列名，需要通过names参数进行设置

In [4]:

```
df = pd.read_csv('./birthday.csv',header=None)
df
```

Out[4]:

|      |       0 |    1 |
| ---: | ------: | ---: |
|    0 |     Bob |  968 |
|    1 | Jessica |  155 |
|    2 |    Mary |   77 |
|    3 |    John |  578 |
|    4 |     Mel |  973 |

In [5]:

```
df = pd.read_csv('./birthday.csv',header=None, names=['Names', 'Births'])
df
```

Out[5]:

|      |   Names | Births |
| ---: | ------: | -----: |
|    0 |     Bob |    968 |
|    1 | Jessica |    155 |
|    2 |    Mary |     77 |
|    3 |    John |    578 |
|    4 |     Mel |    973 |

###### 

##### Excel文件

```
pd.read_excel(io, sheetname=0, header=0, index_col=None, names=None)
```

- io：文件地址
- sheetname：表格的sheet窗口名称
- header：如果有列名，那么这一项不用改；
- names：如果没有列名，那么必须设置header = None， names为列名的列表，不设置默认生成数值索引；
- index_col：int型，选取这一列作为索引。

###### 导出数据为xls格式

* 用法与to_csv类似

> 注意运用index，header参数去掉索引和列名

In [6]:

```
df.to_excel('birthday.xls', index=False)
```

###### 导入excel数据

In [7]:

```
df = pd.read_excel('birthday.xls')
df
```

Out[7]:

|      |   Names | Births |
| ---: | ------: | -----: |
|    0 |     Bob |    968 |
|    1 | Jessica |    155 |
|    2 |    Mary |     77 |
|    3 |    John |    578 |
|    4 |     Mel |    973 |

### 增删查改

#### Series

In[1]:

```
import numpy as np
import pandas as pd

s = pd.Series(data=[1,2,3],index=['a','b','c'])
s
```

Out[1]:

```
a    1
b    2
c    3
dtype: int64
```

##### 通过索引与切片进行查询

In [2]:

```
s['a'] # 通过索引返回目标值
```

Out[2]:

```
1
```

In [3]:

```
s[0:2] # 范围，左闭右开
```

Out[3]:

```
a    1
b    2
dtype: int64
```

In [4]:

```
s['a':'c'] # 注意与上不同，左右均为闭区间
```

Out[4]:

```
a    1
b    2
c    3
dtype: int64
```

In [5]:

```
s[[0,2]] # 通过列表，返回多个值
```

Out[5]:

```
a    1
c    3
dtype: int64
```

In [6]:

```
s[['a','c']] # 通过自定义索引，进行查询，返回多个值
```

Out[6]:

```
a    1
c    3
dtype: int64
```

In [7]:

```
s[[True,False,True]] # 类似于列表，返回该列表为真的相同下标的值
```

Out[7]:

```
a    1
c    3
dtype: int64
```

##### 通过iloc与loc进行查询

* loc查询方式与上述相同
* iloc查询无视索引，只根据位置定位

###### 基于索引--loc

In [8]:

```
s.loc['b'] # <==> s['b']，返回索引位置的目标值
```

Out[8]:

```
2
```

In [9]:

```
s.loc['a':'c'] # <==> s['a':'c']
```

Out[9]:

```
a    1
b    2
c    3
dtype: int64
```

In [10]:

```
s.loc[['a','c']] # <==> s[['a','c']]
```

Out[10]:

```
a    1
c    3
dtype: int64
```

In [11]:

```
s.loc[[True,False,True]] # s[[True,False,True]] 
```

Out[11]:

```
a    1
c    3
dtype: int64
```

###### 基于位置--iloc 

In [12]:

```
s
```

Out[12]:

```
a    1
b    2
c    3
dtype: int64
```

In [13]:

```
s.iloc[1] #　根据下标位置进行查询 <==> s[1]
```

Out[13]:

```
2
```

In [14]:

```
s.iloc[0:2] # 切片 <==> s[0:2]
```

Out[14]:

```
a    1
b    2
dtype: int64
```

In [15]:

```
s.iloc[[0,2]] # 切片 <==> 列表,s[[0,2]] 
```

Out[15]:

```
a    1
c    3
dtype: int64
```

In [16]:

```
s.iloc[[False, True, False]] # 切片 <==> 列表,s[[False, True, False]] 
```

Out[16]:

```
b    2
dtype: int64
```

##### 修改数值

* 直接赋值

In[1]:

```
import pandas as pd
import numpy as np

s = pd.Series(data=np.array([1,2,3,4]),index=['a','b','c','d'])
s
```

Out[1]:

```
a    1
b    2
c    3
d    4
dtype: int32
```

In [2]:

```
s1 = s.copy()
s1['a'] = 1000
s1
```

Out[2]:

```
a    1000
b       2
c       3
d       4
dtype: int32
```

In [3]:

```
s1[0:2] = 10
s1
```

Out[3]:

```
a    10
b    10
c     3
d     4
dtype: int32
```

* 通过replace函数修改

```
Series.replace(to_replace=None, value=None, inplace=False)
```

- to_replace：要修改的值，可以为列表
- value：改为的值，可以为列表，与to_repalce要匹配
- inplace：是否在原地修改

In [5]:

```
s2 = s1.replace(to_replace=10,value=1000)
s2
```

Out[5]:

```
a    1000
b    1000
c       3
d       4
dtype: int32
```

In [6]:

```
s2 = s1.replace(to_replace=[10,3],value=1000)
s2
```

Out[6]:

```
a    1000
b    1000
c    1000
d       4
dtype: int32
```

##### 修改索引

* 通过index进行修改

In [7]:

```
s1.index = ['q','w','e','r']
s1
```

Out[7]:

```
q    10
w    10
e     3
r     4
dtype: int32
```

* 通过rename函数修改

```
Series.rename(index=None, level = None, inplace = False)
```

- index：list or dict，list时必须和已有索引长度相同，dict可以部分修改
- level：多重索引时，可以指定修改哪一重，从0开始递增
- inplace：是否原地修改

In [9]:

```
s1.rename(index={'q':'f'},inplace=False)
```

Out[9]:

```
f    10
w    10
e     3
r     4
dtype: int32
```

##### 添加数据

* 增加一行

In [10]:

```
s2 = s.copy()
s2['e'] = 5
s2
```

Out[10]:

```
a    1
b    2
c    3
d    4
e    5
dtype: int64
```

* 增加多行

```
Series.append(to_append, ignore_index=False, verify_integrity=False)
```

- to_append: 另一个series或多个Series构成的列表；
- ignore_index：False-保留原有索引，True-清除所有索引，生成默认数值索引；
- verify_integrity：True的情况下，如果to_append索引与当前索引有重复，则报错。

In [11]:

```
s3 = pd.Series(data=[25,26],index=['h','j'])
s2.append(s3,ignore_index=False)
```

Out[11]:

```
a     1
b     2
c     3
d     4
e     5
h    25
j    26
dtype: int64
```

##### 删除数据

* 删除一行数据

In [14]:

```
s = pd.Series(np.arange(4),index=['a','b','c','d'])
s2 = s.drop('a')
s2
```

Out[14]:

```
b    1
c    2
d    3
dtype: int32
```

* 删除多行数据

```
Series.drop(labels, level=None, inplace=False)
```

- labels：索引，单索引或索引的列表；
- level：多重索引需要设置；
- inplace：是否本地修改。

In [15]:

```
s.drop(['b','c'])
```

Out[15]:

```
a    0
d    3
dtype: int32
```

#### DataFrame

In[1]:

```
import pandas as pd
import numpy as np

data = np.array([
    [1,2,3],
    [4,5,6]
])
index = ['a','b']
columns = ['A','B','C']
df = pd.DataFrame(data=data,index=index,columns=columns)
df
```

Out[1]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

#####　通过索引与切片进行查询

* 通过列索引--查询单个值

In [2]:

```
df['A']
```

Out[2]:

```
a    1
b    4
Name: A, dtype: int32
```

* 通过列索引--查询多个值

In [3]:

```
df[['A','C']]
```

Out[3]:

|      |    A |    C |
| ---: | ---: | ---: |
|    a |    1 |    3 |
|    b |    4 |    6 |

* 查询第几行--行范围

In [4]:

```
df[:1]
```

Out[4]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |

* 通过布尔值，返回需要的行

In [5]:

```
df[[False,True]]
```

Out[5]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    b |    4 |    5 |    6 |

* 通过行索引查询

In [6]:

```
df['a':'b']
```

Out[6]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

* 通过条件筛选查询

In [7]:

```
df[df>4]
```

Out[7]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |  NaN |  NaN |  NaN |
|    b |  NaN |  5.0 |  6.0 |

##### 基于索引查询--loc

* 查询单值

In [9]:

```
df.loc['b','B']
```

Out[9]:

```
5
```

* 查询多值，通过行索引以及列索引筛选需要的值

In [10]:

```
df.loc['a':'b','A']
```

Out[10]:

```
a    1
b    4
Name: A, dtype: int32
```

In [11]:

```
df.loc['a','A':'B']
```

Out[11]:

```
A    1
B    2
Name: a, dtype: int32
```

In [12]:

```
df.loc[['a','b'],'B']
```

Out[12]:

```
a    2
b    5
Name: B, dtype: int32
```

In [13]:

```
df.loc[[True,True,],'B']
```

Out[13]:

```
a    2
b    5
Name: B, dtype: int32
```

##### 基于位置查询--iloc

* 查询单个值

In [14]:

```
df
```

Out[14]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

In [15]:

```
df.iloc[1,1]
```

Out[15]:

```
5
```

In [16]:

```
df.iloc[0,0]
```

Out[16]:

```
1
```

* 查询多个值：第一个参数为行，第二个参数为列，均可为列表

In [20]:

```
df.iloc[[0,1],[1,2]]
```

Out[20]:

|      |    B |    C |
| ---: | ---: | ---: |
|    a |    2 |    3 |
|    b |    5 |    6 |

##### 修改数值

* 直接修改

In [18]:

```
df1 = df.copy()
df1.loc['a','A'] = 1000
df1
```

Out[18]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a | 1000 |    2 |    3 |
|    b |    4 |    5 |    6 |

* 通过replace修改

  ```
  DataFrame.replace(to_replace=None, value=None, inplace=False)
  ```

  * to_replace：要修改的值，可以为列表
  * value：改为的值，可以为列表，与to_repalce要匹配
  * inplace：是否在原地修改

  In [19]:

  ```
  df1.replace(to_replace=1000,value=5555,inplace=False)
  ```

  Out[19]:

  |      |    A |    B |    C |
  | ---: | ---: | ---: | ---: |
  |    a | 5555 |    2 |    3 |
  |    b |    4 |    5 |    6 |

* 交换行列

In [20]:

```
df1[['A','B']] = df1[['B','A']]
df1
```

Out[20]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    2 | 1000 |    3 |
|    b |    5 |    4 |    6 |

##### 修改索引

* 直接修改行索引index，列索引columns

In [21]:

```
df1 = df.copy()
df1
```

Out[21]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

In [22]:

```
df1.index = ['c','d']
df1.columns = ['C','D','E']
df1
```

Out[22]:

|      |    C |    D |    E |
| ---: | ---: | ---: | ---: |
|    c |    1 |    2 |    3 |
|    d |    4 |    5 |    6 |

* 通过rename函数进行修改

In [24]:

```
df1.rename(index={'c':'t'},columns={'C':'H'},inplace=False)
```

Out[24]:

|      |    H |    D |    E |
| ---: | ---: | ---: | ---: |
|    t |    1 |    2 |    3 |
|    d |    4 |    5 |    6 |

##### 添加行数据

* 添加一行数据

In [25]:

```
df1 = df.copy()
df1.loc['j'] = ['7','8','9']
df1
```

Out[25]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |
|    j |    7 |    8 |    9 |

* 添加多行数据

```
pd.concat(objs, axis=0)
```

确保 **列索引** 相同，行增加。 （其实这个函数并不要求列索引相同，它可以选择出相同的列。而我写这个教程遵循了python的宣言—明确：做好一件事有一种最好的方法，精确控制每一步，可以少犯错。）

- objs: list of DataFrame；
- axis: 取0，进行行增加操作。

In [26]:

```
df1 = pd.DataFrame(
    data=[
        [1,2,3,],
        [4,5,6],
    ],
    index=['a','b'],
    columns=['A','B','C'],
)
df2 = pd.DataFrame(
    data=[
        [7,8,9]
    ],
    index=['c','d'],
    columns=['A','B','C'],
)
pd.concat([df1,df2],axis=0)
```

Out[26]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |
|    c |    7 |    8 |    9 |
|    d |    7 |    8 |    9 |

##### 添加列数据

* 添加一列数据

In [27]:

```
df1 = df.copy()
df1
```

Out[27]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

In [28]:

```
df1['D'] = [4,7]
df1
```

Out[28]:

|      |    A |    B |    C |    D |
| ---: | ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |    4 |
|    b |    4 |    5 |    6 |    7 |

* 添加多列数据

In [29]:

```
df2 = pd.DataFrame(
    data=[
        [11,12],
        [14,15]
    ],
    index=['a','b'],
    columns=['E','F']
)
pd.concat([df1,df2],axis=1)
```

Out[29]:

|      |    A |    B |    C |    D |    E |    F |
| ---: | ---: | ---: | ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |    4 |   11 |   12 |
|    b |    4 |    5 |    6 |    7 |   14 |   15 |

##### 删除数据

* 删除多行数据

  ```
  DataFrame.drop(labels, axis = 0,  level=None, inplace=False)
  ```

  * labels：索引，单索引或索引的列表；
  * axis：0-删行；
  * level：多重索引需要指定；
  * inplace：是否本地修改。

In[30]:

```
df = pd.DataFrame(
    data = [
        [1,2,3],
        [4,5,6]
    ],
    index=['a','b'],
    columns=['A','B','C']
)
df
```

Out[30]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    a |    1 |    2 |    3 |
|    b |    4 |    5 |    6 |

In [33]:

```
df2 = df.copy()
df2.drop(['a'],axis=0)
```

Out[33]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    b |    4 |    5 |    6 |

* 删除一列删除

In [32]:

```
df1 = df.copy()
del df1['A']
df1
```

Out[32]:

|      |    B |    C |
| ---: | ---: | ---: |
|    a |    2 |    3 |
|    b |    5 |    6 |

* 删除多列数据

  ```
  DataFrame.drop(labels, axis = 1,  level=None, inplace=False)
  ```

  * labels：索引，单索引或索引的列表；
  * axis：1-删列；
  * level：多重索引需要指定；
  * inplace：是否本地修改。

In [33]:

```
df3 = df.copy()
df3.drop(['A','C'],axis=1)
```

Out[33]:

|      |    B |
| ---: | ---: |
|    a |    2 |
|    b |    5 |

In [34]:

```
df4 = df.copy()
df4.drop(columns=['A','C'],)
```

Out[34]:

|      |    B |
| ---: | ---: |
|    a |    2 |
|    b |    5 |

### 合并数据

#### merge()

```
pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None, left_index=False, right_index=False, sort = False)
```

concat函数本质上是在所有索引上同时进行对齐合并，而如果想在任意**列**上对齐合并，则需要merge函数，其在sql应用很多。

- left,right： 两个要对齐合并的DataFrame；
- how： 先做笛卡尔积操作，然后按照要求，保留需要的，缺失的数据填充NaN；
  - left: 以左DataFrame为基准，即左侧DataFrame的数据全部保留（不代表完全一致、可能会存在复制），保持原序
  - right: 以右DataFrame为基准，保持原序
  - inner: 交，保留左右DataFrame在on上完全一致的行，保持左DataFrame顺序
  - outer: 并，按照字典顺序重新排序
- on：列索引或列索引列表，如果要在DataFrame相同的列索引做对齐，用这个参数；
- left_on, right_on, left_index, right_index：
  - on对应普通的列索引或列索引列表，对齐不同列名的DataFrame，用这俩参数；
  - index对应要使用的index，建议不要使用这俩参数，因为可以用concat方法代替。
- sort: True or False，是否按字典序重新排序。

##### 1.初步

In [1]:

```
import numpy as np
import pandas as pd

df1 = pd.DataFrame(
    data=np.array([
        [1,2],
        [3,4]
    ]),
    index = ['a','b'],
    columns = ['A','B']
)

df2 = pd.DataFrame(
    data=np.array([
        [1,3],
        [4,7]
    ]),
    index = ['b','d'],
    columns = ['B','C']
)
```

In [2]:

```
df1
```

Out[2]:

|      |    A |    B |
| ---: | ---: | ---: |
|    a |    1 |    2 |
|    b |    3 |    4 |

In [3]:

```
df2
```

Out[3]:

|      |    B |    C |
| ---: | ---: | ---: |
|    b |    1 |    3 |
|    d |    4 |    7 |

1. 如果单纯的按照index对齐，不如用concat方法，所以一般不建议使用left_index, right_index 

In [4]:

```
pd.merge(left = df1, right = df2, left_on='A', right_on='B')
```

Out[4]:

|      |    A |  B_x |  B_y |    C |
| ---: | ---: | ---: | ---: | ---: |
|    0 |    1 |    2 |    1 |    3 |

> ```
> 小区别是concat对重复列没有重命名，但是重名的情况不多，而且重名了说明之前设计就不大合理。
> ```

In [5]:

```
pd.concat([df1,df2],join='inner',axis=1)
```

Out[5]:

|      |    A |    B |    B |    C |
| ---: | ---: | ---: | ---: | ---: |
|    b |    3 |    4 |    1 |    3 |

##### 2.on用法

* 设置**how='inner'**

In [6]:

```
# 对于'B'列，df1的b行以及df2的d行，是相同的，其他都不相同
pd.merge(left=df1,right=df2,how='inner',on=['B'])
```

Out[6]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    0 |    3 |    4 |    7 |

In [7]:

```
# 对于'A'列'b'行，df2的'C‘列d行是相同的，其他都不相同
# 其他列如果同名会进行重命名
pd.merge(left=df1,right=df2,how='inner',left_on=['A'],right_on=['C'])
```

Out[7]:

|      |    A |  B_x |  B_y |    C |
| ---: | ---: | ---: | ---: | ---: |
|    0 |    3 |    4 |    1 |    3 |

##### 3.how用法

In [8]:

```
# 保持左侧的不便，用右侧的来进行对齐，对不齐的填NaN
pd.merge(left=df1,right=df2,how='left',on=['B'])
```

Out[8]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    0 |    1 |    2 |  NaN |
|    1 |    3 |    4 |  7.0 |

In [9]:

```
# 保持右侧的不便，用左侧的来进行对齐，对不齐的填NaN
pd.merge(left=df1,right=df2,how='right',on=['B'])
```

Out[9]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    0 |  3.0 |    4 |    7 |
|    1 |  NaN |    1 |    3 |

* 对齐的列存在重复值

In [10]:

```
df1.loc['a','B']=4
df1
```

Out[10]:

|      |    A |    B |
| ---: | ---: | ---: |
|    a |    1 |    4 |
|    b |    3 |    4 |

In [11]:

```
df2
```

Out[11]:

|      |    B |    C |
| ---: | ---: | ---: |
|    b |    1 |    3 |
|    d |    4 |    7 |

In [12]:

```
# 根据B列，两个DataFrame之间不同行，有相同数据，则重新组成一行，并保持右侧# 不变
pd.merge(left=df1,right=df2,how='right',on=['B'])
```

Out[12]:

|      |    A |    B |    C |
| ---: | ---: | ---: | ---: |
|    0 |  1.0 |    4 |    7 |
|    1 |  3.0 |    4 |    7 |
|    2 |  NaN |    1 |    3 |

#### concat()详解

```
pd.concat(objs, axis=0, join='outer', join_axes=None, ignore_index=False, keys=None, levels=None, names=None, verify_integrity=False, sort=None, copy=True)
```

##### 1.初步

In [13]:

```
s1 = pd.Series(
    data=np.array([1,2,3]),
    index=['a','b','c']
)
s2 = pd.Series(
    data=np.array([4,5,6]),
    index=['e','f','g']
)
s3 = pd.Series(
    data=np.array([7,8,9]),
    index=['h','i','j']
)
```

In [14]:

```
pd.concat([s1,s2,s3])
```

Out[14]:

```
a    1
b    2
c    3
e    4
f    5
g    6
h    7
i    8
j    9
dtype: int32
```

In [15]:

```
pd.concat([s1,s2,s3],axis=1,sort=False)
```

Out[15]:

|      |    0 |    1 |    2 |
| ---: | ---: | ---: | ---: |
|    a |  1.0 |  NaN |  NaN |
|    b |  2.0 |  NaN |  NaN |
|    c |  3.0 |  NaN |  NaN |
|    e |  NaN |  4.0 |  NaN |
|    f |  NaN |  5.0 |  NaN |
|    g |  NaN |  6.0 |  NaN |
|    h |  NaN |  NaN |  7.0 |
|    i |  NaN |  NaN |  8.0 |
|    j |  NaN |  NaN |  9.0 |

### 普通列和行index的相互转化

### 字符串处理

### 查看信息

#### info

```
DataFrame.info(verbose=None, memory_usage=True, null_counts=True)
```

- verbose：True or False，字面意思是冗长的，也就说如果DataFrame有很多列，是否显示所有列的信息，如果为否，那么会省略一部分；
- memory_usage：True or False，默认为True，是否查看DataFrame的内存使用情况；
- null_counts：True or False，默认为True，是否统计NaN值的个数。

#### ndim、shape、size

> 查看维数，形状，元素个数

#### head、tail

默认分别查看头5行和后5行。

```
Series/DataFrame.head(n=5)
Series/DataFrame.tail(n=5)
```

#### memory_usage

```
Series/DataFrame.memory_usage(index=True, deep=False)
```

- index：是否显示索引占用的内存，毫无疑问索引也占用内存；
- deep：是否显示object类型的列消耗的系统资源，由于pandas中object元素只是一个引用，我估计这个deep是指显示真实的内存占用。

#### describe

>  快速查看每一列的统计信息，默认排除所有NaN元素

```
DataFrame.describe( include= [np.number])
```

- include：'all'或者[np.number 或 np.object]。numberic只对元素属性为数值的列做数值统计，object只对元素属性为object的列做类字符串统计。

### 数值运算

### 与数据库进行交互



