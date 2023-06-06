简记，依次做了以下设置（不确定哪步可能不是必要的）
1. fork [d90a835 - May 22, 2023 @jeffreytse](https://github.com/jeffreytse/jekyll-deploy-action/commit/d90a835c3b0d80402bd8f7a8c7cf694bb75c05dd)
1. 修改`.github/workflows/deploy-test.yml`，24行最后一行加上`branch: 'gh-pages'`
1. Settings→Pages，Source选“Deploy from a branch”、Branch选“gh-pages”
1. Settings→Actions→General最下面两项，
	“Allow GitHub Actions to create and approve pull requests”、
	“Workflow permissions”选“Read and write permissions”
1. 修改“test_site/about.markdown”，随便加些文字。

查看Actions中，会先产生一条“Update about.markdown”，
完成后再产生一条“pages build and deployment pages”，
是先触发了Jekyll后触发了gh-pages。
之后就能看到生效。

通过写一个测试页确认，Jekyll版本从本来的<4.0升级到了≥4.1。
但站点的生成时间也大概延长了一倍，
如何取舍还要再考虑。
