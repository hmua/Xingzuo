

### escape
行内代码和代码块的情况完全一致
```liquid
&lcub;%assign abcde='ab,c,def'|split:','%}
&#123;%assign abcde='ab,c,def'|split:','%}
{{'{'}}%assign abcde='ab,c,def'|split:','%}✓
\{%assign abcde='ab,c,def'|split:','%}
{\%assign abcde='ab,c,def'|split:','%}

&lcub;{abcde}}
&#123;{abcde}}
{{'{'}}{abcde}}✓
\{{abcde}}
{\{abcde}}
```

正文段落和blockquote则情况完全一致，比代码块多几种可用写法
>&lcub;%assign abcde='ab,c,def'|split:','%}
>&#123;%assign abcde='ab,c,def'|split:','%}✓
>{{'{'}}%assign abcde='ab,c,def'|split:','%}✓
>\{%assign abcde='ab,c,def'|split:','%}
>{\%assign abcde='ab,c,def'|split:','%}
>
>&lcub;{abcde}}
>&#123;{abcde}}✓
>{{'{'}}{abcde}}✓
>\{{abcde}}
>{\{abcde}}✓

### Handles、Filters
和JS中“函数”对应的概念，
在Liquid中是“handle”和“filter”，这样命名符合“模板语言”。

#### Handle

#### Filter

#### 数字
`round`、`abs`等数字操作只支持`|`一种写法

`5|round`|`5.round`|`5[round]`|`5['round']`|`5["round"]`
{{5|round}}|{{5.round}}×|{{5[round]}}×|{{5['round']}}×|{{5["round"]}}×

`assign a=5.5`{%assign a=5.5%}

`a|round`|`a.round`|`a[round]`|`a['round']`|`a["round"]`
{{a|round}}|{{a.round}}×|{{a[round]}}×|{{a['round']}}×|{{a["round"]}}×

#### 文本
`assign a='abc'`{%assign a='abc'%}

`a|upcase`|`a.upcase`|`a[upcase]`|`a['upcase']`|`a["upcase"]`
{{a|upcase}}|{{a.upcase}}×|{{a[upcase]}}×|{{a['upcase']}}×|{{a["upcase"]}}×

#### size

`size`则可以`|`、`.`两种写法

{%assign abc='abcde'-%}
`assign abc='abcde'`

`abc|size`|`abc.size`|`abc[size]`|`abc['size']`|`abc["size"]`
{{abc|size}}|{{abc.size}}|{{abc[size]}}×|{{abc['size']}}×|{{abc["size"]}}×

{%assign abc='abc,de,fg'|split:','-%}
`assign abc='abc,de,fg'|split:','`

`abc|size`|`abc.size`|`abc[size]`|`abc['size']`|`abc["size"]`
{{abc|size}}|{{abc.size}}|{{abc[size]}}×|{{abc['size']}}×|{{abc["size"]}}×

*不知道是否有人能看懂，我是真看不懂。*
`size`可以用`.`，`upcase`不可以，
只知道唯一线索是，size应该是array的，参考[文档](https://shopify.dev/docs/api/liquid/filters/size)

>Returns the size of a string or array.

从文档看出`size`对string的支持是特别的，
array的其他filter经过测试，`'abc'|first`没有输出，
`'bcdae'|sort`会导致Jekyll build失败。

扩展一组

`abc.[size]`|`abc.['size']`|`abc.["size"]`
{{abc.[size]}}×|{{abc.['size']}}×|{{abc.["size"]}}×

匿名值，和数字一样，只支持`|`一种写法

`'abc'|size`|`'abc'.size`|`'abc'[size]`|`'abc'['size']`|`'abc'["size"]`
{{'abc'|size}}|{{'abc'.size}}×|{{'abc'[size]}}×|{{'abc'['size']}}×|{{'abc'["size"]}}×

#### join

`abcdefg|join:','`{:.liquid}{{abcdefg|join:','`}}✓|`abcdefg.join:','`{{abcdefg.join:','}}×

#### concat
{%assign abc='abc,de,fg,hijk,lmn'|split:','%}
{%assign abc=abc|concat:abc%}
{{abc|join:','}}

#### first
{{'abc'|first}}*无效*

### map
{%assign abc='abc,de,fg,hijk,lmn'|split:','%}
{{abc|map:'size'|join:'、'}}
{{site.pages|map:'path'|join:'、'}}

{%assign n='1.3,1.4,1.5,1.6'|split:','%}
{{n}}|{{n.first}}|{{n.first.ceil}}|{{n.first|ceil}}
{{n|map:'ceil'}}

{{n}}|{{n.first}}|{{n.first.floor}}|{{n.first|floor}}
{{n|map:'floor'}}

### if/unless

`if a.categories|size<=1`×|`if a.categories.size<=1`✓
`if a.slug|contains:'：'`×|`if a.slug contains'：'`✓

#### contains
- `if 'abcde' contains 'e'`{%if 'abcde' contains 'e'%}t{%else%}f{%endif%}
- `if 'abcde' contains 'f'`{%if 'abcde' contains 'f'%}t{%else%}f{%endif%}

`assign abcde='abcde'`{%assign abcde='abcde'%}
- `if abcde contains'e'`{%if abcde contains'e'%}t{%else%}f{%endif%}
- `if abcde contains'f'`{%if abcde contains'f'%}t{%else%}f{%endif%}

以下全部是错误语法，会产生错误结果，但不会报错
- `if abcde.contains'e'`{%if abcde.contains'e'%}t{%else%}f{%endif%}
- `if abcde.contains'f'`{%if abcde.contains'f'%}t{%else%}f{%endif%}
- `if abcde|contains'e'`{%if abcde|contains'e'%}t{%else%}f{%endif%}
- `if abcde|contains'f'`{%if abcde|contains'f'%}t{%else%}f{%endif%}
- `if abcde|contains:'e'`{%if abcde|contains:'e'%}t{%else%}f{%endif%}
- `if abcde|contains:'f'`{%if abcde|contains:'f'%}t{%else%}f{%endif%}
