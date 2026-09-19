# IX专线：云厂前置怎么配、四条线路怎么选，Mkcloud 最新套餐价格一览

搜「IX 专线」的人，大概分两类：一类是在 NodeSeek 这类论坛上看到别人聊深港 IXP、沪日 IXP，想知道这东西和 IPLC、IEPL 到底差在哪；另一类是手里已经有阿里云、腾讯云的机器，听说走云内网接 IX 专线比公网中转稳，想直接查价格和套餐。这篇文章按这两个问题展开：先讲清楚 IX 专线的原理和接入条件，再把 Mkcloud（mkcloud.net）目前在售的四条 IX 线路全部套餐和价格整理成表，最后说说哪些人适合买、哪些人买了也用不上。

## IX 专线到底是什么

IX 指 Internet Exchange Point，也就是互联网交换中心。它是不同网络互相交换流量的基础设施，各网络在交换中心里建立对等互联（Peering），互相访问时可以少绕路、少交中转费。国内目前没有成熟的商用 IX 环境，运营商之间的互联占主流，所以国内用户接触到的「IX 专线」基本都是海外的交换中心资源，比如香港的 Equinix IX、HKIX，日本的 JPIX、JPNAP。

Mkcloud 官方知识库对 IX 是什么、IX 专线和 IXP 接入的区别有专门解释，简单概括：你买到的不是自己接进交换中心的端口——零售 VPS 用户不需要自己的 ASN，那是交换中心成员才玩的东西。你买到的是一台出海 VPS，它的跨境路径经过商家在交换中心里优化过的网络资源，体现出来就是更低的端内延迟和更稳的晚高峰表现。

## 接入方式：先确认前置机，再看套餐

Mkcloud 的 IX 产品全称叫「上云互联优化专线」，这个名字已经说明了接入逻辑：**只允许云厂 BGP 网络连入**，你必须先有一台支持范围内的云服务器当前置，从它的内网或优化通道连到 IX VPS 的入口，再在 VPS 里向外访问。

每台 IX VPS 分配 1 个独立入口 IP 和 1 个独立出口 IP，进出各一个独享 IPv4。入口有云厂网络白名单保护，出口只出不进——不能拿出口 IP 建站、收回调或者跑游戏服务端。

前置机的支持范围按线路入口分两种：

- **深圳入口**（深港方向）：阿里云、腾讯云、百度云国内全网，加上火山云、华为云华南；
- **上海入口**（沪日、沪港、沪美方向）：阿里云、腾讯云、百度云国内全网，加上火山云、华为云、UCloud 华东。

具体以购物车页面为准，而且不是所有云厂所有地域都行，下单前先核对自己手上的云机在不在线。IX 不限连入省份，这点和直连产品不一样：广港、沪港这类直连款采用省级白名单，一次只允许一个省的 IP 连入（后续可以改）。如果你人在香港周边省份但云机在别处，IX 的灵活性反而是优势。

还有一条容易被忽略：前置云机本身的月租要算进总预算。IX 套餐单价看着低，加上前置机之后的总成本才是你实际花的钱。反过来，公司业务本来就跑在云上，前置机是现成的，IX 的价格优势就很直接了。

## 四条线路怎么选

Mkcloud 的 IX 产品线目前覆盖四个方向，官方知识库给了一张选型矩阵，我按延迟和用途整理如下：

| 线路 | 入口 | 出口 | 端内参考延迟 | 典型场景 |
| --- | --- | --- | --- | --- |
| 深港 IX | 云厂优化网络通道 | 香港 BGP | 1~2ms | 华南团队访问香港目标服务、后台操作 |
| 沪港 IX | 云厂优化网络通道 | 香港 BGP | 21ms | 华东方向对港业务 |
| 沪日 IX | 云厂优化网络通道 | 日本 BGP | 25~28ms | 日区后台、日本方向 API 与测试 |
| 沪美 IX | 云厂优化网络通道 | 美国 BGP | 124~134ms | 美区店铺后台、美国方向 API 与上传 |

几个背景信息帮你判断这些数字的含金量。深港 IX 走腾讯广州八线 BGP 接入，深圳到香港物理距离近，1~2ms 的端内延迟在跨境产品里属于地板级别；沪港方向官方统一标 21ms。日本 BGP 出口接入 PCCWG、NTT、Cogent、Lumen、Telstra、HE 等国际运营商，交换中心资源覆盖 Equinix IX、JPIX、BBIX、JPNAP，并有到 Google、Cloudflare、Valve、SGGS 的 PNI 私有互联；香港方向则接入 Equinix IX、HKIX，同样带 Google、Cloudflare、Valve 的 PNI。沪美的 124~134ms 是跨太平洋的物理距离决定的，任何中美线路都绕不开这个量级。

要注意这些全是**端内延迟**，不含你本地到前置机、出口到目标平台这两段公网。官方在知识库里反复强调这一点，避免有人拿 21ms 当全程延迟去预期。

