# 随机梯度下降 SGD

```py
import matplotlib.pyplot as plt
 
x_data = [1.0, 2.0, 3.0]
y_data = [2.0, 4.0, 6.0]
 
w = 1.0
 
def forward(x):
    return x*w
 
# calculate loss function
def loss(x, y):
    y_pred = forward(x)
    return (y_pred - y)**2
 
# define the gradient function  sgd
def gradient(x, y):
    return 2*x*(x*w - y)
 
epoch_list = []
loss_list = []
print('predict (before training)', 4, forward(4))
for epoch in range(100):
    for x,y in zip(x_data, y_data):
        grad = gradient(x,y)
        w = w - 0.01*grad
        # update weight by every grad of sample of training set
        print("\tgrad:", x, y,grad)
        l = loss(x,y)
    print("progress:",epoch,"w=",w,"loss=",l)
    epoch_list.append(epoch)
    loss_list.append(l)
 
print('predict (after training)', 4, forward(4))
plt.plot(epoch_list,loss_list)
plt.ylabel('loss')
plt.xlabel('epoch')
plt.show() 
```
梯度下降 计算所有数据的梯度求和再下降
随机梯度下降 只计算一个数据的梯度
梯度下降速度快 但是性能差 无法处理鞍点
随机梯度下降效率低 但是效果好 
一般应用中选择一个batch一起计算梯度


# 反向传播
`w.requires_grad = true`
计算loss的过程是forward
`w.backward( )`
`w.grad.data.zero_( )` 

# 线性回归
1. 准备数据集

2. 设计模型
```py
class LinearModel(torch.nn.Module):  #继承自Module
    # _init_ 和 forward 必须要有
    def __init__(self):  #构造函数
        super(LinearModel, self).__init__()
        self.linear = torch.nn.Linear(1, 1)
 
    def forward(self, x):
        y_pred = self.linear(x)

model = LinearModel()
```
`torch.nn.Linear(in_features, out_features, bias=True)`
in_features 输入维度
out_features 输出维度

3. loss 和 optimizer
```py
criterion = torch.nn.MSELoss(reduction = 'sum')
optimizer = torch.optim.SGD(model.parameters(), lr = 0.01)
```

`torch.nn.MSELoss(size_average=False,reduce=true)`
torch.nn.MSELoss( )
size_average 是否求和

`torch.optim.SGD( )`
lr 学习率

4. training cycle
一般来说，先计算y_hat，再计算loss，梯度清零，backward，更新参数。
```py
for epoch in range(100):
    y_pred = model(x_data)
    loss = criterion(y_pred, y_data)
    print(epoch, loss.item())
 
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
```

# logistic回归
是个分类问题
sigmoid函数 σ(x) 
$$ σ(x) = \frac {1}{1+e^x} $$

交叉熵 cross-entropy
BCE Loss
![二分类损失函数](photo/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202022-10-12%20204549.png)
表示

# 多层神经网络 
```py
class Model(torch.nn.Module):
    def __init__(self):
        super(Model, self).__init__()
        self.linear1 = torch.nn.Linear(8, 6) 
        self.linear2 = torch.nn.Linear(6, 4)
        self.linear3 = torch.nn.Linear(4, 1)
        self.sigmoid = torch.nn.Sigmoid()
    def forward(self, x):
        x = self.sigmoid(self.linear1(x))
        x = self.sigmoid(self.linear2(x))
        x = self.sigmoid(self.linear3(x)) # y hat
        return x

model = Model()
```


# 数据集和batch

`xy=np.loadtxt('./data/Diabetes_class.csv.gz',delimiter=',',dtype=np.float32)#加载训练集合`

```py
from torch.utils.data import Dataset
from torch.utils.data import DataLoader


class DiabetesDataset(Dataset):
    def __init__(self, filepath):
        xy = np.loadtxt(filepath, delimiter=',', dtype=np.float32)
        self.len = xy.shape[0] # shape(多少行，多少列)
        self.x_data = torch.from_numpy(xy[:, :-1])
        self.y_data = torch.from_numpy(xy[:, [-1]])
 
    def __getitem__(self, index):
        return self.x_data[index], self.y_data[index]
 
    def __len__(self):
        return self.len
 
 
dataset = DiabetesDataset('diabetes.csv')
train_loader = DataLoader(dataset=dataset, batch_size=32, shuffle=True, num_workers=2) #num_workers 多线程

if __name__ == '__main__':
    for epoch in range(100):
        for i, data in enumerate(train_loader, 0):
            inputs, labels = data
            y_pred = model(inputs)
            loss = criterion(y_pred, labels)
            print(epoch, i, loss.item())
 
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()

```

# 多分类问题

要求所有概率之和为1
softmax
NLLLost
torch.nn.CrossEntropyLoss( )包括 softmax和损失函数NLLLoss

# CNN
* 经过一个卷积核得到的输出通道必然是1
  卷积核的通道等于输入通道
  卷积核的数量等于输出通道

* `torch.nn.Conv2d(In_Channel,Out_Channel,kernel_size=3,stride=2,bias=False)`

* 1*1 卷积核的作用：融合，改变通道数。
  
* Inception Moudel 有四个分支
  GoogleNet

* 梯度消失 ResNet
  H(x) = f(x) + x
```py
class ResidualBlock(nn.Module): #残差块
    def __init__(self, channels):
        super(ResidualBlock, self).__init__()
        self.channels = channels
        self.conv1 = nn.Conv2d(channels, channels, kernel_size=3, padding=1)
        self.conv2 = nn.Conv2d(channels, channels, kernel_size=3, padding=1)
 
    def forward(self, x):
        y = F.relu(self.conv1(x))
        y = self.conv2(y)
        return F.relu(x + y)

class Net(nn.Module):
    def __init__(self):
        pass
 
    def forward(self, x):
        pass

```

# RNN






