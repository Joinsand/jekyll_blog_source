---
layout: post
title:  "2014辽大计算机网络复习题"
category: CS
tags: 计算机网络
---

> written by zhangqi xuxiao


###第一章

####1. 在存储-转发数据包交换系统中，衡量延迟的一个因素是数据包在交换机上存储和转发需要多长时间。假设在一个客户机-服务器系统中，客户机在纽约而服务器在加州，如果交换时间为10微秒，试问交换时间是否会成为影响延迟的一个主要因素？假设信号在铜线和光纤中的传播速度是真空光速的2/3。

* 不，传送.速度为200,000 公里/秒或200米/ 微秒。信号在10微秒中传送了2千米，每个交换机相当于增加额外的2 公里电缆。 如果客户和服务器之间的距离为5000 公里，平均通过50个交换机给那些总道路只增加100 公里，只是2%。 因此，交换延迟不是这些情形中的主要因素。

####2. 在有些网络中，数据链路层处理传输错误的做法是请求发送方重传被损坏的帧。如果一帧被破坏的概率为p，试问发送一帧所需要的平均传输次数是多少？假设确认帧永远不会丢失。

* $$\sum_{k=1}^\infty k(1-p)p^{k-1}={1\over 1-p}$$

####3. 一幅图像的分辨率为1024*768像素，每个像素用3字节表示。假设该图像没有被压缩。试问，通过56kbps的调制解调器传输这副图像需要多长时间？通过1Mbps的线缆调制解调器呢？通过10Mbps的以太网呢？通过100Mbps的以太网呢？

* $$ 1024 * 768 * 3 = 2359296B $$

$$ {2359296 * 8\over{56 * 1000}}=337.042S $$

$$ 337.042 * {56 *10^3\over 10^6}= 18.874S $$

$$1.887S $$

$$0.189S $$

####4. 假设实现第k层操作的算法发生了变化。试问这会影响到第k-1和第k+1层的操作吗？

* 不会影响

###第二章

####5. 每1毫秒对一条无噪声4kHz信道采样一次。试问最大数据传输率是多少？如果信道上有噪声，且信噪比是30dB，试问最大数据速率将如何变化？

* 无噪声信道最大数据传输率公式：最大数据传输率=$ 2Hlog _ 2V  b/s $。发送二进制信号的$3kHz$ 信道的最大数据传输速率为$2*4 log_22=8kbps$
* 信噪比为$30 dB $即$ S/N =1000 $.由于$ log _ 2 1001≈9.967 $，由香农定理，该信道的信道容量为$3log _ 2(1+1000)=29.9kbps$

####6. 如果在一条3kHz的信道上发送一个二进制信号，该信道的信噪比为20dB，试问可达到的最大数据率为多少？

* 信噪比为$ 20 dB $ 即 $ S/N =100 $.由于 $ log _ 2 101≈6.658 $，由香农定理，该信道的信道容量为$ 3log _ 2(1+100)=19.98kbps $。
* 又根据乃奎斯特定理，发送二进制信号的3kHz 信道的最大数据传输速率为
$ 2*3 log _ 2 2=6kbps $。
所以可以取得的最大数据传输速率为$ 6kbps $。

####7. 试问调制解调器的解调部分与编码解码器的编码部分有没有区别？如果有的话，区别是什么？（毕竟两者都将模拟信号转换成）

* 有。编码器接受任意的模拟信号，并从它产生数字信号。而解调器仅仅接受调制了的正弦（或余弦）波，产生数字信号。

####8. __使用如图2-17所示的集线器，试问需要多长时间才能把一个1GB的文件从一个VSAT发送到另一个？假设上行链路是1Mbps，下行链路是7Mbps，采用电路交换技术，电路的建立时间是1.2秒。__

* $$1.2+{1GB \over 1Mbps / 8 }+ 540ms=8001.75S$$

####9. 一个CDMA接收器得到了下面的码片：（-1+1-3+1-1-3+1+1）。假设码片序列如图2-28（a）所定义，试问哪些移动站传输了数据？每个站发送了什么比特？

