# Spanner - Google全球分布式数据库

## 2.2 目录放置
- 目录是桶，在键值集合的上层？一组前缀相同的连续的键的集合
- 2.3讲述前缀的来源，目录可以控制数据的局部性，尽量在数据中心内传输？
- 缓解Paxos组的负载而移动目录，即相同的连续的键放在一起
- 目录可以在客户端操作的时候移动，50MB的目录移动需要几秒
- 一个Paxos组包含多个目录，Spanner的tablet装有多个空间分区的容器
- Bigtable必须是行空间上字典顺序连续的分区
- 后台任务movedir，可以添加和删除副本，不是单个事务，避免阻塞
- 开始移动数据时注册时间，完成时启动事务原子性地移动剩余数据，更新组的元数据
- 目录还可以指定副本的地理位置，数量，类型，比如北美，五份副本，一份证人
- 应用程序给目录打上标签，保存各自的目录到不同的区域
- 目录太大还可以分成多个段，从而移动段而不是整个目录
