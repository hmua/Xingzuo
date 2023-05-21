*_config.yml*中的设置，从[文档](https://jekyllrb.com/docs/configuration/markdown)看来还有更多的设置，
边尝试边记录。
```
markdown: kramdown
markdown: GFM
```

## 关于默认设置的问题
文档写默认就是GFM，
但实际默认没有Autolinking，声明后才支持，
因此实际默认应该是kramdown。

## 自动链接
GFM支持Autolinking。

## 表格
对表格格式也有一点影响。
设为*kramdown*时最简练
```
kramedown|GFM
```
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
