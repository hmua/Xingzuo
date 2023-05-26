

<script>
	a=document.currentScript.parentNode
	a.insertAdjacentHTML('beforeEnd', '<input />')
	b=a.lastChild
	
	function greet(e) {
		a.insertAdjacentHTML('beforeEnd',e.target.value)
		console.log(e.target.value)
	}

	a.oninput = greet;
</script>
