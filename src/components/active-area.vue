<template>
	<div>
		<div id="D-out">
			<sa v-for="(sa,index) in sas" :key="index"></sa>
		</div>
	</div>
</template>

<script>
	import sa from './small-area.vue'
	export default {
		name: 'D-out',
		components: {
			sa,
		},
		data() {
			return {
				sas: []

			}
		},
		mounted() {
			var i = 0;
			var sh; /* 初始蛇头位置 */
			var sh1; /* 初始食物位置 */
			while (i < 400) {
				this.sas.push("<sa class=\"sa\"/>");
				i++;
			}


			setTimeout(() => {

				sh = Math.round(Math.random() * 400);

				var ds = document.getElementsByClassName("d1");
				/* 绘制蛇头，给蛇头添加class */
				ds[sh].className = ds[sh].className + " cred";
				/* 避免蛇头与食物重叠 */
				sh1 = Math.round(Math.random() * 400);
				while(sh===sh1){
					sh1 = Math.round(Math.random() * 400)
				};
				/* 给食物添加样式 */
				ds[sh1].className = ds[sh1].className + " cgreen";

			}, 1000)


		},


	}
</script>

<style>
	#D-out {
		width: 440px;
		height: 440px;
		border: 2px solid white;
		background-color: green;

	}

	.sa {
		float: left;
		display: inline-block;
	}
</style>
