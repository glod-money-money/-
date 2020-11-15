<template>
	<div id="A-out">
	<aa id='aa'/>
	<cf id="cf"/>
	
	
	</div>
</template>

<script>
	import cf from './components/control-panel.vue'
	import aa from './components/active-area.vue'
	
	export default {
		name:'A-out',
		components:{			
			aa,
			cf,
		}
	}
</script>

<style>
	#A-out{
		width: 640px;
		height: 444px;
		background-color: darkgray;
		border: 1px solid green;
		margin: 50px auto;
		position: relative;
	}
	#aa{
		width: auto;
	}
	#cf{
		width: 194px;
		height: 440px;
		margin-top: 0px;
		position: absolute;
		right: 0;
		top: 0;
		border: 2px solid white;
	}
</style>
