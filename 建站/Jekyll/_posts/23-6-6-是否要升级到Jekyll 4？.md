升级到Jekyll 4，即使用GitHub Actions。

#### 优点
1. 可以使用plugin、复杂表格、Mermaid等，
目前来看在这方面需求不强，可有可无。
1. Jekyll 4有些新语法，像“find”是不太必要，
但“binary operators in where_exp”就对原本啰嗦的语法改进很多。
考虑到准备加入分类方面的功能，一定会很有帮助。

#### 缺点
1. 使用Actions好像、大约令生成时间延长一倍。
2. 从到目前的经验来看，Jekyll的完成质量有限，升级后不知道有多少坑。

所幸是，Actions的启用关闭，在尝试过程中反复多次操作，看来完全没问题，
启用、关闭都很顺畅，用了4，再回到3.9，至少设置上不麻烦。

##### 注，重要备注
这里说的“使用GitHub Actions”不等于在Settings里选择“GitHub Actions”，
*Settings中用语指代不明，以后应该会改进。*

简单、初步地说，
使用Actions分两种情况：“一个action完成”，和“分两个actions完成”。
我测试使用的@JefferyTse的action就是分两步的情况中的第一步，
该action只完成第一步：Jekyll生成站点，
第二步再由gh-pages本来的基本功能“Deploy from a branch”部署这个站点。

如果在Settings中选择“GitHub Actions（Beta）”，则会生成一个的action并启用，
该action中则包括两步。

即，第一种是两个action分别Jekyll和gh-pages；
第二种是一个action，Jekyll和gh-pages一起。
