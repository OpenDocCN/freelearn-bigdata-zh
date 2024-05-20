# 前言

我们将从 Spark SQL 的基础知识和其在 Spark 应用中的作用开始。在对 Spark SQL 进行初步了解之后，我们将专注于使用 Spark SQL 执行所有大数据项目常见的任务，如处理各种类型的数据源、探索性数据分析和数据整理。我们还将看到如何利用 Spark SQL 和 SparkR 来实现典型的大规模数据科学任务。

作为 Spark SQL 核心的 DataFrame/Dataset API 和 Catalyst 优化器，在基于 Spark 技术栈的所有应用中发挥关键作用并不奇怪。这些应用包括大规模机器学习管道、大规模图应用和新兴的基于 Spark 的深度学习应用。此外，我们还将介绍基于 Spark SQL 的结构化流应用，这些应用部署在复杂的生产环境中作为连续应用。

我们还将回顾 Spark SQL 应用中的性能调优，包括 Spark 2.2 中引入的基于成本的优化（CBO）。最后，我们将介绍利用 Spark 模块和 Spark SQL 在实际应用中的应用架构。具体来说，我们将介绍大规模 Spark 应用中的关键架构组件和模式，这些组件和模式对架构师和设计师来说将是有用的构建块，用于他们自己特定用例的构建。

# 本书内容

第一章《开始使用 Spark SQL》概述了 Spark SQL，并通过实践让您熟悉 Spark 环境。

第二章《使用 Spark SQL 处理结构化和半结构化数据》将帮助您使用 Spark 处理关系数据库（MySQL）、NoSQL 数据库（MongoDB）、半结构化数据（JSON）以及 Hadoop 生态系统中常用的数据存储格式（Avro 和 Parquet）。

第三章《使用 Spark SQL 进行数据探索》演示了使用 Spark SQL 来探索数据集，执行基本的数据质量检查，生成样本和数据透视表，并使用 Apache Zeppelin 可视化数据。

第四章《使用 Spark SQL 进行数据整理》使用 Spark SQL 执行一些基本的数据整理/处理任务。它还向您介绍了一些处理缺失数据、错误数据、重复记录等技术。

第五章《在流应用中使用 Spark SQL》提供了使用 Spark SQL DataFrame/Dataset API 构建流应用的几个示例。此外，它还展示了如何在结构化流应用中使用 Kafka。

第六章《在机器学习应用中使用 Spark SQL》专注于在机器学习应用中使用 Spark SQL。在本章中，我们将主要探讨特征工程的关键概念，并实现机器学习管道。

第七章《在图应用中使用 Spark SQL》向您介绍了 GraphFrame 应用。它提供了使用 Spark SQL DataFrame/Dataset API 构建图应用并将各种图算法应用于图应用的示例。

第八章《使用 Spark SQL 与 SparkR》涵盖了 SparkR 架构和 SparkR DataFrames API。它提供了使用 SparkR 进行探索性数据分析（EDA）和数据整理任务、数据可视化和机器学习的代码示例。

第九章，*使用 Spark SQL 开发应用程序*，帮助您使用各种 Spark 模块构建 Spark 应用程序。它提供了将 Spark SQL 与 Spark Streaming、Spark 机器学习等相结合的应用程序示例。

第十章，*在深度学习应用程序中使用 Spark SQL*，向您介绍了 Spark 中的深度学习。在深入使用 BigDL 和 Spark 之前，它涵盖了一些流行的深度学习模型的基本概念。

第十一章，*调整 Spark SQL 组件以提高性能*，向您介绍了与调整 Spark 应用程序相关的基本概念，包括使用编码器进行数据序列化。它还涵盖了在 Spark 2.2 中引入的基于成本的优化器的关键方面，以自动优化 Spark SQL 执行。

第十二章，*大规模应用架构中的 Spark SQL*，教会您识别 Spark SQL 可以在大规模应用架构中实现典型功能和非功能需求的用例。

# 本书所需内容

本书基于 Spark 2.2.0（为 Apache Hadoop 2.7 或更高版本预构建）和 Scala 2.11.8。由于某些库的不可用性和报告的错误（在与 Apache Spark 2.2 一起使用时），也使用了 Spark 2.1.0 来进行一两个小节的讨论。硬件和操作系统规格包括最低 8GB RAM（强烈建议 16GB）、100GB HDD 和 OS X 10.11.6 或更高版本（或建议用于 Spark 开发的适当 Linux 版本）。

# 本书的受众

如果您是开发人员、工程师或架构师，并希望学习如何在大规模网络项目中使用 Apache Spark，那么这本书适合您。假定您具有 SQL 查询的先前知识。使用 Scala、Java、R 或 Python 的基本编程知识就足以开始阅读本书。

# 约定

