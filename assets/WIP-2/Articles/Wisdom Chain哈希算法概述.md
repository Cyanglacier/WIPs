# Wisdom Chain 哈希算法概述

### 前言
 **哈希（Hash）** 算法，又叫散列算法，它既是密码学领域最有名的技术之一，也是目前互联网领域众多技术与应用的基础，区块链也是如此。哈希算法可以将任意长度的明文（在计算机中一般表达为二进制码）通过特定的计算算法输出一段固定长度的哈希值，以此来为明文数据提供类似“标签”、“摘要”的功能。随着技术的不断发展，到目前为止已经有非常多的哈希算法可供选择，这些算法都或多或少有着自己的特点，适用于不同的应用领域，例如比特币就采用了SHA-256与RIPEMD-160作为基础哈希函数，为钱包地址生成和区块生产提供安全性；以太坊则采用了基于Keccak改进的Ethash作为挖矿哈希函数。而在Wisdom Chain中，矿工出块时可使用的哈希函数包括**WhirlpoolDigest、RIPEMD-256、BLAKE2b-256、SHA3-256/Keccak-256、Skein256**在内总计5种，这些挖矿函数究竟什么区别，他们各自又有什么特点呢？

### WhirpoolDigest
WhirlpoolDigest源于Whirlpool哈希函数，最早由Vincent Rijmen和Paulo Barreto在2000年提出，目前该哈希函数被NEESSIE项目所推荐，同样也被ISO和IEC标准所采纳（ISO/IEC 10118-3）。Whirlpool本意是指“河水或海水中形成的漩涡”。Whirlpool属于密码学中的“分组密码学”范畴，根据Square结构进行设计，使用的数值转化技术和AES加密标准（对称式加密）相同，不过在模函数上不同于AES。此外，Whirlpool的输出位数为512位，对于接受的所有长度小于2^256位数值，Whirlpool都会输出相同位数的摘要信息，或者说哈希值。
目前Whirlpool经过了20年的发展，已经有了数个版本的更新。原始版本的Whirlpool被称为Whirlpool-0，其第一个稳定版本则被称为Whirlpool-T，最新版本则被称为Whirlpool/x，x代表着测试版本代号。Whirlpool的作者们并未对该哈希函数申请专利，同其他密码学先驱一样，他们将Whirlpool进行了开源，这种精神也让Whirlpool被多个加密软件所应用（如TrueCrypt和VeraCrypt等等）。

### RIPEMD-256
RIPEMD是RIPE Message Digest的简称，中文又叫做“RACE原始完整性校验讯息摘要”。该哈希函数最早由鲁汶大学的COSIC研究小组于1996年发布。不同于Whirlpool源于AES的结构，RIPEMD的算法结构是基于MD4进行设计的，就表现形式上与同样基于MD4设计的SHA-1哈希函数类似。RIPEMD根据算法位数的不同，分为了RIPEMD-128，RIPEMD-160，RIPEMD-256等等不同的版本。目前RIPEMD的原始版本已经发生了哈希碰撞，从安全性角度考虑已不建议使用原始版本，但RIPEMD-128，RIPEMD-256等暂未出现碰撞报告，可以认为是安全的。值得一提的是，由于RIPEMD的设计，修改位数没有有效提升函数的安全级（因为算法没有做出更改），仅仅只是通过提高输出位数来降低碰撞的概率。
同Whirlpool一样，RIPEMD哈希函数也是开源且免费使用的。

### BLAKE2b-256
BLAKE2b-256源于BLAKE哈希函数。Blake哈希函数由Jean-Philippe Aumasson, Luca Henzen, Willi Meier, Raphael Phan共同设计完成，也是SHA-3竞赛的入围函数，虽然SHA-3竞赛最后的胜出者是Keccak函数，但入围的哈希函数都被证明有着极其优秀的结构与效率，Blake哈希函数具有两种不同的字变体，BLAKE-256和BLAKE-224使用32位字，分别产生256位和224位的摘要大小，而BLAKE-512和BLAKE-384分别使用64位字，产生512位和384位的摘要大小。同样的，Blake哈希函数也有相应的改进版本。Blake2哈希函数是Blake函数于2012年12月推出的改进版本，而Blake3则是Blake2的改进版，已于2020年提出。Blake2b则是BLAKE2算法的64位字版本，其最高可以生成512位的哈希值，而生成256位哈希值的Blake2b算法则被称为Blake2b-256。

### SHA3-256/Keccak-256
虽然有着不同的名字，但实际上Keccak算法与SHA3算法基本是一致的。从2007年开始，NIST（国家标准技术研究所）开始向全球征集全新的哈希算法SHA-3，在SHA-3竞赛中胜出的便是Guido Bertoni等人设计的Keccak哈希函数，2015年8月，Keccak正式作为SHA-3由NIST发表。Keccak采用了海绵函数结构，这令其拥有更快的计算速度，并且不会对硬件配置作出太高要求，Intel 奔腾3执行性能大约是57.4cpb。而根据输出哈希值位数的不同，SHA-3/Keccak又分为了SHA3-224、SHA3-256、SHA3-384、SHA3-512等，他们的算法并无差距，仅在输出位数上有所区别（计算速度也和位数呈正比）。

### Skein256
