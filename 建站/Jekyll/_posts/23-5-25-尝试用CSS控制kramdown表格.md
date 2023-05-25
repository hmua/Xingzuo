kramdown对表格的支持非常有限，
尝试用一些非常简易的方式改善……

这|是|一个|小|表格
_这里可以有个通栏……吗？_|

<style>
:last-child tr:nth-of-type(2) td { border: 0 }
:last-child tr:nth-of-type(2) td:first-child { position: absolute }
</style>

这|是|一个|小|表格
_可以有右对齐的通栏……吗？_|
<style>
:last-child tr:nth-of-type(2) td{
	text-align: right;
	width: 100%;
	box-sizing: border-box;
}
</style>

#### 保留，测试用的
这|是|一个|小|表格
_这里可以有个通栏……吗？_|
这|是|表格|的|另一行
{:.t1}
<style>
	.t1 tr:nth-of-type(2) td{color:red}
</style>