* (-1 +1 -3 +1 -1 -3 +1 +1)* (-1 -1 -1 +1 +1 -1 +1 +1)/8 = 1

(-1 +1 -3 +1 -1 -3 +1 +1) *(-1 -1 +1 -1 +1 +1 +1 -1)/8 = -1

 (-1 +1 -3 +1 -1 -3 +1 +1) *(-1 +1 -1 +1 +1 +1 -1 -1)/8 = 0

(-1 +1 -3 +1 -1 -3 +1 +1) *(-1 +1 -1 -1 -1 -1 +1 -1)/8 = 1

* A,D发送1bit，B发送0bit，C没有发送

###第三章

####10. 一个数据流中出现了这样的数据段A B ESC FLAG D，假设采用本章介绍的字节填充法，试问经过填充之后输出的是什么？

* A B ESC ESC ESC FLAG D

####11. 需要在数据链路层上被发送一个比特串：0111101111101111110。试问，经过比特填充之后实际被发送出去的是什么？

* 011110111110011111010

####12. 使用本章介绍的标准CRC方法传输比特流10011101.生成多项式未$x^3+1$。试问实际传输的位串是什么？假设左边开始的第三个比特在传输过程中变反了。请说明这个错误可以在接收方被检测出来。给出一个该比特流传输错误的实例，使得接收方无法检测出该错误。

* 10011101 101
* 余数不为0
* 10011110 101

####13. 想象一个滑动窗口协议，它的序号占用的位数相当多，使得序号几乎永远不会回传。试问4个窗口边界和窗口大小之间必须满足什么样的关系？假设这里窗口的大小固定不变，并且发送方和接收方的窗口大小相同。

* 发送窗口为(Si , Su) 接收窗口为 (Ri , Ru).窗口大小为W.  
$$0 ≤　Su-Si+1 ≤　W $$
$$Ru-Rl +1 ≤　W $$
$$Si ≤　Ri ≤　Su -1 $$


####14. 在前面的问题中，假设使用滑动窗口协议代替停-等协议。试问多大的发动窗口才能使得链路利用率为100%？发送方和接收方的协议处理时间可以忽略不计。

* $$ { 600.008 \over 0.004}=150002 $$

###第四章

####15. 试问经典10Mbps以太网的波特率是多少？

* 以太网使用曼彻斯特编码，这就意味着发送的每一位都有两个信号周期。标准以太网的数据率为10Mb/s，因此波特率是数据率的两倍，即20MBaud

####16. 假设经典以太网使用曼彻斯特编码，请画出比特流0001 1101 01的编码输出。

* LH LH LH HL HL HL LH HL LH HL

####__17. 一个1千米长、10Mbps的CSMA/CDLAN（不是802.3），其传播速度为200米/微秒。这个系统不允许使用中继器。数据帧的长度是256位，其中包括32位的头、校验和以及其他开销。再一次成功传输后的第一个比特槽被预留给接收方，以便它抓住信道发送32位的确认帧。假设没有冲突，试问除去开销之后的有效数据率是多少？__

* $${1000m\over200m/us}*2+{256b+32b\over10^6b/s}=0.298ms$$

$${256b-32b\over0.298ms}=0.75Mbps$$

$${0.75\over10}=7.5\%$$

####18. 两个CSMA/CD站都企图传送大文件（多个帧）。每发出一帧，它们就使用二进制指数后退算法竞争信道。试问在第k轮结束竞争的概率是多少？每个竞争周期的平均次数是多少？

* $$ p_k={(1-k^{-(k-1)})(2^{-(k-1)(k-2)/2})} $$

####19. 以太网帧必须至少64字节长，才能确保党电缆一端发生冲突时，发送方仍处于发送过程中。快速以太网也有同样的64字节最小帧长度限制，但是它可以快10倍的速度发送数据。试问它如何有可能维持同样的最小帧长度限制？

* 长度缩小到原来的1/10

###第五章

####20. 请列举出两个适合使用面向连接服务的计算机应用实例，再列举出两个最好使用无线连接服务的计算机应用实例。

