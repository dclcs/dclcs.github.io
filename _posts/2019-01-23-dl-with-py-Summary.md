---
title: "【deep learning】dl-with-python-Summary"
author: dcl
CreateTime: 2019-01-19 17:23:3 +0800
date: 2019-01-19 17:23:3 +0800
categoies: dl
---

Summary of Chapter 1-5
DataSet : Mnist
Architecture: Two Layer network, Two Affine ,Activation: Relu and the last layer is softmax, loss is cross-entropy
<!--more-->

### 目标
<b>用两层网络实现</b>
### 架构
- LayerOne    :   `Input([图片展开向量], )`<br>
    - Weights: 
    - Bais
    - Activation: `Relu`<br>
- LayerTwo
    - Weights: 
    - Bais
    - Activation : `Relu`
- Output
    - Softmax
- Loss
    - crossentropy
### Details
#### 全连接层
- forward : $Y = WX + b$
- backward : 
    - 传递参数：`out`$=\frac{dL}{dY}$<br>
$\frac{dL}{dX} = \frac{dL}{dY} * \frac{dY}{dX} = dout * W^T$<br>
$\frac{dL}{dW} = \frac{dL}{dY} * \frac{dY}{dW} = X^T * dout$<br>
$\frac{dL}{db} = \frac{dL}{dY} * \frac{dY}{db} = dout * 1$<br>
#### ReLu层
- $y =\begin{cases} x, & x \ge 0 \\\ 0 , & x \lt 0\end{cases}$
- $\frac{\partial y}{\partial x} = \begin{cases} 1, & x \ge 0 \\\ 0 , & x \lt 0\end{cases}$
- `mask = x <= 0` 
- forward : `out[mask] = 0`
- backward : `dout[mask] = 0`

#### Softmax With CrossEntropy 层
- softmax:
    - $y_k = \frac {exp(a_k)}{\sum_{i=1}^n exp(a_i)}$
        - 改进：$y_k = \frac {exp(a_k)}{\sum_{i=1}^n exp(a_i)} = \frac {Cexp(a_k)}{C\sum_{i=1}^n exp(a_i)} = \frac {exp(a_k + logC)}{\sum_{i=1}^n exp(a_i + logC)}= \frac {exp(a_k + C^{'})}{\sum_{i=1}^n exp(a_i + C^{'})}$
- crossentropy:
    - $\mathbf E = -\sum_kt_klogy_k$,$y_k$是正确输出，$t_k$是正确理解标签，并且$t_k$中只有正确解标签为1，其他均为0（one-hot表示）
- softmaxwithcrossentropy
    - forward : 先进行`softmax`，再计算`crossentropy`<br>
    $y = softmax(x)$<br>
    $loss = cross\_entropy(y, t)$
    - backward: <br>
        $\frac{\partial L}{\partial a_k} = \frac{\partial L}{\partial y_k}\frac{\partial y_k}{\partial a_k} =-t_k\frac{1}{y_k}(\frac{exp(a_k)\sum_{i=1}^nexp(a_i) - exp(a_k)^2}{(\sum_{i=1}^nexp(a^i))^2}) =-t_k\frac{1}{y_k}(\frac{exp(a_k)}{\sum_{i=1}{n}} - (\frac{exp(a_k)}{\sum_{i=1}^n})^2) = -t_k\frac{1}{y_k}(y_k - y_k^2) = t_k(y_k - 1) = \begin{cases} y_k - 1 = y_k - t_k & t_k = 1 \\\ 0(y_k - 1) = y_k - t_k & t_k = 0\end{cases} = y_k -t_k$

### 数据导入
- 通过`tensorflow`自带的导入数据

```python
import tensorflow as tf
from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets('MNIST_data',one_hot=True)
```
- 操作数据,获取图片，标签

```python
train_nums = mnist.train.num_examples
validation_nums = mnist.validation.num_examples
test_nums = mnist.test.num_examples

train_data = mnist.train.images
val_data = mnist.validation.images
test_data = mnist.test.images

train_labels = mnist.train.labels
```

### 网络搭建
- 前向传播

```python
def __init__(self, input_size, hidden_size, output_size,weight_init_std=0.01):
    
    self.params = {}
    self.params['W1'] = weight_init_std * np.random.randn(input_size, hidden_size)
    self.params['b1'] = np.zeros(hidden_size)
    self.params['W2'] =  weight_init_std * np.random.randn(hidden_size, output_size)
    self.params['b2'] = np.zeros(output_size)
    
    
    self.layers = OrderedDict()
    self.layers['Affine1'] = Affine(self.params['W1'], self.params['b1'])
    self.layers['Relu'] = Relu()
    self.layers['Affine2'] = Affine(self.params['W2'], self.params['b2'])
    self.lastLayer = SoftmaxWithLoss()

def predict(self, x):
    for name, layer in self.layers.items():
      print(name, layer)
      x = layer.forward(x)
    return x
```