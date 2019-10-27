## 未归类的
1. something
2. 

## 大论文
1. 大论文还是要继续做点击率预估的，数据集可以用`360或者腾讯`的，主要还是要参考别人实现过的解决方案(参见dalao的博客)。
2. 我要做的是基于他们实现的方法做优化，思路保持一致，改进的地方就是在`uv/pv`等指标的计算过程中，用到流计算的技术，有工程意义而且实现了效率准确率的提升，勉强说的过去吧。
3. 具体的实现可以选择自己搭集群，或者直接用阿里云的现成产品？flink aliyun实时计算买服务，结合datahub项目，构建上下游的维表，用`flink SQL`即可完成demo

## 好文章
1. A Hierarchical Extreme Learning Machine：`we first propose a weighted output extreme learning machine (WO-ELM) to learn the imbalanced data`，对不同的imbalance ratio进行对比，对不同算法在不同的IR下对比较
2. A Novel Ensemble Approach for Click-Through Rate：`FM+GBDT`，`GFM, which is an ensemble learning of FM and GBDT`，FM做线性特征，GBDT做其他特征，attention mechanism做高阶特征选择如DIN和DIEN，目的是更加的个性化，不同用户对不同特征的注意度是不同的。数据集用的是movie-lens 和 KKBox；评价指标Hit Ratio (HR)和Normalized Discounted Cumulative Gain
(NDCG)
3. Accurate Prediction of Advertisement Clicks based on Impression：minimum redundancy-maximum relevance (mRMR) 用作特征值选择（能够选出具有最大相关性的最小特征子集），传统的简单算法做核心预测；dataset来自于 dashboard of an OTA，经过enrich处理，指标rmse和r2
4. Deep Interest Evolution Network ：增加了一层 interest extractor layer，用于提取用户兴趣特征，部署到淘宝，获得了20.7%的CTR提升；数据集采用Amazon Dataset 中的书籍和电子商品，工程数据用阿里内部的49天日志采集数据
5. Deeply supervised model for click-through rate：query和CTR结合，利用CNN，提升2%点击率和0.5%的 normalized discounted cumulative gain (NDCG)；不需要特征工程；1 Billion条搜索引擎查询样本;LSTM用作查询语句训练text embedding
6. Data-driven
identification of accidental clicks ：误点击率？判断广告停留时间`dwell time`这个指标然后针对性的训练学习。数据集用到的是Yahoo的数据集,CTR+3.9%,revenue+0.2%

## 好思路
1. 在[特征工程](https://github.com/luoda888/tianchi-diabetes-top12/blob/master/README.md)上下功夫（较好实现但是可能创新点不够？）特征提取用xgboost自动筛选，也可以用蚁群退火算法构造特征
2. 特征筛选的时候用多模型筛选，不止纠结于xgboost一个，给不同的模型加权，应该可以有效降低过拟合的风险，属于特征工程的范畴
3. 选好特征之后还是用stacking的思想堆叠模型吗，需要创新点。

## 网络安全
1. 如果要做出网络安全作品(系统安全/应用安全/网络安全/数据安全/安全检测)五大类中的，目前想法结合flink做异常检测，携程好像是有现成的异常检测报警服务的，结合了ai方法，多留意下其他方向的应用

## 模拟面试大赛 1022 周二  No.12

| 项目 | 分值 |
| - | - |
| 简历 | 20% |
|自我介绍 3min | 20% |
|答辩 1min | 20% |
|小组讨论(分析/交流/压力/组织能力考察) | 40% |
