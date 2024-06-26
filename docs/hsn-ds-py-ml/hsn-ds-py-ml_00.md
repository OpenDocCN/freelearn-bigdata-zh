# 前言

成为科技行业的数据科学家是当今地球上最有价值的职业之一。我去研究了科技公司数据科学家职位的实际工作描述，并将这些要求归纳为您将在本课程中看到的主题。

《动手做数据科学和 Python 机器学习》真的非常全面。我们将从 Python 的速成课程开始，然后回顾一些基本的统计和概率知识，但接着我们将直接涉及超过 60 个数据挖掘和机器学习的主题。其中包括贝叶斯定理、聚类、决策树、回归分析、实验设计；我们将全面研究它们。其中一些主题真的非常有趣。

我们将开发一个实际的电影推荐系统，使用实际的用户电影评分数据。我们将创建一个真正适用于维基百科数据的搜索引擎。我们将构建一个可以正确分类垃圾邮件和非垃圾邮件的垃圾邮件分类器，并且我们还有一个关于将这项工作扩展到在大数据上运行的集群的整个部分，使用 Apache Spark。

如果您是一名软件开发人员或程序员，希望转向数据科学职业，这门课程将教会您最热门的技能，而不需要所有这些数学符号和伪装，这些都是与这些主题相关的。我们只会解释这些概念，并向您展示一些真正有效的 Python 代码，您可以深入研究并进行操作，以使这些概念深入人心，如果您在金融行业担任数据分析师，这门课程也可以教会您转向科技行业。您只需要一些编程或脚本编写的经验，就可以开始了。

这本书的一般格式是我将从每个概念开始，用一堆部分和图形示例来解释它。我会向您介绍一些数据科学家喜欢使用的符号和花哨的术语，这样您就可以用相同的语言交流，但这些概念本身通常非常简单。之后，我会让您实际运行一些真正有效的 Python 代码，让我们可以运行并进行一些操作，并且这将向您展示如何将这些想法应用到实际数据中。这些将被呈现为 IPython Notebook 文件，这是一种我可以在其中混合代码和解释代码周围的笔记的格式，解释概念中发生的事情。在阅读完本书后，您可以将这些笔记本文件带走，并在以后的职业生涯中使用它作为方便的快速参考，而在每个概念的结尾，我会鼓励您实际深入研究 Python 代码，进行一些修改，进行一些操作，并通过实际进行一些修改，看到它们产生的效果，从而更加熟悉。

# 这本书是为谁准备的

如果您是一名新兴的数据科学家或数据分析师，希望使用 Python 分析数据并获得可操作的见解，那么这本书适合您。有一些 Python 经验的程序员，希望进入数据科学这个利润丰厚的领域，也会发现这本书非常有用。

# 约定

在这本书中，您将找到许多文本样式，用于区分不同类型的信息。以下是这些样式的一些示例以及它们的含义解释。

文本中的代码词、数据库表名、文件夹名、文件名、文件扩展名、路径名、虚拟 URL、用户输入和 Twitter 用户名显示如下："我们可以使用`sklearn.metrics`中的`r2_score()`函数来衡量这个。"

代码块设置如下：

```py
import numpy as np 
import pandas as pd 
from sklearn import tree 

input_file = "c:/spark/DataScience/PastHires.csv" 
df = pd.read_csv(input_file, header = 0) 

```

当我们希望引起您对代码块的特定部分的注意时，相关行或项目将以粗体显示：

```py
import numpy as np
import pandas as pd
from sklearn import tree

input_file = "c:/spark/DataScience/PastHires.csv"
df = pd.read_csv(input_file, header = 0) 

```

任何命令行输入或输出都将按以下方式书写：

```py
spark-submit SparkKMeans.py  

```

新术语和重要单词以粗体显示。例如，屏幕上显示的单词，例如菜单或对话框中的单词，会以这种方式出现在文本中：“在 Windows 10 上，您需要打开“开始”菜单，然后转到“Windows 系统”|“控制面板”以打开“控制面板”。”

警告或重要提示会显示为这样。

提示和技巧会显示为这样。
