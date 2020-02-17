[toc]

# Java面试

## 1. Redis

### Redis简介

![image-20200208202136078](Java面试.assets/image-20200208202136078.png)

![image-20200208202406960](Java面试.assets/image-20200208202406960.png)

![image-20200208202455061](Java面试.assets/image-20200208202455061.png)

![image-20200208202954120](Java面试.assets/image-20200208202954120.png)

![image-20200208203150685](Java面试.assets/image-20200208203150685.png)

![image-20200208203512024](Java面试.assets/image-20200208203512024.png)

### Redis常用数据类型

![image-20200208205515771](Java面试.assets/image-20200208205515771.png)

![image-20200208205906253](Java面试.assets/image-20200208205906253.png)

![image-20200208205146198](Java面试.assets/image-20200208205146198.png)

![image-20200208205213970](Java面试.assets/image-20200208205213970.png)

![image-20200208205500602](Java面试.assets/image-20200208205500602.png)

![image-20200208205745731](Java面试.assets/image-20200208205745731.png)

![image-20200208205943082](Java面试.assets/image-20200208205943082.png)

### 从海量数据查询某一固定前缀的key

1、留意细节

​		摸清数据规模，问清楚边界

![image-20200213105911992](Java面试.assets/image-20200213105911992.png)

![image-20200213110859882](Java面试.assets/image-20200213110859882.png)

![image-20200213110913368](Java面试.assets/image-20200213110913368.png)

**批量生成Redis测试数据**

```
1.Linux Bash 执行
	for((i=1;i<=20000000;i++));
		do echo "set k$i V$i" >> /tmp/redisTest.txt
	生成两千万条Redis批量设置kv的语句写入文件
2.用vim去掉行尾的^M符号，如下：
	vim /tmp/redisTest.txt
	:set fileformat=dos # 设置文件的格式，通过这句话去掉每行结尾的^M符号
3.通过Redis提供的管道--pipe形式去跑Redis，传入文件指令批量灌数据，需要十分钟左右
cat /tmp/redisTest.txt | ../redis/src/redis-cli -h ip -p --pipe
```

![image-20200213110927278](Java面试.assets/image-20200213110927278.png)

![image-20200213111442545](Java面试.assets/image-20200213111442545.png)

![image-20200215171123769](Java面试.assets/image-20200215171123769.png)

**存到hashset里面达到去重的效果**



### 通过Redis实现分布式锁

![image-20200215171449570](Java面试.assets/image-20200215171449570.png)

![image-20200215171544424](Java面试.assets/image-20200215171544424.png)

 ![image-20200215171810552](Java面试.assets/image-20200215171810552.png)

<u>**缺点：原子性得不到满足**</u>

![image-20200215172122795](Java面试.assets/image-20200215172122795.png)

![image-20200215172214496](Java面试.assets/image-20200215172214496.png)

![image-20200215172226659](Java面试.assets/image-20200215172226659.png)

![image-20200215172358967](Java面试.assets/image-20200215172358967.png)

### 如何使用Redis做异步队列

![image-20200215174720010](Java面试.assets/image-20200215174720010.png)

![image-20200215174912782](Java面试.assets/image-20200215174912782.png)

![image-20200215174845884](Java面试.assets/image-20200215174845884.png)



**发布订阅模式**

![image-20200215175204982](Java面试.assets/image-20200215175204982.png)

![image-20200215175134383](Java面试.assets/image-20200215175134383.png)



### Redis如何做持久化

**RDB快照**

![image-20200215232357901](Java面试.assets/image-20200215232357901.png)

![image-20200215232808912](Java面试.assets/image-20200215232808912.png)

![image-20200215232827550](Java面试.assets/image-20200215232827550.png)

![image-20200215232930058](Java面试.assets/image-20200215232930058.png)

![image-20200215233046449](Java面试.assets/image-20200215233046449.png)

![image-20200215233059129](Java面试.assets/image-20200215233059129.png)

![image-20200215233332322](Java面试.assets/image-20200215233332322.png)

![image-20200215233410887](Java面试.assets/image-20200215233410887.png)

