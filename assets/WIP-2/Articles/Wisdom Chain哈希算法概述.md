# Wisdom Chain 哈希算法概述

### 前言
**哈希（Hash）**算法，又叫散列算法，它既是密码学领域最有名的技术之一，也是目前互联网领域众多技术与应用的基础，区块链也是如此。哈希算法可以将任意长度的明文（在计算机中一般表达为二进制码）通过特定的计算算法输出一段固定长度的哈希值，以此来为明文数据提供类似“标签”、“摘要”的功能。随着技术的不断发展，到目前为止已经有非常多的哈希算法可供选择，这些算法都或多或少有着自己的特点，适用于不同的应用领域，例如比特币就采用了SHA-256与RIPEMD-160作为基础哈希函数，为钱包地址生成和区块生产提供安全性；以太坊则采用了基于Keccak改进的Ethash作为挖矿哈希函数。而在Wisdom Chain中，矿工出块时可使用的哈希函数包括**WhirlpoolDigest、RIPEMD-256、BLAKE2b-256、SHA3-256、Keccak-256、Skein256**在内总计6种，这些挖矿函数究竟什么区别，他们各自又有什么特点呢？

### WhirpoolDigest
WhirlpoolDigest源于Whirlpool哈希函数，最早由Vincent Rijmen和Paulo Barreto在2000年提出，目前该哈希函数被NEESSIE项目所推荐，同样也被ISO和IEC标准所采纳（ISO/IEC 10118-3）。Whirlpool本意是指“河水或海水中形成的漩涡”。Whirlpool属于密码学中的“分组密码学”范畴，根据Square结构进行设计，使用的数值转化技术和AES加密标准（对称式加密）相同，不过在模函数上不同于AES。此外，Whirlpool的输出位数为512位，对于接受的所有长度小于2^256位数值，Whirlpool都会输出相同位数的摘要信息，或者说哈希值。
目前Whirlpool经过了20年的发展，已经有了数个版本的更新。原始版本的Whirlpool被称为Whirlpool-0，其第一个稳定版本则被称为Whirlpool-T，最新版本则被称为Whirlpool/x，x代表着测试版本代号。Whirlpool的作者们并未对该哈希函数申请专利，同其他密码学先驱一样，他们将Whirlpool进行了开源，这种精神也让Whirlpool被多个加密软件所应用（如TrueCrypt和VeraCrypt等等）。

### RIPEMD-256