* 文件传送、远程登录和视频点播需要面向连接的服务。另一方面，信用卡验证和其他的销售点终端、电子资金转移，以及许多形式的远程数据库访问生来具有无连接的性质，在一个方向上传送查询，在另一个方向上返回应答。 


####21. 一个有4800台路由器的网络采用了层次路由。试问对于三层结构来说，应该选择多大的区域和簇才能将路由表的尺寸降低到最小？一个好的起点是假设这样的方案接近最优：有k个簇，每个簇有k个区域，每个区域有k个路由器。这意味着k大约是4800的立方根（约等于16）。反复试验找出所有这三个参数在16附近的各种组合。

* 所谓分级路由，就是将路由器按区（REGION）进行划分，每个路由器只须知道在自己的区内如何为分组选择路由到达目的地的细节，而不用知道其他区的内部结构。对于大的网络，也许两级结构是不够的，还可以把区组合成簇（CLUSTER），把簇再组合成域（ZONE），对于等级式路由，在路由表中对应所有的本地路由器都有一个登录项，所有其他的区（本簇内）、簇（本域内）和域都缩减为单个路由器，因此减少了路由表的尺寸。 在本题中，4800=15*16*20。当选择 15 个簇、16 个区，每个区 20 个路由器时（或等效形式，例如 20 个簇、16 个区，每个区 15 个路由器），路由表尺寸最小，此时的路由表尺寸为 15+16+20=51。 

####22. Internet上一个网络的子网掩码为255.255.240.0。试问它最多能容纳多少台主机？

* 11111111.11111111.11110000.00000000

$$2^{12} -2$$

####23. 从198.16.0.0开始有大量连续的IP地址可以使用。假设4个组织A、B、C和D按照顺序依次申请4000、2000、4000和8000个地址。对于每一个申请，请用w.x.y.z/s的形式写出所分配的第一个IP地址、最后一个IP地址以及掩码。

*  198.00010000.00000000.00000000
A: 198.16.0.0 –198.16.15.255   198.16.0.0/20 
B: 198.16.16.0 – 198.23.15.255   198.16.16.0/21 
C: 198.16.32.0 – 198.47.15.255   198.16.32.0/20 
D: 198.16.64.0 – 198.95.15.255   198.16.64.0/19 


####24. 一个路由器刚刚接收到以下新的IP地址：57.6.96.0/21、57.6.104.0/21、57.6.112.0/21和57.6.120.0/21。如果所有这些地址都使用同一条出境线路，试问他们可以被聚合吗？如果可以，他们被聚合到哪个地址上？如果不可以，请问为什么？

* 57.6.01100000.0
* 57.6.01101000.0
* 57.6.01110000.0
* 57.6.01111000.0

* 聚合地址：57.6.96.0/19

####25. 一个路由器的路由表中有如下的表项：


地址/掩码   |   下一条
:-- | :--
135.46.56.0/22  | 0
135.46.60.0/22  | 1
192.53.40.0/23  | 1
Default         | 2


####对于下列IP地址，如果到达的数据包带有这些地址，试问路由器该如何处理？


    a) 135.46.63.10
    b) 135.46.57.14
    c) 135.46.52.2
    d) 192.53.40.7
    e) 192.53.56.7

1. 135.46.001110  00.0/22
2. 135.46.001111  00.0/22
3. 135.53.0010100  0.0/23

a)135.46.001111 11>1
b)135.46.001110 01>0
c)135.46.001101>2
d)192.53.00101000>1
e)192.53.00111000>2

###第六章

####26. 传输服务原语假设在两个端点之间建立连接的过程是不对称的，一端（服务器）执行LISTEN，而另一端（客户端）执行CONECT。然而，在对等应用中，比如BitTorrent那样的文件共享系统，所有的端点都是对等的。没有服务器或客户端功能之分。试问如何使用传输服务原语来构建这样的对等应用？

* 既是客户端也是服务器。

####27. 想象用两次握手过程而不是三次握手过程来建立连接。换句话说，第三个消息不再是要求的。试问现在有可能死锁吗？请给出一个例子说明存在死锁，或者证明死锁不存在。

