  2019ICLR的一篇文章，来自mit hansong 团队。
  motivation:
  1之前的nas在小数据集cifar搜索，然后再通过堆叠更多的相同cell的形式迁移到大数据imagenet上测试效果，不能保证最优
  2one-shot的搜索方式内存消耗较大，每次需要计算并保存所有候选操作
  3没有将再不同的硬件上的latency作为考虑。
  
  创新：
  1不同于darts和one-shot计算所有候选操作求和：
  ![image](https://github.com/johsnows/save-self-from-deep-learning/blob/master/images/proxyless%20nas/微信图片_20200101175544.png)
  proxylessnas用概率p生成每个候选操作对应的binarize参数g，每次只激活一个path，从而减少了内存消耗。在更新的时候如果对每个操作都更新的话如果每个操作都
  计算以下更新梯度就和darts的方法没有区别了，于是作者采样了两条path出来跟新相当于时间换空间了。
  
  2同时作者将latency作为优化目标加入到loss里，由于latency是不可导的，作者将block i的lantency的期望定义为：
  ![2](https://github.com/johsnows/save-self-from-deep-learning/blob/master/images/proxyless%20nas/微信图片_20200101175656.png)
  
  F(Oi,j)就是Oi,j的预期latency，E[lantencyi]的梯度就是： ∂(E[latency i]) / ∂(pi,j) = F(oi,j). 
  
  3除了用gradient之外，用RL去优化上面提到的binarize gate和latency
  
  实验：
  1实验验证了在GPU、CPU、moblie phone上对应搜到的网络架构不适用于其它设备，说明了针对不同的部署环境搜索对应的架构的必要性
  2在imagenet上作者分别在gpu、mobilephone上验证了性能优于stoa，AmoebaNet-A 和
mnasnet，并且latency相应更低
