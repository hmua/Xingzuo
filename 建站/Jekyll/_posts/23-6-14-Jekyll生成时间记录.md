*只是积累生成时间记录，以便之后总结经验*

从`{{'{'}}{site.categories|join:','}}`{:.liquid}
改`{{'{'}}{site.categories|map:'name'|join:','}}`{:.liquid}
时间从1m40s缩减到50s。

`site.posts.size`
`site.posts|map:'slug'`
`site.posts|map:'slug'|join:'、'`
: 没有明显增加时间
