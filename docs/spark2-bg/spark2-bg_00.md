# 前言

数据处理框架 Spark 最初是为了证明，通过在多次迭代中重用数据集，它在 Hadoop MapReduce 作业表现不佳的地方提供了价值。研究论文《Mesos：数据中心细粒度资源共享平台》讨论了 Spark 设计背后的哲学。加州大学伯克利分校的研究人员为测试 Mesos 而构建的一个非常简单的参考实现，已经远远超越了最初的用途，发展成为一个完整的数据处理框架，后来成为最活跃的 Apache 项目之一。它从一开始就被设计用于在 Hadoop、Mesos 等集群上进行分布式数据处理，以及在独立模式下运行。Spark 是一个基于 JVM 的数据处理框架，因此它可以在支持基于 JVM 的应用程序的大多数操作系统上运行。Spark 广泛安装在 UNIX 和 Mac OS X 平台上，而 Windows 上的采用也在增加。

Spark 通过编程语言 Scala、Java、Python 和 R 提供了一个统一的编程模型。换句话说，无论使用哪种语言编写 Spark 应用程序，API 在所有语言中几乎都是相同的。这样，组织可以采用 Spark 并在他们选择的编程语言中开发应用程序。这也使得在需要时可以快速将 Spark 应用程序从一个语言移植到另一个语言，而无需太多努力。Spark 大部分是用 Scala 开发的，因此 Spark 编程模型本质上支持函数式编程原则。最基本的 Spark 数据抽象是弹性分布式数据集（RDD），基于此构建了所有其他库。基于 RDD 的 Spark 编程模型是开发者可以构建数据处理应用程序的最低级别。

Spark 迅速发展，以满足更多数据处理用例的需求。当采取这种前瞻性的产品路线图步骤时，出现了对商业用户进行更高级别编程的需求。基于 Spark 核心的 Spark SQL 库，以其 DataFrame 抽象，被构建来满足大量非常熟悉无处不在的 SQL 的开发者的需求。

数据科学家使用 R 语言进行计算需求。R 语言最大的限制是所有需要处理的数据都应该*适合*运行 R 程序的计算机的主内存。Spark 为 R 语言引入的 API 让数据科学家们熟悉了在熟悉的数据帧抽象中的分布式数据处理世界。换句话说，使用 R 语言的 Spark API，数据处理可以在 Hadoop 或 Mesos 上并行进行，远远超出了主机内存的限制。

在当前大规模应用收集数据的时代，摄入数据的速率非常高。许多应用场景要求对流式数据进行实时处理。建立在 Spark Core 之上的 Spark Streaming 库正是为此而设计。

静态数据或流式数据被输入机器学习算法以训练数据模型，并使用这些模型来回答业务问题。在 Spark 之前创建的所有机器学习框架在处理计算机的内存、无法进行并行处理、重复的读写周期等方面存在许多限制。Spark 没有这些限制，因此建立在 Spark Core 和 Spark DataFrames 之上的 Spark MLlib 机器学习库成为了最佳的机器学习库，它将数据处理管道和机器学习活动紧密结合。

图是一种非常有用的数据结构，在某些特殊用例中被大量使用。用于处理图数据结构的算法计算密集。在 Spark 之前，出现了许多图处理框架，其中一些处理速度非常快，但生成图数据结构所需的数据预处理在大多数图处理应用中成为了一个巨大的瓶颈。建立在 Spark 之上的 Spark GraphX 库填补了这一空白，使得数据处理和图处理成为链式活动。

过去，存在许多数据处理框架，其中许多是专有的，迫使组织陷入供应商锁定的陷阱。Spark 为各种数据处理需求提供了一个非常可行的替代方案，且无需许可费用；同时，它得到了许多领先公司的支持，提供专业的生产支持。

# 本书涵盖的内容

第一章，*Spark 基础*，探讨了 Spark 作为一个框架的基本原理，包括其 API 和随附的库，以及 Spark 与之交互的整个数据处理生态系统。