在本书中，您将找到几种文本样式，用于区分不同类型的信息。以下是这些样式的一些示例及其含义的解释。

文本中的代码词，数据库表名，文件夹名，文件名，文件扩展名，路径名，虚拟 URL，用户输入和终端命令如下："通过在训练数据集上调用`fit()`方法来训练模型。"

代码块设置如下：

```scala
scala> val inDiaDataDF = spark.read.option("header", true).csv("file:///Users/aurobindosarkar/Downloads/dataset_diabetes/diabetic_data.csv").cache()
```

任何命令行输入或输出都将如下所示：

```scala
head -n 8000 input.txt > val.txt
tail -n +8000 input.txt > train.txt
```

**新术语**和**重要单词**以粗体显示。例如，您在屏幕上看到的单词，例如菜单或对话框中的单词，会以这种方式出现在文本中："单击“下一步”按钮将您移至下一个屏幕。"

警告或重要说明会出现如下。

技巧和窍门会出现如下。

# 读者反馈

我们一直欢迎读者的反馈。请告诉我们您对本书的看法-您喜欢或不喜欢的内容。读者的反馈对我们很重要，因为它有助于我们开发出真正能让您受益的标题。

要向我们发送一般反馈，只需发送电子邮件至`feedback@packtpub.com`，并在主题中提及书名。

如果您在某个专题上拥有专业知识，并且有兴趣撰写或为书籍做出贡献，请参阅我们的作者指南[www.packtpub.com/authors](http://www.packtpub.com/authors)。

# 客户支持

现在您是 Packt 图书的自豪所有者，我们有几件事可以帮助您充分利用您的购买。

# 下载示例代码

您可以从[`www.packtpub.com`](http://www.packtpub.com)的帐户中下载本书的示例代码文件。如果您在其他地方购买了本书，可以访问[`www.packtpub.com/support`](http://www.packtpub.com/support)并注册，以便直接通过电子邮件接收文件。

您可以按照以下步骤下载代码文件：

1.  使用您的电子邮件地址和密码登录或注册我们的网站。

1.  将鼠标指针悬停在顶部的“支持”选项卡上。

1.  单击“代码下载和勘误”。

1.  在搜索框中输入书名。

1.  选择您要下载代码文件的书籍。

1.  从下拉菜单中选择您购买本书的地点。

1.  单击“代码下载”。

下载文件后，请确保使用最新版本的解压缩软件解压缩文件夹：

+   WinRAR / Windows 7-Zip

+   Mac 的 Zipeg / iZip / UnRarX

+   Linux 的 7-Zip / PeaZip

该书的代码包也托管在 GitHub 上，网址为[`github.com/PacktPublishing/Learning-Spark-SQL`](https://github.com/PacktPublishing/Learning-Spark-SQL)。我们还有其他代码包来自我们丰富的图书和视频目录，可在[`github.com/PacktPublishing/`](https://github.com/PacktPublishing/)上找到。来看看吧！

# 下载本书的彩色图像

我们还为您提供了一个 PDF 文件，其中包含本书中使用的屏幕截图/图表的彩色图像。彩色图像将帮助您更好地理解输出中的变化。您可以从[`www.packtpub.com/sites/default/files/downloads/LearningSparkSQL_ColorImages.pdf`](https://www.packtpub.com/sites/default/files/downloads/LearningSparkSQL_ColorImages.pdf)下载此文件。

# 勘误

尽管我们已经尽一切努力确保内容的准确性，但错误确实会发生。如果您在我们的书籍中发现错误-可能是文本或代码中的错误-我们将不胜感激，如果您能向我们报告。通过这样做，您可以帮助其他读者免受挫折，并帮助我们改进本书的后续版本。如果您发现任何勘误，请访问[`www.packtpub.com/submit-errata`](http://www.packtpub.com/submit-errata)，选择您的书籍，单击“勘误提交表”链接，并输入您的勘误详情。一旦您的勘误经过验证，您的提交将被接受，并且勘误将被上传到我们的网站或添加到该标题的勘误部分的任何现有勘误列表中。

要查看先前提交的勘误，请访问[`www.packtpub.com/books/content/support`](https://www.packtpub.com/books/content/support)，并在搜索字段中输入书名。所需信息将出现在勘误部分下。

# 盗版

互联网上侵犯版权材料的盗版是所有媒体的持续问题。在 Packt，我们非常重视保护我们的版权和许可。如果您在互联网上发现我们作品的任何非法副本，请立即向我们提供位置地址或网站名称，以便我们采取补救措施。请通过`copyright@packtpub.com`与我们联系，并附上涉嫌盗版材料的链接。我们感谢您帮助保护我们的作者以及我们提供有价值内容的能力。

# 问题

如果您对本书的任何方面有问题，可以通过`questions@packtpub.com`与我们联系，我们将尽力解决问题。
