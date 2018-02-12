# Work Doc

1. 向我们总结此项目的目标以及机器学习对于实现此目标有何帮助。作为答案的部分，提供一些数据集背景信息以及这些信息如何用于回答项目问题。你在获得数据时它们是否包含任何异常值，你是如何进行处理的？【相关标准项：“数据探索”，“异常值调查”】

> 项目概述：安然曾是 2000 年美国最大的公司之一。2002 年，由于其存在大量的企业欺诈行为，这个昔日的大集团土崩瓦解。 在随后联邦进行的调查过程中，大量有代表性的保密信息进入了公众的视线，包括成千上万涉及高管的邮件和详细的财务数据。 你将在此项目中扮演侦探，运用你的新技能，根据安然丑闻中公开的财务和邮件数据来构建相关人士识别符。 为了协助你进行侦查工作，我们已将数据与手动整理出来的欺诈案涉案人员列表进行了合并， 这意味着被起诉的人员要么达成和解，要么向政府签署认罪协议，再或者出庭作证以获得免受起诉的豁免权。

> 机器学习："我们将给予你可读入数据的初始代码，将你选择的特征放入 numpy 数组中，该数组是大多数 sklearn 函数假定的输入表单。 你要做的就是设计特征，选择并调整算法，用以测试和评估识别符。 我们在设计数个迷你项目之初就想到了这个最终的项目，因此请记得借助你已完成的工作成果。"