第二章，*Spark 编程模型*，讨论了基于函数式编程方法论的统一编程模型，该模型在 Spark 中使用，并涵盖了弹性分布式数据集（RDD）的基础、Spark 转换和 Spark 操作。

第三章，*Spark SQL*，讨论了 Spark SQL，这是最强大的 Spark 库之一，用于使用无处不在的 SQL 结构以及 Spark DataFrame API 来操作数据，并探讨了它如何与 Spark 程序协同工作。本章还讨论了如何使用 Spark SQL 从各种数据源访问数据，实现对多样数据源的数据处理统一。

第四章，*使用 R 进行 Spark 编程*，讨论了 SparkR 或 R on Spark，这是 Spark 的 R API；这使得 R 用户能够利用 Spark 的数据处理能力，使用他们熟悉的数据帧抽象。它为 R 用户提供了一个很好的基础，以便熟悉 Spark 数据处理生态系统。

第五章，*使用 Python 进行 Spark 数据分析*，讨论了使用 Spark 进行数据处理和使用 Python 进行数据分析，利用了 Python 提供的各种图表和绘图库。本章讨论了将这两项相关活动结合在一起，作为使用 Python 作为首选编程语言的 Spark 应用程序。

第六章，*Spark 流处理*，讨论了 Spark Streaming，这是用于捕获和处理以流形式输入的数据的最强大的 Spark 库之一。还讨论了作为分布式消息代理的 Kafka 和作为消费者的 Spark Streaming 应用程序。

第七章，*Spark 机器学习*，探讨了 Spark MLlib，这是用于开发入门级机器学习应用程序的最强大的 Spark 库之一。

第八章，*Spark 图处理*，讨论了 Spark GraphX，这是处理图数据结构的最强大的 Spark 库之一，并附带了许多用于图数据处理的算法。本章涵盖了 GraphX 的基础知识以及使用 GraphX 提供的算法实现的一些用例。

第九章，*设计 Spark 应用程序*，讨论了 Spark 数据处理应用程序的设计和开发，涵盖了本书前几章中介绍的 Spark 的各种特性。

# 本书所需条件

Spark 2.0.0 或更高版本需要安装在至少一台独立机器上，以运行代码示例并进行进一步的活动，以更深入地了解该主题。对于第六章，*Spark 流处理*，需要安装并配置 Kafka 作为消息代理，其命令行生产者产生消息，而使用 Spark 开发的应用程序作为这些消息的消费者。

# 本书面向的读者

如果你是应用程序开发者、数据科学家或大数据解决方案架构师，并对将 Spark 的数据处理能力与 R 结合，以及将数据处理、流处理、机器学习、图处理整合到一个统一且高度互操作的框架中，使用统一的 API（Scala 或 Python）感兴趣，那么这本书适合你。

# 约定

在本书中，您会发现多种文本样式用于区分不同类型的信息。以下是这些样式的一些示例及其含义的解释。

文本中的代码词、数据库表名、文件夹名、文件名、文件扩展名、路径名、虚拟 URL、用户输入和 Twitter 句柄如下所示："将此属性`spark.driver.memory`设置为更高值是个好主意。"

代码块设置如下：

```scala
Python 3.5.0 (v3.5.0:374f501f4567, Sep 12 2015, 11:00:19)
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
```

任何命令行输入或输出书写如下：

```scala
$ python 
Python 3.5.0 (v3.5.0:374f501f4567, Sep 12 2015, 11:00:19)  
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin 
Type "help", "copyright", "credits" or "license" for more information. 
>>> 

```

**新术语**和**重要词汇**以粗体显示。屏幕上出现的词汇，例如在菜单或对话框中，在文本中这样呈现："本书中的快捷键基于`Mac OS X 10.5+`方案。"

### 注意

警告或重要提示以这样的方框形式出现。

### 提示

提示和技巧这样呈现。
