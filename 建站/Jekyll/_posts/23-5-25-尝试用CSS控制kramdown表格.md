kramdown对表格的支持非常有限，
尝试用一些非常简易的方式改善……

## 尝试

这|是|一个|表格|演示的
_这里可以有个通栏……吗？_|{:.t1}
<style>
.t1 tr:nth-of-type(2) td { border: 0 }
.t1 tr:nth-of-type(2) td:first-child { position: absolute }
</style>

这|是|一个|表格|演示的
_那可以有右对齐通栏吗？_|
{:.t2}
<style>
.t2 tr:nth-of-type(2) td { border: 0 }
.t2 tr:nth-of-type(2) { position: relative }
.t2 tr:nth-of-type(2) td:first-child{
    position: absolute;
	text-align: right;
    width: 100%;
    box-sizing: border-box;
}
</style>

这|是|一个|表格|演示的
*可以合并吗？*|||*合并啦！*
这|是|表格|的|另一行
{:.t3}
<style>
.t3 tr:nth-of-type(2) td { border: 0 }
.t3 tr:nth-of-type(2) td:is(:first-child,:nth-child(4)){
	position:absolute;
	border-left:initial
}
</style>

## 细看kramdown生成表格
```
这|是一个|表格|表格|表表格
*行尾缺省的格会自动补全*|
这|是|表格|的|另一行
```
