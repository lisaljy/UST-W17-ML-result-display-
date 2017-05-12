# Dynamic Learning Neural Network 算法笔记
[参考文献： A dynamic learning neural network for remote sensing applications](http://ieeexplore.ieee.org/document/322598/)  
## 网络模型  
* 以 MLP 为 framework 设计的  
* 可以有多个hidden layer（通常情况下小于3层）  
* 第i层只能作为第i+1层的输入   

![pic 1](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/1.%20%E5%8D%95%E4%B8%AA%E7%BD%91%E7%BB%9C%E8%8A%82%E7%82%B9%E6%A8%A1%E5%9E%8B.PNG)  
![pic 2](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/2.%20%E5%8D%95%E4%B8%AA%E8%8A%82%E7%82%B9%E7%9A%84%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F.PNG)  
```   
符号解释:
* h 为每一层单个节点的 total net input
* S() 为 activation function; 通常用 sigm 函数
```
![pic 3](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/3.%20%E5%85%B8%E5%9E%8BMLP%E7%BD%91%E7%BB%9C%E6%95%B4%E4%BD%93%E7%BB%93%E6%9E%84.PNG)  
```   
h[i] = W[i]S(h[i-1]) + B[i] (for i = 1; i < p+1 )  

符号解释:  
* 设有p层hidden layer
* W：每一层的权重矩阵
  B: 偏置矩阵  
  n: 每一层节点的数量
* input = S(h[0])
  output = S(h[p+1])  
* input_num = n[0]
  output_num = n[p+1]

```  
![pic 4](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/4.%20%E5%85%B8%E5%9E%8BMLP%E7%BD%91%E7%BB%9C%E7%BB%93%E6%9E%84%20notation%20%E6%B3%A8%E8%AE%B0.PNG)
## Learning algorithm  
* BP learning algorithm
* Polynomial basis function
* Kalman filtering technique  

### BP（梯度下降法）   
[参考网址](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)  
#### 目的  
对权重进行最优化处理，使得input和output的映射关系达到最优  
**即：使得误差率rms小于某个特定的值**  
**基于本参考文献，BP算法只是用于展示后续算法develop的self-contained**
#### Process  
1. 计算每一层每一个节点的hij
2. 计算total error(rms) = sum(1/2(target - output)^2)
3. 计算每一个权重的变化对于total error的影响   
  即： total error 相较于每一个权重值的偏导数
4. 跟新权重矩阵中的每一个权重值(包括偏置值)：w' = w - (学习率*total error 相较于w的偏导数)  
5. **重复1~4步骤，直到total error小于预设误差率threshold**

```
补充内容：  
* 权重及偏置的初始值为小随机数；学习率为0~1之间
* 参考文献内有提供求解偏导数的recursive equations
```  
### PBF  
#### 目的  
对每一层中每一个节点的S(hij)化简，将 activation function 放入单个节点表达式中  
**将 MLP 网络转化成 complete 网络  
好处：当为 complete network 时，隐藏层的节点权重不再为必须的，只需要输出层的节点权重向量即可**  

#### Process  
![pic 5](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/5.%20%E5%81%87%E8%AE%BES(hij)%E5%8F%AF%E4%BB%A5%E5%B1%95%E5%BC%80%E4%B8%BA%E4%B8%8A%E5%BC%8F.PNG)  
```
符号解释：  
* Dij[k]: 代表误差率最优情况下的多项式系数  
* P(i,j): 由relative rms计算得到，P(i,j)会随着rms的下降而增大
```  
![pic 6](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/6.%20express%20the%20activation%20function%20within%20the%20network.PNG)  
![pic 6.1](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/6.1.PNG)  
![pic 6.2](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/6.2.PNG)
```
符号解释：  
* x: (M*1)转置的矩阵  
* M：0到p层每层节点的数量和+1(即：输入层节点和 + 隐藏层节点和 + 1)  
  实验例子中 M = 123  
* C: (M*L)的相关矩阵  
* X：(L*1)转置的输入参数矩阵；X = [X[0][1], X[1][1]... X[2][1], X[2][2]...]  
* X[0][1] = 1  
  X[1][l] = xl  
  X[2][l] = x1^2, x2^2, x1x2, x1x3 ect  
```  
![pic 7](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/7.%20output%E7%9A%84%E8%A1%A8%E7%A4%BA%E6%96%B9%E5%BC%8F.PNG)  
```   
符号解释：  
* W：(m*M)的输出层权重矩阵  
  W = [w1, w2, ..., w(p+1)]T  
  wk = 输出层每个节点组成的集合  
  wijk = 输出层的每个节点关于上一层节点连边上的权重值组成的集合  
```  
![pic 8](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/8.%20%E6%9C%80%E7%BB%88%E7%AE%80%E5%8C%96%E8%80%8C%E6%88%90%E7%9A%84%E6%AF%8F%E4%B8%80%E4%B8%AA%E8%BE%93%E5%87%BAy%E7%9A%84%E8%A1%A8%E8%BE%BE%E5%BC%8F.PNG)  
### Kalman filtering  
#### 目的  
预测和反馈向最小mse值的递归过程，对每一个输出节点上的权重进行filter  
#### Process  
![pic 9](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/9.%20%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%8A%B6%E6%80%81%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B.PNG)  
![pic 9.2](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/9.2.PNG)  
![pic 9.3](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/9.3.PNG)  
![pic 9.4](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/9.4%20%E5%99%AA%E5%A3%B0%E7%9A%84%E7%9B%B8%E5%85%B3%E5%85%B3%E7%B3%BB.PNG)  
```
补充及符号解释：  
* 每一个输出节点对应的权重值可以独立更新  
* A: (M*M)的状态转化矩阵  
* B: (M*M)的对角矩阵  
* uk: (1*M)的process error向量  
* vk: scalar measurement error  
* uk及vk为服从高斯模型的白噪声,相关关系如上图9.4  
```  
![pic 10](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/10.%20%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%E4%B8%AD%E6%9D%83%E9%87%8D%E7%9F%A9%E9%98%B5%E5%88%A9%E7%94%A8%E5%8D%A1%E5%B0%94%E6%9B%BC%E6%BB%A4%E6%B3%A2%E8%BF%9B%E8%A1%8C%E5%8F%8D%E9%A6%88%E5%92%8C%E9%A2%84%E6%B5%8B%E7%9A%84%E8%BF%87%E7%A8%8B.PNG)  
```
补充解释：  
* 上图第一个等式右边的权重值为经过PBF预测得到的估计值；
  左边的权重值为filter预测反馈而得到的估计值
* gk^j: 卡尔曼增益值; 通常使用UD分解来求卡尔曼增益值（ud文件的意义）
```  
![pic 11](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/11.%20%E5%8D%A1%E5%B0%94%E6%9B%BC%E5%A2%9E%E7%9B%8A%E5%80%BC%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F.PNG)  
[基于UD分解的卡尔曼增益值计算方式](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&ved=0ahUKEwjFk4zK1ZfTAhWKKJQKHc-tDE4QFgghMAI&url=http%3a%2f%2fwww%2epaper%2eedu%2ecn%2fdownload%2fdownPaper%2f201111-57&usg=AFQjCNHUSgmm5nxSln-DEmz1Vf4If02Mjw&sig2=pcntDt6E4g-XCvm_ip77pA)
```
简化计算：  
* 令Aj和Bj为单位矩阵  
* rk^j为小的正数  
* 令 Qk^j = φ^2 * I(单位矩阵)
  φ为指定的过程误差变量
* 初始权重设置为小随机数  
* 设立初始预测误差相关矩阵为图11.1
```  
![pic 11.1](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/DLNN/11.1.PNG)  
## 实验过程  
1. 预处理：
  * 对输入数据到预测数据进行 sensitibity test
  * 采用Monte Carlo对训练数据集进行选择，选取输出值易受输入值影响的
2. 神经网络黑箱处理
