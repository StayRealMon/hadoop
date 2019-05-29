## Hadoop安装流程 ##
1. jdk1.8环境安装&环境变量配置
2. ssh免密配置ssh-keygen -t -rsa ？
3. 配置hostname，测试免密
4. hadoop2.7 压缩包安装
5. /etc/hadoop/关键配置文件(core-site.xml&hdfs-site.xml&mapred-site.xml&yarn-site.xml)
5.1 core-site	hdfs://master:9000&hadoop.tmp.dir
5.2 hdfs-site	NN.dir&DN.dir
5.3 mapred-site	framework->yarn
5.4 yarn-site	RMwebappaddr->master:8088&RMaddr&minmaxallocation
6. hdfs -format①②③④

## HDFS ##
1. HDFS的设计目的是为了支持Map-Reduce分布式计算框架，其次才是一个文件系统，FileSystem不是重点。
2. 特点
> 低廉的节点和硬盘存储，导致错误是常态，且冗余较高
> 
> 目的是为了大数据分析而不是事务处理。因此适用于流式访问和批处理，不支持随机读取而是一写多读
> 
> 数据在节点之间有距离的概念。优先寻找本机数据，其次是就近机架的数据。
> 
> 优点：①高容错多副本自恢复②批处理&移动分布计算(计算向数据移动)&block位置暴露给计算框架，计算框架自行读取文件③大数据PB级百万文件万级节点④廉价可靠&容灾恢复
> 
> 缺点：①不适用于低延迟高吞吐②小文件存取时占内存，寻找时间大于读写时间③不支持并发写入和随机修改，同一时间仅仅支持一个写操作，文件修改仅仅支持append
3. 文件在HDFS中是以块 Block 为单位存储的。默认64M，备份*3

## OLTP与OLAP ##
数据处理大致可以分成两大类：联机事务处理OLTP（on-line transaction processing）、联机分析处理OLAP（On-Line Analytical Processing）。
> OLTP是传统的关系型数据库的主要应用，主要是基本的、日常的事务处理，例如银行交易。
> 
> OLAP是数据仓库系统的主要应用，支持复杂的分析操作，侧重决策支持，并且提供直观易懂的查询结果。 
> 
> OLTP 系统强调数据库内存效率，强调内存各种指标的命令率，强调绑定变量，强调并发操作；
> 
> OLAP 系统则强调数据分析，强调SQL执行市场，强调磁盘I/O，强调分区等

