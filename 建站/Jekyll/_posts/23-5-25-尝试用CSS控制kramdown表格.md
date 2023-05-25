kramdown对表格的支持非常有限，
尝试用一些非常简易的方式改善……

<div markdown='1'>
	
这|是|一个|小|表格
_这里可以有个通栏……吗？_|
这|是|表格|的|另一行

<style scoped>
:scope tr:nth-of-type(2) td { border: 0 }
:scope tr:nth-of-type(2) td:first-child { position: absolute }
</style>

</div>
<div markdown='1'>
	
这|是|一个|小|表格
_那可以有右侧对齐的通栏吗？_|
这|是|表格|的|另一行

<style scoped>
:scope tr:nth-of-type(2) td{
	text-align: right;
	width: 100%;
	box-sizing: border-box;
}
</style>
</div>

#### 保留，测试用的

这|是|一个|小|表格
_这里可以有个通栏……吗？_|
这|是|表格|的|另一行
{:.t1}
<style>
	.t1 tr:nth-of-type(2) td{color:red}
</style>
