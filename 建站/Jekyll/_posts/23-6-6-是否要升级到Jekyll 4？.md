升级到Jekyll 4，即使用Actions部署GitHub Pages。

#### 优点
1. 可以使用插件：复杂表格、Mermaid图表等，但目前来看这些完全不需要。
1. Jekyll 4有些新语法，像“find”是不太必要，
但“binary operators in where_exp”就对原本啰嗦的语法改进很多。
考虑到准备加入分类方面的功能，一定会很有帮助。

#### 缺点
1. 使用Actions好像、大约令生成时间延长一倍，
但可能是错觉，可能可以优化。
3. 从到目前的经验来看，Jekyll的完成质量有限，
升级操作不知道会带来多少坑。

#### 以及
1. 所幸是，
Actions的启用关闭，在尝试过程中反复多次操作，看来完全没问题，
启用、关闭都很顺畅，用了4，再回到3.9，至少设置上不麻烦。
2. Jekyll 4已经很多年了，gh-pages新的Actions支持4，classic仍限定3.9，
可能是将gh-pages定向到喜欢自己动手的小伙伴们，
也可能出于对现有大量站点的兼容性考虑。
3. 不马上升级，应该马上要着手加入分类方面的功能，到时看情况。
一是文章要分星座和建站、生活板块，
二是文学类、应用类文章在排版上要分开。

##### 注，重要备注
这里说的“使用GitHub Actions”不等于在Settings里选择“GitHub Actions”，
*Settings中用语指代不明，以后应该会改进。*

简单、初步地说，
使用Actions分两种情况：“一个action完成”，和“分两个actions完成”，
（这里所说的“一个action”都是指一个脚本：.yml文件）。
我测试使用的@JefferyTse的action就是分两步的情况中的第一步，
该action只完成第一步：Jekyll生成站点，
第二步再由gh-pages本来的基本功能“Deploy from a branch”部署这个站点。

如果在Settings中选择“GitHub Actions（Beta）”，
则会生成一个的action（.yml文件）并启用，该一个action中包括两步。

即，第一种是两个actions分别Jekyll和gh-pages；
第二种是一个action，Jekyll和gh-pages一起。

这个混淆也源自本身“Deploy from a branch”也是一个action，
和选择“GitHub Actions”的区别是不会有脚本文件，但也会有Actions记录，
如果不升级Jekyll版本、不扩展plugin的话，则完全不需关心。
