

测试输入：
{::-nomarkdown-}
<script>
	a=document.currentScript.parentNode
	a.insertAdjacentHTML('beforeEnd','<input />')
	a.lastChild.oninput=()=>{
		a.insertAdjacentHTML('beforeEnd','\n'+a.value)
		console.log(e.target.value)
	}
</script>
{:/}