* 我们知道，3 次握手完成两个重要功能，既要双方做好发送数据的准备工作（双方都知道彼此已准备好），也要允许双方就初始序列号进行协商，这个序列号在握手过程中被发送与确认。
 现在把三次握手改成仅需要两次握手，死锁是可能发生的。作为例子。考虑计算机 A 和B 之间的通信。假定 B 给 A 发送一个连接请求分组，A 收到了这个分组，并发送了确认应答分组。按照两次握手的协定，A 认为连接已经成功的建立了，可以开始发送数据分组。 可是，B 在 A 的应答分组在传输中被丢失的情况下，将不知道 A 是否已经准备好，不知道 A 建议什么样的序列号用于 A 到 B 的通，也不知道 A 是否同意 A 所建议的用于 B 到 A交通的初始序列号，B 甚至怀疑 A 是否收到己的连接请求分组。在这种情况下，B 认为连接还未建立成功，将忽略 A 发来的任何数据分组，只等待接收连接确认应答分组。而 A 在发出的分组超时后，重复发送同样的分组。这样就形成了死锁。 


####28. 一个客户通过一条1Gbps的光纤向100千米以外的服务器发送一个128字节的请求。试问在远过程调用中这条线路的效率是多少？

* 128 字节等于 1024 位，在 1Gb/s 的线路上发送 1000 位需要 1 的时间。光在光导纤维中的传播速度是 200km/ms，请求到达服务器需要传输 0.5ms 的时间，应答返回又需要 0.5ms 的传输时间。总的看来，1000 位在1ms 的时间内传输完成。这等效于 1Mb/s，即线路效率是 0.1%。 


####29. 请考虑在一条往返时间为10毫秒的无拥塞线路上使用慢速启动算法的效果。接收窗口为24KB，最大段长为2KB。试问需要多长时间才能首次发送满窗口的数据？

* 按照慢启动算法，经过 10、20、30、40ms 后拥塞窗口大小分别为 4、8、16、32，所以在 40ms 后将按照 min{24，32}=24KB 发送数据。 


####30. 假设TCP的拥塞窗口被设置为18KB，并且发生了超时。如果接下来的4次突发传输全部成功，试问拥塞窗口将达到多大？假设最大段长为1KB。

* 由于发生了超时，下一次传输将是 1 个最大报文段，然后是 2 个、4 个、8 个最大报文段，所以在 4 次突发量传输后，拥塞窗口将是 8K 字节。 

####31. 如果TCP往返时间RTT的当前值是30毫秒，紧接着分别在26、32、24毫秒确认到达，那么，若使用Jacobson算法，试问新的RTT估计值为多少？请使用α=0.9。

* 对于每一条连接，TCP 都维持一个变量 RTT，它是当前到达目的地的最佳估计值。当发送一个报文段的时候，启动计时器，察看应答要花多长时间，如果时间太长，就要重发报文段。如果应答在超时前返回，TCP 就测量应答花了多长时间，比如说是 M，然后用下列公式更新 RTT 值： 
 
 $$RTT=\alpha RTT+(1-\alpha)$$

现在，　a=0.9，RTT=30ms，M1=26，M2=32，M3=24 
所以， 

$$RTT=0.9 * 30+(1-0.9) * 26=29.6$$

$$RTT=0.9 * 29.6+(1-0.9) * 32=29.84$$

$$RTT=0.9 * 29.84+(1-0.9) * 24=29.256$$

因此，新的 RTT 29.256ms。 


####32. 一台TCP机器正在通过一条1Gbps的信道发送满窗口的65535字节数据，该信道的单向延迟为10毫秒。试问可以达到的最大吞吐量是多少？线路的效率是多少？

* 10ms*2=20ms 每 20ms 可以发送一个窗口大小的交通量，因此每秒 50 个窗口。 

$$65536×8×50=26.2Mb/s$$ 
 
 $$26.2/1000=2.6 % $$

所以，最大的数据吞吐率为 26.2Mb/s，线路效率为 2.6%。

