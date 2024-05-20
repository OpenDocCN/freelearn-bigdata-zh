# 前言

大数据-这是我们几年前探索 Spark 机器学习世界的动力。我们希望构建能够利用大量数据训练模型的机器学习应用程序，但一开始并不容易。Spark 仍在不断发展，它并不包含强大的机器学习库，我们仍在努力弄清楚构建机器学习应用程序意味着什么。

但是，逐步地，我们开始探索 Spark 生态系统的不同方面，并跟随 Spark 的发展。对我们来说，关键部分是一个强大的机器学习库，它将提供 R 或 Python 库所提供的功能。对我们来说，这是一项容易的任务，因为我们积极参与了 H2O 的机器学习库及其名为 Sparkling Water 的分支的开发，该分支使得可以从 Spark 应用程序中使用 H2O 库。然而，模型训练只是机器学习冰山的一角。我们还必须探索如何将 Sparkling Water 连接到 Spark RDDs、DataFrames 和 DataSets，如何将 Spark 连接到不同的数据源并读取数据，或者如何导出模型并在不同的应用程序中重用它们。

在我们的旅程中，Spark 也在不断发展。最初作为纯 Scala 项目，它开始提供 Python 和后来的 R 接口。它还将其 Spark API 从低级别的 RDDs 发展到高级别的 DataSet，并提供了类似 SQL 的接口。此外，Spark 还引入了机器学习管道的概念，这是从 Python 中已知的 scikit-learn 库中采用的。所有这些改进使 Spark 成为数据转换和数据处理的强大工具。

基于这种经验，我们决定通过这本书与世界其他地方分享我们的知识。它的目的很简单：通过示例演示构建 Spark 机器学习应用程序的不同方面，并展示如何不仅使用最新的 Spark 功能，还使用低级别的 Spark 接口。在我们的旅程中，我们还发现了许多技巧和捷径，不仅与 Spark 有关，还与开发机器学习应用程序或源代码组织的过程有关。所有这些都在本书中分享，以帮助读者避免我们所犯的错误。

本书采用 Scala 语言作为示例的主要实现语言。在使用 Python 和 Scala 之间做出了艰难的决定，但最终选择了 Scala。使用 Scala 的两个主要原因是：它提供了最成熟的 Spark 接口，大多数生产部署的应用程序都使用 Scala，主要是因为其在 JVM 上的性能优势。此外，本书中显示的所有源代码也都可以在线获取。

希望您喜欢我们的书，并且它能帮助您在 Spark 世界和机器学习应用程序的开发中进行导航。

# 本书涵盖的内容

第一章，*大规模机器学习简介*，邀请读者进入机器学习和大数据的世界，介绍了历史范式，并描述了包括 Apache Spark 和 H2O 在内的当代工具。

第二章，*探测暗物质：希格斯玻色子粒子*，着重介绍了二项模型的训练和评估。

第三章，*多类分类的集成方法*，进入健身房，并尝试基于从身体传感器收集的数据来预测人类活动。

第四章，*使用 NLP 预测电影评论*，介绍了使用 Spark 进行自然语言处理的问题，并展示了它在电影评论情感分析中的强大功能。

第五章，*使用 Word2Vec 进行在线学习*，详细介绍了当代自然语言处理技术。

第六章，*从点击流数据中提取模式*，介绍了频繁模式挖掘的基础知识和 Spark MLlib 中提供的三种算法，然后在 Spark Streaming 应用程序中部署了其中一种算法。

第七章，*使用 GraphX 进行图分析*，使读者熟悉图和图分析的基本概念，解释了 Spark GraphX 的核心功能，并介绍了 PageRank 等图算法。

﻿第八章，*Lending Club Loan Prediction*，结合了前几章介绍的所有技巧，包括数据处理、模型搜索和训练，以及作为 Spark Streaming 应用程序的模型部署的端到端示例。

# 本书所需内容

本书提供的代码示例使用 Apache Spark 2.1 及其 Scala API。此外，我们使用 Sparkling Water 软件包来访问 H2O 机器学习库。在每一章中，我们都会展示如何使用 spark-shell 启动 Spark，以及如何下载运行代码所需的数据。

总之，运行本书提供的代码的基本要求包括：

+   Java 8

+   Spark 2.1

# 本书适合的读者是谁

您是一位具有机器学习和统计背景的开发人员，感到当前的慢速和小数据机器学习工具限制了您的发展吗？那么这本书就是为您而写！在本书中，您将使用 Spark 创建可扩展的机器学习应用程序，以支持现代数据驱动的业务。我们假设您已经了解机器学习的概念和算法，并且已经在 Spark 上运行（无论是在集群上还是本地），并且具有对 Spark 中包含的各种库的基本知识。

# 约定

在本书中，您将找到一些文本样式，用于区分不同类型的信息。以下是一些样式的示例及其含义的解释。文本中的代码词、数据库表名、文件夹名、文件名、文件扩展名、路径名、虚拟 URL、用户输入和 Twitter 句柄显示如下：“我们还附加了魔术列`row_id`，它唯一标识数据集中的每一行。” 代码块设置如下：

