

测试输入：
{::nomarkdown}
<script>
	a=document.currentScript.parentNode
	a.insertAdjacentHTML('beforeEnd', '<input />')
	a.lastChild.oninput=(e)=>{
		a.insertAdjacentHTML('beforeEnd',e.target.value)
		console.log(e.target.value)
	}
</script>
{:/}
