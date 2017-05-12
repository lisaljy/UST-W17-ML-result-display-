# Test Result  
## Case1  
* **将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)**    
* 随机截取1-1440作为training集；1441-2058为测试集    
* 由于重复训练12次变化不大，故没有继续进行下去，第 i 次用了第 i-1 的weight和基于UD分解的卡尔曼滤波增益值  

**training集合的regression**  
![kl_train](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case1/kl_train.png)  
![ks_train](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case1/ks_train.png)  
![mv_train](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case1/mv_train.png)  

**testing集合的regression**  
![kl_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case1/kl.png)  
![ks_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case1/ks.png)  
![mv_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case1/mv.png)  

**rms error: 4.509680, 0.818279, 0.142472**  
**inverted result & rms 为第10次实验结果**  

## Case2  
* 将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)
* 随机截取1-1440作为training集；1441-2058为测试集  
* **修改网络参数，将网络每层节点数降为10**  
* 由于重复训练2次变化不大，故没有继续进行下去，第 i 次用了第 i-1 的weight和基于UD分解的卡尔曼滤波增益值 (重复实验下去？)  

**testing集合的regression**  
![kl_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case2/kl.jpg)  
![ks_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case2/ks.png)  
![mv_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case2/mv.png)  

**rms error: 3.741964, 0.768856, 0.118365**   

## Case3  
* 将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)
* **增大了数据集，扩充至16744**  
* 随机截取1-11720作为training集；11721-16744为测试集  
* regression fit 显示与case1，2情况大致相同，没有本质的提升

**testing集合的regression**  
![kl_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case3/kl.png)  
![ks_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case3/ks.png)  
![mv_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case3/mv.png)  

**rms error: 3.295030, 0.646489, 0.119759**   

## Case4  
* 将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)  
* 数据均来自2058sample数据集
* 随机截取1-1440作为training集；1441-2058为测试集  
* **开始训练网络之前，手动调整了训练集数据集前10个对象，保证其覆盖range均衡**  
* 相较于case2，rms有一定程度的下降，regression fit肉眼上没有直观的提升  

**testing集合的regression**  
![kl_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case4/kl.png)  
![ks_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case4/ks.png)  
![mv_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case4/mv.png)  

**rms error: 3.302407, 0.685067, 0.119522**   

## Case5  
* 将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)
* 数据集为16744sample  
* 随机截取1-11720作为training集；11721-16744为测试集   
* **每一次迭代时，训练集的数据均随机排列一次，共迭代了3次**  
* 实验结果没有本质提升

## Case6  
* **将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)**
* **再对输入输出进行了归一化处理**  
* 数据集为16744sample  
* 随机截取1-11720作为training集；11721-16744为测试集   
* 共迭代了2次  
* 实验结果没有本质提升  

**testing集合的regression**  
![kl_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case6/kl.png)  
![ks_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case6/ks.png)  
![mv_test](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case6/mv.png)  

**rms error: 0.723196, 0.737914, 0.843352**  

## Case7  
* **将三个输出变量拆分成三个单独的target，即有三个3input & 1output模型**  
* hh,vv为真值：A(dB)变成了B(real value) (A = 10lgB)  
* 数据集为16744sample
* 随机截取1-15070作为training集；15071-16744为测试集
* 实验结果没有本质提升  
***（未完成，当前只验证了kl）***  

**testing_kl集合的regression**  
![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case7/kl.png)  

## Case8  
* **基于DLNN网络结构实验**    
* **选取ks,mv,hh,vv做输入；kl为输出**  
* **hh,vv为真值**  
* 数据集为16744sample  

**testing_kl集合的regression**   
![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case8/kl_test.png)  

## Case9  
* 基于DLNN网络结构实验  
* 选取ks,mv,hh,vv做输入；kl为输出  
* **hh,vv为dB值**  
* 数据集为16744sample  

**testing_kl集合的regression**   
![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case9/kl_test.png)

## Case10  
* 利用 Matlab 中的现成神经网络工具包测试
* 基于feed-forward network  
* 网络结构：1个隐藏层（10个结点，激活函数为sigmoid）；1个输出层（由输出结构组成，激活函数为线性）  
* 训练算法采用： Levenberg-Marquardt backpropagation algorithm  
* 数据均来自2058sample数据集  
* 随机选取数据集：training:70%; validation:15%; testing:15%   

#### 小组实验结果展示
* case10.1：hh,vv,theta为输入；kl,ks,mv为输出  

![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case10/3in3out.png)  

* case10.2：hh,vv,theta为输入；kl为输出  

![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case10/3in1out_kl.png)  

* case10.3：hh,vv,theta为输入；ks为输出  

![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case10/3in1out_ks.png)  

* case10.4：hh,vv,theta为输入；mv为输出  

![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case10/3in1out_mv.png)  

* case10.5：hh,vv,ks,mv为输入；kl为输出  

![regression](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/case10/4in1out_kl.png)  


## 阶段性实验总结  
#### Conclusion & Question   
* 由case1 自身实验发现：
  * 随着训练次数的增加kl,ks与er的rms轻微反弹，怀疑过拟合情况发生，缺少validation数据集或模型选择（信息论？）  
  * 对比train集合与test集合的regression图像可知，基于当前的training集而言，testing集合已经尽可能的预测了  
* 由case1 & case2 发现减少网络节点对于训练结果影响不大  
* 由case1 & case3 发现增大数据集对于训练结果的影响也不大  
* 依据师姐的建议，调整了训练集前10个训练对象的顺序，保证覆盖性均匀，感觉实验效果有一定的提升，然而拟合效果仍欠佳  
* 由case5 排除迭代训练样本顺序重复问题  
* 由hh与vv的概率密度函数曲线图可知：  

![hh](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/hh_pmf.png)
![hh_normalize](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/hh_normalize_pmf.png)  
![vv](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/vv_pmf.png)
![vv_normalize](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp3_DLNN_result/vv_normalize_pmf.png)  

*归一化处理并未改变其分布，同时由大数定理可知，当样本量足够大时，样本的均值和方差均趋于恒定，正则化处理，相对而言只是进行了坐标轴的变换，故不应存在理论上的错误*  
* 由case6 发现，归一化处理的效果并未提升训练结果，因此怀疑归一化的方法，后期是否可以尝试：A = B/B的range？  
* 由case3 & case8 可发现基于当前DLNN的网络结构，当换用不同结构的数据集时，所得效果会改变，因此猜想是否由于实验数据集合自身的原因导致训练结果不佳  
* 对比case8 & case9 可知输入的单位确实对于训练结果有一定的影响  
* 由case10 猜想，训练结果不佳的原因：  
  * 数据集合本身的原因  
  * 网络结构局限性造成  
  * 数据集与网络结构的契合问题  
  * 缺少验证集合（validation）对网络模型进行最优化选择   

#### Next Step  
* 尝试elm算法  
* 学习，尝试coding？   
* 了解更多经典神经网络，结构及适用范围   
