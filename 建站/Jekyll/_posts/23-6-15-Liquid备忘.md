

### escape
行内代码和代码块的情况完全一致
```liquid
&lcub;%assign abc='abc'|slice:1%}
&#123;%assign abc='abc'|slice:1%}
{{'{'}}%assign abc='abc'|slice:1%}✓
\{%assign abc='abc'|slice:1%}
{\%assign abc='abc'|slice:1%}

&lcub;{'abc'|slice:1}}
&#123;{'abc'|slice:1}}
{{'{'}}{'abc'|slice:1}}✓
\{{'abc'|slice:1}}
{\{'abc'|slice:1}}
```

正文段落和blockquote则情况完全一致，比代码块多几种可用写法
>&lcub;%assign abc='abc'|slice:1%}
>&#123;%assign abc='abc'|slice:1%}✓
>{{'{'}}%assign abc='abc'|slice:1%}✓
>\{%assign abc='abc'|slice:1%}
>{\%assign abc='abc'|slice:1%}
>
>&lcub;{'abc'|slice:1}}
>&#123;{'abc'|slice:1}}✓
>{{'{'}}{'abc'|slice:1}}✓
>\{{'abc'|slice:1}}
>{\{'abc'|slice:1}}✓

其实正文、片段引用中不必带起止括号，去掉起止括号就简洁多了。
奇怪的还有，第二部分的引号都被“smart quote”识别转换了，
第一部分却全都没有。
猜测可能引号前面有等号就不会转换？这方面暂不必要进一步确认了。

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

从文档看，有部分filter是同时支持string和array的，
如array下的`size`也支持string，
>Returns the size of a string or array.（[文档](https://shopify.dev/docs/api/liquid/filters/size)）

string下的`slice`则也支持array
>Returns a substring or series of array items, starting at a given 0-based index.（[文档](https://shopify.dev/docs/api/liquid/filters/slice)）

但并不是所有filter都通用，或者也不是想当然的都通用。
经过测试，`'abc'|first`没有输出，`'bac'|sort`会导致Jekyll build失败。
（[Jekyll文档]中，sort有特别处理，区别于原本的Liquid filter。）

[Jekyll文档]:https://jekyllrb.com/docs/liquid/filters

array的filters支持“dot notation”，string的则不支持。
文档也是这样写的没错，但为什么会有这种差异，似乎并没逻辑，
也没有讲解讨论。

#### 扩展一组

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

#### slice
{{'abc'|slice:1}}

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
