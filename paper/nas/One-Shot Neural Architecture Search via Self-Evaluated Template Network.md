2019iccv的文章

motivation：
1作者认为之前darts这样的优化方法在优化整个supenet的时候会造成简单网络更容易被优化，从而造成马太效应。
2之前的one-shot方法在训练完之后直接随机采样网络选取最优网络，作者认为这样很难选出最优网络


Innovation:
1在训练supenet的时候随机采样网络出来进行训练跟新，保证每个网络被均匀的优化
2提出了一个network estimator，用以选取出loss较低的网络：
![1](https://github.com/johsnows/save-self-from-deep-learning/blob/master/images/setn/1.png)
![2](https://github.com/johsnows/save-self-from-deep-learning/blob/master/images/setn/2.png)
![3](https://github.com/johsnows/save-self-from-deep-learning/blob/master/images/setn/3.png)
其实就是给每条边的操作选择和每个节点输入选择加入权重α然后softmax训练一下权重α，最后根据这个概率分布采样出来的网络就会相对loss低一些
