# Data Visualization of Titanic Dataset in d3.js & dimple
## 1.概要:
>The sinking of the RMS Titanic is one of the most infamous shipwrecks in history.  On April 15, 1912, during her maiden voyage, the Titanic sank after colliding with an iceberg, killing 1502 out of 2224 passengers and crew. This sensational tragedy shocked the international community and led to better safety regulations for ships.One of the reasons that the shipwreck led to such loss of life was that there were not enough lifeboats for the passengers and crew. Although there was some element of luck involved in surviving the sinking, some groups of people were more likely to survive than others, such as women, children, and the upper-class.


> 泰坦尼克号数据集记录了乘客们的个人信息以及存活信息，这个项目我将利用d3.js和dimple以及相关知识完成泰坦尼克号数据集的可视化，通过分析相关变量，去展示存活者与其最关键特征的关系。

## 2.设计：
> 首先了解了泰坦尼克号的大背景，推测存活者将集中在女士和小孩中，但小孩只占总人数的小部分，所以我并没有想到一个好的可视化方法，于是就将重心放在另一个变量——船舱等级上，所以这次可视化分析了不同船舱，不同性别的存活人数比较。
> 设计决策：此次图表选择了饼状矩阵(pie matrix)图，x轴变量是船舱等级从高到低（头等舱，二等舱，三等舱），y轴变量为性别的categorical变量（男士和女士），每一个饼状表达了相同舱位相同性别的存活（survived）／死亡（perished）对比，存活／死亡对应的颜色为红／蓝，如第一行第一列的饼状图表现了头等舱全体男士中，存活／死亡对比为43%与57%，将鼠标悬浮在饼状图中的passengerId所表现的数据即为人数和其百分比。

## 3.反馈：
> 1.盲目地去寻求好看或者复杂的数据可视化，忽略了思考最有可能的关系，好的数据可视化是简单直接而不是复杂晦涩。<br>
> 2.(优达学城第一次提交反馈）请对可视化初始的设计决策进行说明。比如：选择的图表类型是什么，x,y轴和颜色分别代表什么，使用了哪些图例，可视化动画和互动的层次是什么？

## 4.资源
[项目中可视化主要的饼状图dimple模版](http://dimplejs.org/examples_viewer.html?id=pie_matrix) <br>
[Creating an Animated Ring or Pie chart in d3js](http://javascript.tutorialhorizon.com/2015/03/05/creating-an-animated-ring-or-pie-chart-in-d3js/)<br>
[Hover over a segment to see a custom tooltip](http://dimplejs.org/adhoc_viewer.html?id=adhoc_bar_custom_tooltips)<br>
