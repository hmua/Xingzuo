“_config.yml”中的设置，从[文档](https://jekyllrb.com/docs/configuration/markdown)看来还有更多的设置，
边尝试边记录。
```
markdown: kramdown
markdown: GFM
```

## 关于默认设置的问题
文档写默认就是GFM，
但实际默认没有Autolinking，声明后才支持，
因此判断实际默认是kramdown。

## 自动链接
GFM支持Autolinking。

## 斜体粗体BUG
这是GFM的BUG，在GitHub在线编辑器、预览中能方便地查看，
正常情况：
`中文*中文斜体*`
>中文*中文斜体*

当斜体部分需要以中文“全角括号”开头时，斜体失效：
`中文*（GFM中斜体失效*`
>中文*（GFM中斜体失效*

英文也是同样：
`abc*(def*`
>abc*(def*

可见这是一个“英文单词以空格间隔”为前提的严谨设定，
英文中括号前面应该有空格，
当只考虑英文时，这应该是个严谨的设定；
但这个设定被照搬至中文括号，是错误的。

### 解决
- 当设定“markdown: kramdown”时可以避免这个GFM的BUG；
- 如果使用GFM也可以通过直接写HTML，非常方便地解决：
  `中文<em>中文斜体</em>`
  >中文<em>中文斜体</em>

## 表格
对表格格式也有一点影响。
设为kramdown时最简练
`kramedown|GFM`
kramedown|GFM
GFM则稍啰嗦
头两行必须至少有如下内容
表头也不能省略
```
|||
-|-
kramedown|GFM
```
|||
-|-
kramedown|GFM
