# Test Result  
## Case1  
* 无归一化  
* 顺序截取1-700作为training集；701-1000为测试集  
* 重复训练5次，第 i 次用了第 i-1 的weight和基于UD分解的卡尔曼滤波增益值  
* 随着训练次数的增加kl的rms下降速率显著，ks与er下降速率较慢并伴随震荡  
* myoutput.csv文件为inverted result  
* Test_result.csv文件为truth  
* myrms文件为inversion performance  

![rms error: 14.431792, 0.109710, 6.642404 ](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp2_DLNN_result/case%201.png)  

**rms error: 14.431792, 0.109710, 6.642404**  
**inverted result & rms 为第五次训练结果**

## Case2  
* 输入输出均进行了归一化处理  
* 顺序截取1-700作为training集；701-1000为测试集  
* 重复训练3次，第 i 次用了第 i-1 的weight和基于UD分解的卡尔曼滤波增益值
* 随着训练次数的增加kl,ks与er的rms轻微震荡    
* myoutput.csv文件为inverted result
* myoutput_normalizeInverse.csv文件为反归一化处理后的inverted result  
* Test_result.csv文件为truth  
* Testresult_normalizeInverse.csv文件为反归一化处理后的truth
* myrms文件为inversion performance   

![rms error: 1.614599, 0.542806, 0.681706  ](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp2_DLNN_result/case%202.png)  

**rms error: 1.614599, 0.542806, 0.681706**  
**inverted result & rms 为训练最好结果**

## Case3  
* 输入输出均进行了归一化处理  
* 随机截取1-700作为training集；701-1000为测试集  
* 重复训练3次，第 i 次用了第 i-1 的weight和基于UD分解的卡尔曼滤波增益值
* 随着训练次数的增加kl,ks与er的rms轻微震荡    
* myoutput.csv文件为inverted result
* myoutput_normalizeInverse.csv文件为反归一化处理后的inverted result  
* Test_result.csv文件为truth  
* Testresult_normalizeInverse.csv文件为反归一化处理后的truth
* myrms文件为inversion performance   

![rms error: 0.965910, 0.314225, 0.277262 ](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp2_DLNN_result/case%203.png)

**rms error: 0.965910, 0.314225, 0.277262**  
**inverted result & rms 为训练最好结果**  

## Case4  
* 将三个输出变量拆分成三个单独的target，即有三个2input & 1output模型（case4.1 = kl; case4.2 = ks; case4.3 = er）  
* 输入输出均进行了归一化处理  
* 随机截取1-700作为training集；701-1000为测试集  
* kl, ks与er的rms与case3的结果基本一致
* 每一个myrms文件为对应输出的inversion performance  
* myrms_4.1_Train为第一列输出（kl）对于Train集合自身的拟合效果  

![rms error](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp2_DLNN_result/case%204.png)

**由于rms结果与case3实验基本一致，固只进行了一次实验**  

## Case5  
* 将输入的单位进行转化：A(dB)变成了B(real value) (A = 10lgB)  
* 随机截取1-700作为training集；701-1000为测试集  
* 由于重复训练2次变化不大，故没有继续进行下去，第 i 次用了第 i-1 的weight和基于UD分解的卡尔曼滤波增益值  
* 随着训练次数的增加kl,ks与er的rms轻微震荡    
* myoutput.csv文件为inverted result  
* Test_result.csv文件为truth  
* myrms文件为inversion performance   

![rms error: 2.707689, 0.043042, 2.293964](https://github.com/lisaljy/UST-W17-ML/blob/master/pic/exp2_DLNN_result/case%205.png)  

**rms error: 2.707689, 0.043042, 2.293964**  
**inverted result & rms 为训练最好结果**     

## 阶段性实验总结  
#### Conclusion  
* 前期是否对数据进行归一化处理对实验结果有显著影响  
* Train 集和 Test 集的随机选取能较有效的避免实验结果泛化问题
* 加入归一化处理和随机选取训练集使得第一次训练结果有较大程度的提高  
* 输出合并和分开对于模型performance没有影响  
* 第一列输出（kl）对于Train集合自身的拟合效果欠佳

#### Question         
* myerror文件的意义，myerror下一行打印的内容意义？    

#### Next Step  
* 跑加入了角度变化的数据  
* 画图（inversion & truth | rms & iteration | probability density funtion & ?）
* 思考是否需要利用coding进行编码（Haming distance）从而缩小input的range  
* 收敛后需根据震荡情况决定是否需要取rms以及inversion的平均
* ？？模糊理论；Fuzzy；神经网络调参依据  

* 学习实验预处理  
* 跑大量数据

#### If I have time  
* 程序移植性
* 程序robust问题