不知道从哪条线路开始看的话，可以直接先浏览 Mkcloud IX 专线四个方向的全系套餐与实时价格，对配置和价格档位有个整体印象再回头细选。

## 全部 IX 套餐与价格（2026 年 9 月实测抓取自官网商店）

下面四个表覆盖 Mkcloud 官网当前展示的 IX 产品线全部流量计费套餐。计量型套餐流量按上行加下行双向合计，超量后停机，可自助购买流量重置（重置价格为原价 9 折）或提交工单补差价升级；共享带宽标注的是峰值，不保证持续跑满。所有套餐均为每台 1 个独立入口 IP 加 1 个独立出口 IP，支持月付、季付、半年付、年付等周期，系统可选 Ubuntu、Debian、CentOS、AlmaLinux 等。

**深港 IX（深圳-香港，端内 1~2ms）**

| 套餐 | 配置 | 带宽峰值 | 月流量 | 月付价格 | 购买链接 |
| --- | --- | --- | --- | --- | --- |
| 2TB | 2核4G / 40GB | 1Gbps | 2TB | ¥158 | [ 选购深港IX 2TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 4TB | 2核4G / 40GB | 1Gbps | 4TB | ¥258 | [ 选购深港IX 4TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 6TB | 4核8G / 40GB | 2Gbps | 6TB | ¥378 | [ 选购深港IX 6TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 10TB | 4核8G / 40GB | 2Gbps | 10TB | ¥826 | [ 选购深港IX 10TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 20TB | 4核8G / 40GB | 2Gbps | 20TB | ¥1,639 | [ 选购深港IX 20TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 30TB | 4核8G / 60GB | 3Gbps | 30TB | ¥2,458 | [ 选购深港IX 30TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 50TB | 8核8G / 60GB | 3Gbps | 50TB | ¥3,588 | [ 选购深港IX 50TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 100TB | 8核16G / 80GB | 5Gbps | 100TB | ¥7,168 | [ 选购深港IX 100TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 200TB | 8核16G / 80GB | 5Gbps | 200TB | ¥12,288 | [ 选购深港IX 200TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |
| 300TB | 8核16G / 80GB | 5Gbps | 300TB | ¥18,428 | [ 选购深港IX 300TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-hk-sz) |

**沪港 IX（上海-香港，端内 21ms）**

| 套餐 | 配置 | 带宽峰值 | 月流量 | 月付价格 | 购买链接 |
| --- | --- | --- | --- | --- | --- |
| 2TB | 2核4G / 40GB | 500Mbps | 2TB | ¥198 | [ 选购沪港IX 2TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |
| 3TB | 2核4G / 40GB | 500Mbps | 3TB | ¥288 | [ 选购沪港IX 3TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |
| 6TB | 4核8G / 40GB | 1Gbps | 6TB | ¥398 | [ 选购沪港IX 6TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |
| 10TB | 4核8G / 40GB | 1Gbps | 10TB | ¥666 | [ 选购沪港IX 10TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |
| 20TB | 4核8G / 40GB | 1Gbps | 20TB | ¥1,290 | [ 选购沪港IX 20TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |
| 30TB | 4核8G / 60GB | 2Gbps | 30TB | ¥1,900 | [ 选购沪港IX 30TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |
| 50TB | 8核8G / 60GB | 2Gbps | 50TB | ¥3,120 | [ 选购沪港IX 50TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-sh-hk-sh) |

**沪日 IX（上海-日本，端内 25~28ms）**

| 套餐 | 配置 | 带宽峰值 | 月流量 | 月付价格 | 购买链接 |
| --- | --- | --- | --- | --- | --- |
| 1TB | 2核4G / 40GB | 200Mbps | 1TB | ¥166 | [ 选购沪日IX 1TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 2TB | 2核4G / 40GB | 300Mbps | 2TB | ¥268 | [ 选购沪日IX 2TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 3TB | 2核4G / 40GB | 500Mbps | 3TB | ¥358 | [ 选购沪日IX 3TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 6TB | 4核8G / 40GB | 1Gbps | 6TB | ¥688 | [ 选购沪日IX 6TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 10TB | 4核8G / 40GB | 1Gbps | 10TB | ¥1,125 | [ 选购沪日IX 10TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 20TB | 4核8G / 40GB | 1Gbps | 20TB | ¥2,150 | [ 选购沪日IX 20TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 30TB | 4核8G / 60GB | 2Gbps | 30TB | ¥3,165 | [ 选购沪日IX 30TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |
| 50TB | 8核8G / 60GB | 2Gbps | 50TB | ¥5,222 | [ 选购沪日IX 50TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/cloud-jp-sh) |

**沪美 IX（上海-美国，端内 124~134ms）**

| 套餐 | 配置 | 带宽峰值 | 月流量 | 月付价格 | 购买链接 |
| --- | --- | --- | --- | --- | --- |
| 1TB | 1核2G / 20GB | 200Mbps | 1TB | ¥428 | [ 选购沪美IX 1TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/sh-us-sh) |
| 2TB | 2核4G / 40GB | 300Mbps | 2TB | ¥698 | [ 选购沪美IX 2TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/sh-us-sh) |
| 4TB | 2核4G / 40GB | 300Mbps | 4TB | ¥1,258 | [ 选购沪美IX 4TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/sh-us-sh) |
| 6TB | 4核8G / 60GB | 500Mbps | 6TB | ¥1,758 | [ 选购沪美IX 6TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/sh-us-sh) |
| 10TB | 4核8G / 60GB | 500Mbps | 10TB | ¥2,888 | [ 选购沪美IX 10TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/sh-us-sh) |
| 20TB | 4核8G / 60GB | 1Gbps | 20TB | ¥5,666 | [ 选购沪美IX 20TB套餐](https://www.mkcloud.net/aff.php?aff=390&url=https://www.mkcloud.net/index.php/store/sh-us-sh) |

除流量计费款外，IX 产品也有带宽计费的独享带宽版本（5M 到 5G 共 11 个档位，不限流量），香港、日本、美国方向都有；另外深港方向还有 4-8 核、2-5Gbps 峰值的大流量 IXP 系列在售。这类按带宽计费的产品适合持续大流量传输，这里不逐档展开，具体报价见对应商店页。沪日 IX 年付版的历史参考为 1TB 流量档 1188 元/年（折合约 99 元/月），现售规格和周期价格以购物车实时显示为准。

## 流量规则、退款和付款方式

购买前有几条硬规则需要知道，全部来自官方商店页和知识库：

> 流量按上行、下行双向统计。你看到的「2TB」是上下行之和，实际业务流量要按一半估算，跑直播推流这类双向大户时尤其要留余量。

- **超量停机**：计量型套餐流量用完即停，可自助购买流量重置（原价 9 折）或工单补差价升级，不影响原重置周期和到期时间。
- **退款政策**：仅支持质量问题退款，需要提交准确的延迟、速度数据作证据；开通后不支持更换到其他地域。
- **实名与用途**：所有产品需中国身份信息实名，禁止机场、回国等违规用途，违规清退不退款。
- **付款**：目前只支持支付宝。
- **开通速度**：官方口径为多数 VPS 约 1 分钟自动开通，标准产品默认无 SLA，有可用性指标要求需走付费定制。

## 优惠情况：老码已过期，现看活动页

Mkcloud 过去一年跑过不少促销：双旦活动有全场流量计费产品 8.8 折循环码 MK-8.8、独享带宽首月 7.8 折码 MK-7.8 和新客码 MK-NEW；五一、国庆、新春等节点也发过限时折扣码。但官方在知识库里对每个活动回顾都标注了「活动已结束、优惠码仅在活动期内有效」，所以**上面这些码现在都别当有效信息用**。

当前确定有效的只有推广联盟的返佣规则：通过推广链接成交，商家按订单实付金额给推荐人 10% 一次性佣金，满 200 元可提现到支付宝或账户余额。买家侧的常规优惠，建议下单前在 [👉 Mkcloud 商店与结账页查看当前优惠券和活动](https://bit.ly/MKCLoud)，结账页登录后会显示你账号可用的优惠券，比追历史活动帖靠谱。

## 什么样的人该买 IX，什么样的人不该

结合配置、价格和接入条件，IX 专线的适用面其实很清晰。

**适合的场景**：业务本来就跑在阿里云、腾讯云这类云厂上的团队，前置机是现成的，加一台 IX VPS 就能把出海路径换成专线质量；做美区、日区店铺后台和 API 访问的卖家，双独享 IP 加固定出口比公网 VPS 的共享环境可控得多；预算敏感但对晚高峰稳定性有要求的用户，沪日 IX 1TB 月付 166 元、深港 IX 2TB 月付 158 元，比同方向 IPLC（沪日起步 358 元）便宜一半左右，官方店铺也把 6000+ 跨境电商客户数挂在首页，NodeSeek 上关于深港 IX 的讨论里也有用户反馈晚高峰出口表现稳定。

**不适合的场景**：没有云厂机器、也不想为一台前置机多花一份月租的个人用户，直连款或者干脆公网 VPS 更省事；需要用出口 IP 建站、收支付回调、跑游戏服务端的人，IX 出口不收入站，这类需求得看独立服务器方案；预期「专线等于全程 1ms、永不掉线」的人，端内延迟不等于全程延迟，标准套餐也没有 SLA 承诺。

最后提醒一句购买顺序：先确认自己的云机在支持列表里，再选方向和流量档，付款前把双向流量和前置机成本都算进预算。想直接对比四个方向的档位，可以从 [👉 Mkcloud IX 专线全系套餐入口](https://bit.ly/MKCLoud) 进商店逐条核对，价格以购物车实时显示为准。