![image-20200215234749797](Java面试.assets/image-20200215234749797.png)

**AOF默认关闭**

![image-20200215234811116](Java面试.assets/image-20200215234811116.png)

![image-20200215234829545](Java面试.assets/image-20200215234829545.png)

![image-20200215235033110](Java面试.assets/image-20200215235033110.png)

![image-20200215235156302](Java面试.assets/image-20200215235156302.png)

![image-20200215235329278](Java面试.assets/image-20200215235329278.png)

![image-20200215235412286](Java面试.assets/image-20200215235412286.png)

![image-20200215235510374](Java面试.assets/image-20200215235510374.png)

![image-20200215235822922](Java面试.assets/image-20200215235822922.png)

### 使用Pipeline的好处

![image-20200216000732385](Java面试.assets/image-20200216000732385.png)

### Redis的同步机制

![image-20200216001238388](Java面试.assets/image-20200216001238388.png)

**slave负责读，master负责写**

![image-20200216001648830](Java面试.assets/image-20200216001648830.png)

![image-20200216002043979](Java面试.assets/image-20200216002043979.png)

### Redis的集群原理

![image-20200216002208631](Java面试.assets/image-20200216002208631.png)

![image-20200216002245619](Java面试.assets/image-20200216002245619.png)

![image-20200216002305183](Java面试.assets/image-20200216002305183.png)

![image-20200216002425088](Java面试.assets/image-20200216002425088.png)

![image-20200216002442203](Java面试.assets/image-20200216002442203.png)

**最小化有损服务**

![image-20200216002803883](Java面试.assets/image-20200216002803883.png)

![image-20200216002816447](Java面试.assets/image-20200216002816447.png)

**虚拟节点一半设置为32或者更大**



## 2. Linux知识考点

![image-20200216212209339](Java面试.assets/image-20200216212209339.png)

### 查找特定的文件

![image-20200216213825999](Java面试.assets/image-20200216213825999.png)

![image-20200216213929692](Java面试.assets/image-20200216213929692.png)

### 检索文件内容

![image-20200216214044035](Java面试.assets/image-20200216214044035.png)

![image-20200216214141036](Java面试.assets/image-20200216214141036.png)

![image-20200216214329015](Java面试.assets/image-20200216214329015.png)

![image-20200216215820656](Java面试.assets/image-20200216215820656.png)

![image-20200216232636752](Java面试.assets/image-20200216232636752.png)

![image-20200216235002355](Java面试.assets/image-20200216235002355.png)

### 对文件内容做统计

![image-20200216235150104](Java面试.assets/image-20200216235150104.png)

![image-20200216235332623](Java面试.assets/image-20200216235332623.png)

![image-20200216235437425](Java面试.assets/image-20200216235437425.png)

![image-20200217000401200](Java面试.assets/image-20200217000401200.png)

![image-20200217000504047](Java面试.assets/image-20200217000504047.png)

![image-20200217000743330](Java面试.assets/image-20200217000743330.png)

![image-20200217000927542](Java面试.assets/image-20200217000927542.png)

### 批量替换文件内容

![image-20200217001246875](Java面试.assets/image-20200217001246875.png)

![image-20200217001319764](Java面试.assets/image-20200217001319764.png)

![image-20200217001414487](Java面试.assets/image-20200217001414487.png)

![image-20200217001444629](Java面试.assets/image-20200217001444629.png)

![image-20200217001525234](Java面试.assets/image-20200217001525234.png)

**加一个g代表全局的，将每一行所有的都进行替换**

![image-20200217001649067](Java面试.assets/image-20200217001649067.png)

![image-20200217001751426](Java面试.assets/image-20200217001751426.png)

![image-20200217001820660](Java面试.assets/image-20200217001820660.png)

## 3. Java底层知识：JVM

![image-20200217145642230](Java面试.assets/image-20200217145642230.png)

### 谈谈对Java的理解

![image-20200217145951590](Java面试.assets/image-20200217145951590.png)

### 平台无关性如何实现

Compile Once，Run Anywhere

