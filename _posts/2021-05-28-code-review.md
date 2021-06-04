---
layout: post
title: (转)如何学习和阅读代码
categories: [review]
tags: [code review]
---

> 转自极客时间-左耳听风-《高效学习》系列整理



## 如何学习和阅读代码

### 读书还是读代码？

关于书/文档和代码的关系：

- 代码：What、How & Details；
- 书/文档：What、How & Why；

代码是具体的实现，但是并不能告诉你为什么？**书和文档是人对人说的话，代码是人对机器说的话**：

1. **如果想知道为什么要这么搞，应该去看书、看文档**：特别当我们想了解一种思想、一种方法、一种原理、一种经验时，书和文档是最佳的方式、更有效率一些；
2. **如果想知道是怎么实现的，实现的细节，应该去看代码**：对于具体的实现，比如：某协程的实现、某模块的性能、某个算法的实现，这时候最好的方式就是去读代码；

至于从代码中收获大还是从书中收获大，不同的场景、不同的目的下，会有不同的答案，我个人对这部分的想法是：

1. 工作的前几年，更多的时候应该关注代码、关注细节的实现、多写代码（当然不是说完全不看书，书是必须要看的，特别是当有了相关实战经验之后再去看书看，效果会更好），这个阶段，Google、Stack Overflow、Github 将会是最好的学习渠道，如果在过程中，还能获得一些技术影响力，那将再好不过了；
2. 有一定经验之后，这时候需要更多的【理性认识】，在这个阶段，我们的想法不再是实现某个功能，可能是想做出更牛逼的东西来，这时候应该多读那些大牛的书、与大牛交流、关注国际顶级会议的论文，应该让自己往技术 leader 这个方向发展。

### 如何阅读源代码

关于如何阅读源代码，耗子叔分享了一些干货，我这里简单总结一下

首先是阅读代码之前，最好先有以下了解：

1. 基础知识：相关的语言和基础技术的知识；
2. 软件功能：需要知道这个软件是做什么的、有哪些特性、哪些配置项，最好能够读一遍用户手册，然后让软件跑起来，自己先用一下感受一下；
3. 相关文档：读一下相关的内部文档；
4. 代码的组织结构：先简单看下源码的组织结构。

接下来，就是详细地看代码的实现，这里耗子叔分享了一个源代码阅读的经验：

1. **接口抽象定义**：任何代码都会有很多接口或抽象定义，其描述了代码需要处理的数据结构或者业务实体，以及它们之间的关系，理清楚这些关系是非常重要的；

2. **模块粘合层**：我们的代码有很多都是用来粘合代码的，比如中间件（middleware）、Promises 模式、回调（Callback）、代理委托、依赖注入等。这些代码模块间的粘合技术是非常重要的，因为它们会把本来平铺直述的代码给分裂开来，让你不容易看明白它们的关系；

3. **业务流程**：这是代码运行的过程。**一开始，我们不要进入细节，但需要在高层搞清楚整个业务的流程是什么样的**，在这个流程中，数据是怎么被传递和处理的。一般来说，我们需要**画程序流程图或者时序处理图**；

4. 具体实现

   ：了解上述的三个方面的内容，相信你对整个代码的框架和逻辑已经有了总体认识。这个时候，你就可以深入细节，开始阅读具体实现的代码了。对于代码的具体实现，一般来说，你需要知道下面一些事实，这样有助于你在阅读代码时找到重点。

   - **代码逻辑**：代码有两种逻辑，一种是**业务逻辑**，这种逻辑是真正的业务处理逻辑；另一种是**控制逻辑**，这种逻辑只是用控制程序流转的，不是业务逻辑。比如：flag 之类的控制变量，多线程处理的代码，异步控制的代码，远程通讯的代码，对象序列化反序列化的代码等。这两种逻辑你要分开，很多代码之所以混乱就是把这两种逻辑混在一起了；
   - **出错处理**：根据 2：8 原则，20% 的代码是正常的逻辑，80% 的代码是在处理各种错误，所以，你在读代码的时候，完全可以把处理错误的代码全部删除掉，这样就会留下比较干净和简单的正常逻辑的代码。排除干扰因素，可以更高效地读代码；
   - **数据处理**：只要你认真观察，就会发现，我们好多代码就是在那里倒腾数据。比如 DAO、DTO，比如 JSON、XML，这些代码冗长无聊，不是主要逻辑，可以不理；
   - **重要的算法**：一般来说，我们的代码里会有很多重要的算法，我说的并不一定是什么排序或是搜索算法，可能会是一些其它的核心算法，比如一些索引表的算法，全局唯一 ID 的算法，信息推荐的算法、统计算法、通读算法（如 Gossip）等。这些比较核心的算法可能会非常难读，但它们往往是最有技术含量的部分；
   - **底层交互**：有一些代码是和底层系统的交互，一般来说是和操作系统或是 JVM 的交互。因此，读这些代码通常需要一定的底层技术知识，不然，很难读懂；

5. **运行时调试**：很多时候，代码只有运行起来了，才能知道具体发生了什么事，所以，我们让代码运行进来，然后用日志也好，debug 设置断点跟踪也好。实际看一下代码的运行过程，是了解代码的一种很好的方式。

总结一下，阅读代码的方法如下。

- 一般采用自顶向下，从总体到细节的【剥洋葱皮】的读法；
- 画图是必要的，程序流程图，调用时序图，模块组织图；
- 代码逻辑归一下类，排除杂音，主要逻辑才会更清楚；
- debug 跟踪一下代码是了解代码在执行中发生了什么的最好方式。



另外这里也有个见解 https://www.codedump.info/post/20200605-how-to-read-code-v2020/ 兼听则明


---

看到这里或许你有建议或者疑问或者指出我的错误，请留言评论或者邮件mailto:wanghenshui@qq.com, 多谢!  你的评论非常重要！

<details>
<summary>觉得写的不错可以点开扫码赞助几毛</summary>
<img src="https://wanghenshui.github.io/assets/wepay.png" alt="微信转账">
</details>