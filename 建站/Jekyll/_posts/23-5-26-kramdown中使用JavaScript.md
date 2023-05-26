

测试输入：{::nomarkdown}<script>
	let a=document.currentScript.parentNode
	a.insertAdjacentHTML('beforeEnd','<input />')
	a.lastChild.oninput=()=>{
		a.insertAdjacentHTML('beforeEnd','\n'+a.lastChild.text)
	}
</script>{:/}
