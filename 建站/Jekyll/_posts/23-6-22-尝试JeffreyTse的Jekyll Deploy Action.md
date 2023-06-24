简记，依次做了以下设置（不确定哪步可能不是必要的）
1. fork [d90a835 - May 22, 2023 @jeffreytse](https://github.com/jeffreytse/jekyll-deploy-action/commit/d90a835c3b0d80402bd8f7a8c7cf694bb75c05dd)
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

###### 2023年6月19日
## 二刷遇到的问题
theme不正常，分两种情况，查看生成的HTML源码
1. head中没有style：在front matter或`_config.yml`中加入`layout: page`
3. head中有style但路径是`jekyll-deploy-action`：在`_config.yml`中修改`baseurl`

#### 在`_config.yml`中设置layout
```yaml
defaults:
  -
    scope:
      path: ""
    values:
      layout: page
  -
    scope:
      path: "index.md"
    values:
      layout: home
```

#### 以及
1. md文件需要front matter，猜测可以在配置中加`include` md文件，
   或者找gh-pages的配置文件参考
3. 需要index.md

###### 2023年6月22日
## 三刷
1. 创建新项目，带`README.md`
2. 开Action两个权限
3. 建action
	```yaml
	name: Tests
	on:
	  push:
	    branches:
	      - main
	jobs:
	  github-pages:
	    runs-on: ubuntu-latest
	    steps:
	    - uses: actions/checkout@v3
	    - uses: actions/cache@v3
	      with:
	        path: vendor/bundle
	        key: ${{'{'}}{ runner.os }}-gems-${{'{'}}{ secrets.CACHE_VERSION }}-${{'{'}}{ hashFiles('**/Gemfile.lock') }}
	        restore-keys: |
	          ${{'{'}}{ runner.os }}-gems-
	    - uses: jeffreytse/jekyll-deploy-action@v0.4.0
	      with:
	        provider: 'github'
	        token: ${{'{'}}{ secrets.GITHUB_TOKEN }}
	        jekyll_src: './'
	```
build失败，无可用信息。
4. `_config.yml`：`baseurl: "/tjda4"`，build失败，无可用信息。
试了一下gh-pages classic，可以生成。
5. Gemfile（内容略），Jekyll build通过，gh-pages classic通过但没内容。
6. 添加[Jekyll Readme Index]，成功生成首页。

[Jekyll Readme Index]:https://github.com/benbalter/jekyll-readme-index

*已经完成，添加版本探针。进一步配置theme见二刷*

#### 确认action权限
1. 关闭*Allow GitHub Actions to create and approve pull requests*，可build✓
2. 关闭*Read and write permissions*，不能更新`gh-pages`branch了×

#### 其它
1. 将config`baseurl: "/tjda4"`移至action`jekyll_baseurl: '/tjda4'`

#### 尚留问题
1. gh-pages内建action可以不用`Gemfile`

###### 2023年6月24日
## 启用theme
1. 添加[Jekyll Remote Theme](https://github.com/benbalter/jekyll-remote-theme)，build失败
2. 从“Jeffrey Tse's Personal Blog”找到[可用的Gemfile]，build通过，
应该是theme使用到“jekyll-seo-tag”插件需要在Gemfile中声明。

[可用的Gemfile]:https://github.com/jeffreytse/jekyll-jeffreytse-blog/blob/master/Gemfile
