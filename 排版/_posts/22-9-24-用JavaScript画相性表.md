# 用JAVASCRIPT

<script>
var a=[..."羊牛双蟹狮处秤蝎射摩瓶鱼"]
var a=[...Array(12).keys()]
document.getElementById("用JAVASCRIPT".toLowerCase())
.insertAdjacentHTML('afterend',a)
</script>

## 转成图文
羊|牛|双|蟹|狮|
{{ page.xz | inspect }}
{{ page["星座"]["白羊"] | inspect }}
{{ page.xz["白羊"] | inspect }}
{{ page.xz["巨蟹"] | inspect }}
{{ page.xz["巨蟹"][1] | inspect }}