kramdown对表格的支持非常有限，
尝试用一些非常简易的方式改善……

这|是|一个|小|表格
_这里可以有个通栏……吗？_|
{:.t1}

<style>
.t1 tr:nth-of-type(2) td { border: 0 }
.t1 tr:nth-of-type(2) td:first-child { position: absolute }
</style>

这|是|一个|小|表格
_那可以有右侧对齐的通栏吗？_|
{:.t2}

<style>
.t2 tr:nth-of-type(2) { position: relative }
.t2 tr:nth-of-type(2) td { border: 0 }
.t2 tr:nth-of-type(2) td:first-child{
    position: absolute;
	text-align: right;
    width: 100%;
    box-sizing: border-box;
}
</style>

#### 保留，测试用的
这|是|一个|小|表格
_这里可以有个通栏……吗？_|
这|是|表格|的|另一行
{:.t3}
<style>
	.t1 tr:nth-of-type(2) td{color:red}
</style>