> 数据集背景：在【数据集与问题】这一课第二个视频我们得知了len(enron_data)-->146个数据点，第三个视频中得知嫌疑人数量为18个，非嫌疑人数量为128个，特征数量为20个，其中财务特征有14个，财务特征: \['salary', 'deferral_payments', 'total_payments', 'loan_advances', 'bonus', 'restricted_stock_deferred', 'deferred_income', 'total_stock_value', 'expenses', 'exercised_stock_options', 'other', 'long_term_incentive', 'restricted_stock', 'director_fees'] (单位均是美元）,邮件特征: \['to_messages', 'email_address', 'from_poi_to_this_person', 'from_messages', 'from_this_person_to_poi', 'shared_receipt_with_poi'] (单位通常是电子邮件的数量，明显的例外是 ‘email_address’，这是一个字符串）

> 异常值：在第【异常值】这一课最后一个视频中我们得知特征“TOTAL”并非一个具体的特征值，而是一个总和，所以要使用data_dict.pop('TOTAL',0)删除掉这个特征值。视频学习中还提到了两个“异常值”，LAY KENNETH L和SKILLING JEFFREY K，但根据背景了解得知他们是公司高管，也是最大的嫌疑人，故他们并不是异常值，不删除。


2. 你最终在你的 POI 标识符中使用了什么特征，你使用了什么筛选过程来挑选它们？你是否需要进行任何缩放？为什么？作为任务的一部分，你应该尝试设计自己的特征，而非使用数据集中现成的——解释你尝试创建的特征及其基本原理。（你不一定要在最后的分析中使用它，而只设计并测试它）。在你的特征选择步骤，如果你使用了算法（如决策树），请也给出所使用特征的特征重要性；如果你使用了自动特征选择函数（如 SelectBest），请报告特征得分及你所选的参数值的原因。【相关标准项：“创建新特征”、“适当缩放特征”、“智能选择功能”】

> 适当缩放特征 & 创建新特征：通过`from_this_person_to_poi/from_messages`和`from_poi_to_this_person/to_messages`进行特征缩放，形成新的特征

> 智能选择功能：利用`sklearn.feature_selection`中`SelectKBest`自动特征选择函数去筛选得分高于2.0的特征。得到`features_list`


3. 你最终使用了什么算法？你还尝试了其他什么算法？不同算法之间的模型性能有何差异？【相关标准项：“选择算法”】
> 我最终使用了SVM算法，我尝试了NB，DT，和Adaboost算法，

我最终使用了支持向量机分类器算法。我还尝试了“朴素贝叶斯”，“决策树”和“基于决策树的AdaBoost”算法。我是以f1分数作为算法性能的评估标准的，其中支持向量机分类算法得分为0.496；其次是朴素贝叶斯分类器，得分为0.331；AdaBoost和决策树算法性能分别为0.26和0.235。

4. 调整算法的参数是什么意思，如果你不这样做会发生什么？你是如何调整特定算法的参数的？（一些算法没有需要调整的参数 – 如果你选择的算法是这种情况，指明并简要解释对于你最终未选择的模型或需要参数调整的不同模型，例如决策树分类器，你会怎么做）。【相关标准项：“调整算法”】
> 在【支持向量机（SVM）】课程学习的最后一课中我学习到了调整算法的参数是指面对不同的问题与条件选择不同的分类器（算法）和参数（使得算法performance更好），如果不调参，会引发过拟合或者分类能力差等影响。

> 在【支持向量机（SVM）】课程中我还学习到了手动调参任务量大，我利用了Pipeline（《python机器学习》第6章）使得我们可以先拟合出包含任意多个处理步骤的模型（特征缩放，PCA，和不同机器学习模型的不同参数值组合）并将模型用于新数据的预测（GridSearchCV，网格搜索，通过对我们指定的不同超参列表进行暴力穷举搜索，并计算评估每个组合对模型性能对影响，自动查找最优参数调整的sklearn工具）


5. 什么是验证，未正确执行情况下的典型错误是什么？你是如何验证你的分析的？【相关标准项：“验证策略”】
> 验证： 我认为，验证既是评估机器学习模型在新数据集上性能的方法,将数据2


> 验证分析： 第四题有所回答，在调整算法对时候用到了`GridSearchCV`,

验证是指将数据分为训练集和测试集两个部分，通过训练集拟合模型，然后用测试集验证算法的性能。如果没有正确执行验证，那么得到的算法模型可能是过拟合的——对未知情况适应性非常差。

我通过三个度量指标来对每个分类器算法性能进行评估：f1分数，精确度和召回率。我首先将待评估的算法分别用GridSearchCV进行封装，然后迭代地对每个分类器算法进行拟合（GridSearchCV会自动执行交叉验证过程），然后我通过estimate_classifier()函数对拟合过后的分类器计算f1分数，最后选择f1分数最高的“最优参数+最优算法模型”作为最终的clf。

estimate_classifier()函数的原理：首先通过StratifiedShuffleSplit算法将数据分为若干训练集和测试集。StratifiedShuffleSplit算法通过打乱顺序然后分为多个分层的容器来将数据分为测试集和训练集，每个容器中的数据集目标类别（label）比例是按照完整数据集的类别比例进行分配的。然后我对得到的若干训练集+测试集数据用分类器进行拟合，调用sklearn.metrics.f1_score计算得到一个f1分数，最后汇总多次计算的f1分数平均值作为性能评估标准。

6. 给出至少 2 个评估度量并说明每个的平均性能。解释对用简单的语言表明算法性能的度量的解读。【相关标准项：“评估度量的使用”】

> 使用tester.py评估性能时，我得知了性能最好的分类器为SVM，其中最优参数为 `C=1.0`,`class_weigh='balanced'`, `kernel='sigmoid'`，`gamma=0.10000000000000001`

> 性能指标中（python机器学习6.5）

对我所选择的支持向量机分类器而言，最优参数为C=1.0，class_weight='balanced'，kernel='sigmoid'和gamma=0.10000000000000001，PCA的n_components参数为4。
精确度0.331，即被标记为POI的人中有33.1%为真正的POI；召回率0.862，即所有为POI的人中有86.2%被正确的标记。

Reference
[关于F1_score](http://blog.csdn.net/simplelovecs/article/details/50520602)

《PYTHON机器学习》，第六章 模型评估与参数调优实战