在GhP（GitHub Pages）、Jekyll模板中，注释有几种标记语法。
1. Liquid：`{%raw%}{% comment %} ... ... {% endcomment %}{%endraw%}`
2. Liquid行内：`{%raw%}{% # ... ... %}{%endraw%}`
3. kramdown：`{::comment} ... ... {:/}`
4. GFM：`[//]: <> ( ... ... )`
5. XML：`<!-- ... ... -->`

注意：并不是每种都可以，实际每种情况不同。
- Liquid语法是最啰嗦的，啰嗦到不像注释，但也是最可靠的，一定会有效；
- Liquid行内语法最简练，
本应是最优选，但需要Liquid 5.4，GhP目前4.0.4不支持；
- kramdown语法会生成一个XML注释，保留到HTML结果中；
- GFM……测试无效，好像是必须前面有空行，
这是一种hack写法，GFM本身设计用XML语法，
毕竟GFM本身不是为写模板设计的；
- kramdown和GFM语法互相不支持；
- XML语法会保留到HTML结果中，虽然不会显示出来……但这不符合本来目的。

##### 测试
1. Liquid：`{% comment %} ... ... {% endcomment %}`（注释成功）
2. Liquid行内：无法测试，会导致Jekyll生成失败
3. kramdown：“{::comment} ... {:/}”（使用kramdown时注释成功，使用GFM则失败）
	- `{::comment} ... {:/}`（但不能用在code节中）
5. GFM：`[//]: <> ( ... ... )`（失败）
6. XML：<!-- ... ... -->（不会显示，但存在于HTML源代码中），
`<!-- ... ... -->`（在code中则会显示）

## Escape
```liquid{%raw%}
{{'{{'}}'abcde'}}{%endraw%}
```
>{{'{{'}}'abcde'}}
{{'abcde'}}
