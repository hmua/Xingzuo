*只是积累生成时间记录，以便之后总结经验*

从`{{'{'}}{site.categories|join:','}}`{:.liquid}
改`{{'{'}}{site.categories|map:'name'|join:','}}`{:.liquid}
时间从1m40s缩减到50s。

`site.posts.size`
`site.posts|map:'slug'`
`site.posts|map:'slug'|join:'、'`
: 没有明显增加时间

这段时间做了很多通过[jeffreytse/jekyll-deploy-action](https://github.com/jeffreytse/jekyll-deploy-action)升级到Jekyll 4的测试，
时间会从50s升到1m50s，可以接受，并且应该可以优化。