![](https://uploadfiles.nowcoder.com/images/20190503/4206388_1556867239437_7E609B9F3168715D87EDB72E9ED9F4FE)
## Name Node ##
Name Node作用：
> ①管理文件sys的命名空间
> 
> ②Block在DN上的位置和备份位置。通过心跳，DN宕机时抽空复制，备份过少进入安全模式(刚启动时有安全模式是因为还有节点没有汇报心跳，几分钟后收到心跳就可以解除安全模式了)
> 
> ③事务日志edit_log和快照文件fsimage
> 
> ④与client进行通信

NN所维护的信息：元数据信息(文件的时间大小权限所有者等)；**DN**的位置和状态；**Block**的位置和状态；维护虚拟的目录树；
NN的**Block块信息来自于DN的心跳汇报**
NN维护的信息基于内存，存在**单点故障**问题。通过保存edit_log&fsimage到disk以实现**持久化**
SecNN首次备份从NN获取edit_log和fsimage(两个文件都需要)，以后只获取edit_log即可。
> SecNN先停用NN的edit_log，NN先将新的log存至edit_log_new
> SecNN合并拿来的edit_log和**本地的fsimage**为新的fsimage并返回新的fsimage给NN
> NN将edit_log_new重命名为edit_log

首次format后启动NN时，生成空白fsimage，执行edit_log
> 若NN的内存满了就不能进行读写新建元数据，NN是集群的约束瓶颈
> 
> fsimage中不保存Block的位置信息和DN的位置和状态，来自于DN的心跳汇报

## Data Node ##
Data Node作用：①对本节点进行管理②提交自己保存的Block列表。**一写多读**，向NN心跳汇报状态
> 文件线性切割成块(Block)以字节为单位，有**偏移量**(offset)和**位置信息**。块的第一个字节面向于源文件的下标即为偏移量
> 
> Block的大小需要考虑硬盘的I/O量
> 
> disk负责保存实际的Block，以及描述Block的元数据信息(一个md5校验小文件)

## 高可用(HA)和联邦(Federation) ##
要解决的问题
1. 单点故障-HA主NN挂掉，切换到备份的NN
2. 没有故障但是内存受限-F所有的NN共享所有的DN资源

### HA ###
1. 来自于DN汇报的信息可以在两台NN中保持一致
2. 但是来自于Client的请求操作日志只和工作的一台NN进行连接，有可能会因为可用性导致不一致性
3. 可以利用Linux的**NFS**网络文件系统保持日志文件的一致性
4. 也可以加若干个**JN**专门存储操作日志，供两个NN同步
5. ZKFC(DFSZKFailoverController)是一个JVM进程，一边监控NN的健康状态，和NN之间没有网络I/O，属于同一个节点；ZKFC另一边**去ZK某一树目录下抢一个锁**创建一个节点，抢到锁的NN变为actived，其余的standby
6. 所有的standby向ZK进行注册，actived失败的时候，ZKFC删掉节点，**删除事件触发注册方法**，再次进行争抢锁
7. 若actived节点没有失败，但是JVM进程ZKFC断了，ZK的**session机制**，连接失败超时的时候删掉目录下的节点供再次争抢，原actived降为standby，抢到锁的升级actived

> 逻辑集群到物理集群的**映射**
> **journalNode的位置信息**描述配置
> 故障切换的**代理方法**和免密钥配置

1.  同一个物理cluster集群，要先启动**journalNode**(供新的HA集群NN1格式化的edit_log和fsimage存新的集群日志)

		hadoop-daemon.sh start journalnode

2.  然后**format**NN1(日志信息保存到JNN)

		hdfs namenode -format
3.  **启动zookeeper的节点**，进行**格式化**，用于ZKFC进行锁的争抢
		hdfs zkfc -formatZK

4.  接着**启动**NN2，但是不需要format，会根据，此时处于standby状态，NN2会同步已经格式化的所有DN信息

![](https://uploadfiles.nowcoder.com/images/20190528/4206388_1559033761726_4B1CE8F90F401D0BCCC4DBEE05440DB3)

### Federation ###
1. 一个集群有两个或者多个NN处于actived状态，但是两个NN获得到的DN汇报的block信息是不一样的，即**两个NN维护的目录树是不一样的**，虽然cluster是同一个，但是NN是隔离的，不能互相访问对方的数据。若第三方想要获取两个NN的目录树结构，得到cluster所有数据

> 先启动journalnode，format第一个NN，启动ZK，format ZK，(最后启动另一个NN?)

## Block的副本放置策略 ##
1. 第一块副本放在上传文件的DN，磁盘不太满，CPU不太忙的节点
2. 和第一个副本放在不同机架的节点上
3. 与第二个副本相同的机架节点上
4. 更多的节点随机放

## HDFS写流程 ##
1. client访问NN，NN如果说有此文件就不能写了。若没有文件，创建filename_copying
2. NN按照副本放置策略找到三个或多个节点返回DN List
3. client仅仅与DN List中的第一个节点DN1进行socket连接(副本透明，给DN1传输成功完成就ok)，将64M的Block切割为更小的packet，利用时间线重叠，行成pipeline进行流式传输
4. NN根据DN List的心跳汇报校验Block的位置，将filename返回
> 若有节点挂掉，根据本身的副本数量汇报进行复制，保证数量高于安全模式的阈值
> 
> 若全部挂掉，返回写失败

## HDFS读流程 ##
1. client访问NN寻求文件
2. NN根据本身维护的Block位置信息，对节点进行排序(根据副本放置策略)，返回给client
3. client从DN List中排序级别较高**距离最近**的节点读取对应的块

![](https://uploadfiles.nowcoder.com/images/20190503/4206388_1556867353821_2647913E15809B327E3669CC22982D66)
## MapReduce ##
**Input HDFS**
**->Block split**(切片，窗口机制，源文件变成<K,V>)
**->Map**(将<K,V>转化为<K,V,Partition>)
**->sort**(内部有序外部无序，根据Map生成的<K,V,P>中的K和P进行排序；排序前的<K,V,P>没有写入disk，而是在内存中的buffer缓冲区；排序结束后生成的文件按照Partition写入本地磁盘，供reduce节点拉去)
**->combiner**(局部reduce，减少实际reduce的时间)
**->shuffle**(默认Hash映射，注意要减少节点之间的I/O)
**->partition**(将相同的Key拉到同一个分区，便于下一步reduce计算)
**->merge**(依赖于Map作业的sort输出，这一步只是归并排序)
**->reduce**(将<K,V>转化为最终的<K,V,Partition>)
**->Output HDFS part00000**

> 默认一个Split为一个Block，即Block = Split。
> 
> 对于CPU密集计算而非I/O密集计算，小文件高密度计算，应将一个Block划分为更多的Split，让更多的Map任务处理，此时Block = n*Split = n*Map。实际上Map和Split必须是一一对应的
> 
> Split会把Input格式化为一条“记录”，一个“记录”对应一个Map任务；Merge后的reduce输入以“组”为单位，一个“组”有多条记录
> 
> 相同Key的“记录”为一“组”，一“组”对应一个reduce
> 
> Shuffle就是“Reducer启动后从所有的Map节点拉回属于自己数据的过程，是一个copying”或者“从Map算出结果之后，算出各自数据的分区号，直到Reducer拉取完自己的数据准备计算整个流程，是一个procedure”

![](https://uploadfiles.nowcoder.com/images/20190503/4206388_1556867379355_3DFB2E12314E238166FBCFFE6329A170)
## Hadoop1.x ##
**client**：对源文件计算，划分为Split List；上传jar&Split List&配置信息到HDFS，供节点获取，最后触发JobTracker
> 以作业为单位；规划作业的计算分布；提交作业到HDFS；请求JobTracker启动作业

**JobTracker**：**调度**和**资源管理**；获取TaskTracker的心跳汇报，分析资源并进行调度
> 核心主节点；调度所有的作业；根据心跳汇报监控集群的资源

**TaskTracker**：心跳汇报信息给JobTracker；获取JobTracker分配的task，从HDFS中获取Jar&Split&配置文件，运行Task
> 从节点，自身资源管理；和JobTracker心跳汇报状态和资源；获取Task

JobTracker**负载过大**，**单点故障**；资源管理和作业调度位于同一个节点，有**强耦合**，若有其他作业又需要实现一个新的JobTracker；且不同的框架对资源不能进行**全局管理**；(YARN可以)

## Hadoop2.x ##
JobTracker的**①作业调度**由AppMaster管理；②资源管理由ResourceManager实现

> Job1->RM->AM1->Container1
> 
> Job2->RM->AM2->Container2&Container3&Container4

RM根据集群中NodeManager的心跳汇报获取节点资源状态。
AM以作业为单位，负载到不同的节点进行作业调度，避免单点故障
> 每一个Node中必有一个NM做状态资源心跳汇报；可能会有AM和Container；RM为每一个Job分配一个AM，挑选资源足够不忙的Node产生若干个Container，Container由NM监控管理

![](https://uploadfiles.nowcoder.com/images/20190503/4206388_1556867387537_0B02D0BDA344265364CB97AE71F94407)



##WordCount##

	import org.apache.hadoop.conf.Configuration;
	import org.apache.hadoop.fs.Path;
	import org.apache.hadoop.io.IntWritable;
	import org.apache.hadoop.io.Text;
	import org.apache.hadoop.mapred.lib.db.DBInputFormat;
	import org.apache.hadoop.mapreduce.Job;
	import org.apache.hadoop.mapreduce.Mapper;
	import org.apache.hadoop.mapreduce.Reducer;
	import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
	import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
	import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
	import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;
	import org.apache.hadoop.mapreduce.lib.partition.HashPartitioner;
	
	import java.io.IOException;
	import java.util.StringTokenizer;
	
	public class WordCount {
	    //输入的参数不是基本类型，是包装后的泛型，支持①序列化和②排序比较。
	    //IntWritable就是一个可序列化的类。
	    //排序比较也有两种①数值比较②字典排序比较
	    public static class TokenizerMapper extends Mapper<Object, Text, Text, IntWritable>{
	        //one 和 word的声明写在map方法之外；是引用传递，会把上值覆盖
	        //Map之后会将输出转化为Buffer数组，即将<K, V>序列化为数组，Buffer再往disk写持久化
	        //因此one和word的声明不必写在map方法内部保留上次的计算值，仅仅需要创建两个对象用作值的引用
	
	        //one就是map之后<K, V>中的Value
	        private final static IntWritable one = new IntWritable(1);
	        //word是实际的单词，不是偏移量，是map后<K, V>中的Key
	        private Text word = new Text();
	
	        public void map (Object key, Text value, Context context) throws IOException, InterruptedException {
	            //StringTokenizer用来做切割；Object key表面上是Word实际上是Word在整个文件中的偏移量，是一个Long Int型
	            StringTokenizer itr = new StringTokenizer(value.toString());
	            while (itr.hasMoreTokens()){
	                word.set(itr.nextToken());
	                context.write(word, one);
	            }
	        }
	    }
	
	    //Reducer方法
	    public static class IntSumReducer extends Reducer<Text, IntWritable, Text, IntWritable>{
	        //原语：相同的Key为一组，调用一次reduce方法，然后在方法内迭代这一组数据，进行计算max  count   sum  min  等等
	        //result也是类似于one和word，声明在reduce外，写进缓冲区，因此是引用传递
	        private IntWritable result = new IntWritable();
	
	        //hello 1
	        //hello 1
	        //hello 1
	        //hello 1
	
	        //Key:      hello
	        //Value:    (1,1,1,1)
	
	        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
	            int sum = 0;
	            for (IntWritable val:values)
	                sum+=val.get();
	            //求和sum写进result中
	            result.set(sum);
	            //key直接写入context输出就ok了
	            context.write(key, result);
	        }
	    }
	
	    public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
	        //配置信息
	        Configuration conf = new Configuration();
	        Job job = Job.getInstance(conf,"WordCountDemo");
	//        Job job = new Job(conf,"WordCount");
	        //设定输入格式
	        job.setInputFormatClass(TextInputFormat.class);
	        //输入文件的来源路径，以参数传递
	        TextInputFormat.setInputPaths(job,args[0]);
	        //或者直接将路径写死，且可以add多个输入
	        Path input = new Path("/usr/local/test.txt");
	        FileInputFormat.addInputPath(job, input);
	        FileInputFormat.addInputPath(job, input);
	        FileInputFormat.addInputPath(job, input);
	
	        //也支持数据库查询获取数据来源，或者直接获取表的名字字段等
	        //DBInputFormat.setInput();
	
	        //打包时的类名？
	        job.setJarByClass(WordCount.class);
	        //设置Mapper
	        job.setMapperClass(TokenizerMapper.class);
	        //设置Combiner
	        job.setCombinerClass(IntSumReducer.class);
	        //设置Mapper输出，序列化，和Reducer方法的输入反序列化做对接
	        job.setMapOutputKeyClass(Text.class);
	        job.setMapOutputValueClass(IntWritable.class);
	        //设置Partitioner
	        job.setPartitionerClass(HashPartitioner.class);
	        //设置Reduce
	        job.setReducerClass(IntSumReducer.class);
	        //传参Reduce数量
	        job.setNumReduceTasks(Integer.parseInt(args[2]));
	        //设置Reduce输出
	        job.setOutputKeyClass(Text.class);
	        job.setOutputValueClass(Text.class);
	        job.setOutputFormatClass(TextOutputFormat.class);
	        //文件结果的输出路径，可以传参也可以写死
	        TextOutputFormat.setOutputPath(job, new Path(args[1]));
	        //或者直接将路径写死，且仅支持一个输出路径
	        Path output = new Path("/usr/local/res/");
	        //需要对路径是否存在进行判断，存在就写，不存在就报错好了^o^y
	        if(output.getFileSystem(conf).exists(output)) {
	            FileOutputFormat.setOutputPath(job, output);
	        }
	
	        System.exit(job.waitForCompletion(true)?0:1);
	
	    }
	
	}
