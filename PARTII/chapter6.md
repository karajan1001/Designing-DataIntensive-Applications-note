# 第六章 分片
分片主要为了伸缩性，分片经常和备份一起使用。但是两种范式相互独立。

**skewed**：数据分片不平衡都集中到一台机器上
**hot spot**：不成比例高负载的分片
## 两种分片方法
1. 连续分片：优点是range操作简单，缺点是容易skew
2. Hash分片：优点是不会skew，缺点是range麻烦。
## 第二索引
第二索引一般由每个分片单独处理，当需要查询时请求会提交给所有分片最后再汇总，这个过程叫分散(scatter)。还有一个办法是使用term-partitioned。将第二索引按名字分片存储，不过这样会提高写入延迟。
## 重平衡
增减机器，增减内存，机器故障都可能导致分片需要重平衡。
重平衡三原则：
1. 负载需要均衡。
2. 不能打断正常读写。
3. 数据移动尽量少。

问题3是为何分片哈希后不直接使用mod确定分片位置的原因。

## 总结
两种分片方法：
1. 哈希
2. key-range

两种第二索引方法：
1. 本地索引
2. term索引
