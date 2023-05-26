

测试输入：
<script>
	a=document.currentScript.parentNode
	a.insertAdjacentHTML('beforeEnd', '<input />')
	b=a.lastChild
	a.oninput=(e)=>{
		a.insertAdjacentHTML('beforeEnd',e.target.value)
		console.log(e.target.value)
	}
</script>