```scala
import org.apache.spark.ml.feature.StopWordsRemover 
val stopWords= StopWordsRemover.loadDefaultStopWords("english") ++ Array("ax", "arent", "re")
```

当我们希望引起您对代码块的特定部分的注意时，相关行或项目将以粗体显示：

```scala
val MIN_TOKEN_LENGTH = 3
val toTokens= (minTokenLen: Int, stopWords: Array[String], 
```

任何命令行输入或输出都写成如下形式：

```scala
tar -xvf spark-2.1.1-bin-hadoop2.6.tgz 
export SPARK_HOME="$(pwd)/spark-2.1.1-bin-hadoop2.6 
```

**新术语**和**重要单词**以粗体显示。您在屏幕上看到的单词，例如菜单或对话框中的单词，会在文本中以这种方式出现：“按照以下截图下载 DECLINED LOAN DATA”

警告或重要提示会以这种形式出现。

技巧会以这种形式出现。

# 读者反馈

我们始终欢迎读者的反馈。请告诉我们您对本书的看法-您喜欢或不喜欢的地方。读者的反馈对我们很重要，因为它可以帮助我们开发出您真正能够从中受益的标题。要向我们发送一般反馈，只需发送电子邮件至`feedback@packtpub.com`，并在主题中提及书名。如果您在某个专题上有专业知识，并且有兴趣撰写或为一本书做出贡献，请参阅我们的作者指南，网址为[www.packtpub.com/authors](http://www.packtpub.com/authors)。

# 客户支持

现在您是 Packt 书籍的自豪所有者，我们有一些东西可以帮助您充分利用您的购买。

# 下载示例代码

您可以从[`www.packtpub.com`](http://www.packtpub.com)的帐户中下载本书的示例代码文件。如果您在其他地方购买了本书，您可以访问[`www.packtpub.com/support`](http://www.packtpub.com/support)并注册，以便直接通过电子邮件接收文件。您可以按照以下步骤下载代码文件：

1.  使用您的电子邮件地址和密码登录或注册我们的网站。

1.  将鼠标指针悬停在顶部的 SUPPORT 选项卡上。

1.  点击代码下载和勘误。

1.  在搜索框中输入书名。

1.  选择您要下载代码文件的书籍。

1.  从下拉菜单中选择您购买本书的地点。

1.  点击代码下载。

文件下载后，请确保使用最新版本的以下软件解压文件夹：

+   WinRAR / 7-Zip for Windows

+   Zipeg / iZip / UnRarX for Mac

+   7-Zip / PeaZip for Linux

该书的代码包也托管在 GitHub 上，网址为[`github.com/PacktPublishing/Mastering-Machine-Learning-with-Spark-2.x`](https://github.com/PacktPublishing/Mastering-Machine-Learning-with-Spark-2.x)。我们还有其他代码包来自我们丰富的书籍和视频目录，可在[`github.com/PacktPublishing/`](https://github.com/PacktPublishing/)找到。来看看吧！

# 下载本书的彩色图像

我们还为您提供了一个 PDF 文件，其中包含本书中使用的屏幕截图/图表的彩色图像。彩色图像将帮助您更好地理解输出中的变化。您可以从[`www.packtpub.com/sites/default/files/downloads/MasteringMachineLearningwithSpark2.x_ColorImages.pdf`](https://www.packtpub.com/sites/default/files/downloads/MasteringMachineLearningwithSpark2.x_ColorImages.pdf)下载此文件[﻿](https://www.packtpub.com/sites/default/files/downloads/MasteringMachineLearningwithSpark2.x_ColorImages.pdf)。

# 勘误

尽管我们已经尽一切努力确保内容的准确性，但错误确实会发生。如果您在我们的书籍中发现错误——可能是文本或代码中的错误——我们将不胜感激，如果您能向我们报告。通过这样做，您可以帮助其他读者避免挫败，并帮助我们改进本书的后续版本。如果您发现任何勘误，请访问[`www.packtpub.com/submit-errata`](http://www.packtpub.com/submit-errata)报告，选择您的书，点击勘误提交表格链接，并输入您的勘误详情。一旦您的勘误经过验证，您的提交将被接受，并且勘误将被上传到我们的网站或添加到该标题的勘误部分下的任何现有勘误列表中。要查看先前提交的勘误，请转到[`www.packtpub.com/books/content/support`](https://www.packtpub.com/books/content/support)，并在搜索框中输入书名。所需信息将显示在勘误部分下。

# 盗版

互联网上侵犯版权材料的盗版是所有媒体的持续问题。在 Packt，我们非常重视版权和许可的保护。如果您在互联网上发现我们作品的任何非法副本，请立即向我们提供位置地址或网站名称，以便我们采取补救措施。请通过`copyright@packtpub.com`与我们联系，并附上涉嫌盗版材料的链接。感谢您帮助我们保护我们的作者和我们提供有价值内容的能力。

# 问题

如果您对本书的任何方面有问题，可以通过`questions@packtpub.com`与我们联系，我们将尽力解决问题。
