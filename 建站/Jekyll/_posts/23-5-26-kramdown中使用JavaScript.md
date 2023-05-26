

{::nomarkdown}
测试输入：<script>
	let a=document.currentScript.parentNode
	a.insertAdjacentHTML('beforeEnd','<input />')
	a.lastChild.oninput=(e)=>{
		a.insertAdjacentHTML('beforeEnd','\n'+e.target.value)
	}
</script>
{:/}
