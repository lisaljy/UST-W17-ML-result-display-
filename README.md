# UST-W17-ML-result-display-

## Experiment1:  
**Experiment with ELM-tool box  
Aim: Only experiment to see the performance of ELM (without comparing, for we can see the result through other's paper:))**
* Brief introduction  
Small data, regression, elm ,with and without model structure selection  

* Data introduction  
4177 row of data in total  
2/3 (2784) of data is use for training, 1/3 (1393) of data for testing  
Datasets comes from [here](http://archive.ics.uci.edu/ml/datasets/Abalone)  
Data permutations are obtained from [here](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwip166a0cHRAhVJtI8KHdvZAlcQFggcMAA&url=http%3a%2f%2fieeexplore%2eieee%2eorg%2fdocument%2f5350449&usg=AFQjCNH5_dJN8ZYluFQvRy5z3fwCXbywOQ&sig2=ntfr_kJmMBstpY2jcZ1KSA)  
It is about Predicting the age of abalone.  
Given is the attribute name, attribute type, the measurement unit and a brief description.  

Name	|	Data Type |	Meas. |	Description
----	|	---------	| -----	| -----------
Sex		| nominal	|	M, F, and I (infant) |*M=0;F=1;I=2*
Length	|	continuous	| mm	| Longest shell measurement
Diameter |	continuous |	mm	| perpendicular to length
Height	|	continuous |	mm	| with meat in shell
Whole weight |	continuous |	grams	| whole abalone
Shucked weight |	continuous	| grams |	weight of meat
Viscera weight	| continuous	| grams	| gut weight (after bleeding)
Shell weight |	continuous |	grams	| after being dried
Rings	|	integer	|	+1.5 | gives the age in years  


* Implementing  
  Implementing by ELM/HPELM python package  
  More detail infomation about package can be found [here](http://hpelm.readthedocs.io/en/latest/api/elm.html)  

## Experiment2_DLNN:  
* Brief introduction  
Small data, regression, [DLNN](https://github.com/lisaljy/UST-W17-ML/blob/master/DLNN.md)  

* Data introduction
1000 row of data in total  
700 for training, 300 for testing  
2 input, 3 output  

* Experiment result [link](https://github.com/lisaljy/UST-W17-ML/blob/master/result_temp/exp2_DLNN/Result.md)  

## Experiment3_DLNN:  
* Brief introduction  
Small data, regression, [DLNN](https://github.com/lisaljy/UST-W17-ML/blob/master/DLNN.md)  

* Data introduction
2058 row of data in total  
1440 for training, 618 for testing  
3 input, 3 output  

* Experiment result [link](https://github.com/lisaljy/UST-W17-ML/blob/master/result_temp/exp3_DLNN/Result.md)  

## Experiment2_ELM:  
#### TODO  
* 回顾ELM算法的paper，整理[ELM](https://github.com/lisaljy/UST-W17-ML/blob/master/ELM.md)  
* 参考Ex2_DLNN的数据处理及模型参数问题，思考rms及稳定性问题？  
* 采用Ex2_DLNN最优weight，避免ELM模型初始权重随机？  
* 确定是否已设立收敛值？Training次数的选取
* 确定是否能正确输出模型weight和bias？  
* 看神经网络问题排查,了解调参方向 [link](https://deeplearning4j.org/cn/troubleshootingneuralnets)  
* 了解python ML并行调参包scikit-learn？  


**DLNN与ELM模型建构的意图？**
