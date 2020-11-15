<template>
	<div>
		<input type="text" readonly="readonly"  id="num1">
		<button id="start" @click="start">开始游戏</button>
		<button @click="actives">{{active}}游戏</button>
		<button @click="again">重新开始</button>
	</div>
</template>

<script>
	var m; /* 蛇头位置 */
	var n = 0; /* 蛇的长度 */
	var timer; /* 定时器 */
	var code = 4; /* 上一次的 keycode   1,2,3,4=>上下左右*/
	var sh1 /* 食物 */
	var alldiv = document.getElementsByClassName("d1")

	function goTop(longs) {
		
		clearInterval(timer);
		//console.log(e.keyCode)
		timer = setInterval(() => {

			if (m-20 < 0) {
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0)
			}

			if (alldiv[m - 20].className.indexOf('cgreen') !== -1) {
				longs.unshift(alldiv[m - 20])
				n = n + 1;
				document.getElementById("num1").value=document.getElementById("num1").value*1+100;
				/* 随机生成食物 */
				do {
					sh1 = Math.round(Math.random() * 400);
				} while (alldiv[sh1].className.indexOf('cred') !== -1)
				/* 给食物添加样式 */
				alldiv[sh1].className = "d1 cgreen";
			}else if(alldiv[m - 20].className.indexOf('cred') !== -1){
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0)
			}else {
				// 否则将他加入数组，但要除去最后一个方块样式，并删除它
				longs.unshift(alldiv[m - 20]);
				longs[n + 1].className = "d1";
				longs.pop();
			}
			// 所有蛇的身体方块都要染成红色
			for (var i in longs) {
				longs[i].className = "d1 cred";
			}
			m = m - 20;
			console.log(m)
			code=1;
		}, 300)
	}

	function goDown(longs) {
		
		clearInterval(timer);
		timer = setInterval(() => {

			if (m >= 379) {
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0)
			}

			if (alldiv[m + 20].className.indexOf('cgreen') !== -1) {
				longs.unshift(alldiv[m + 20])
				n = n + 1;
				document.getElementById("num1").value=document.getElementById("num1").value*1+100;

				/* 随机生成食物 */
				do {
					sh1 = Math.round(Math.random() * 400);
				} while (alldiv[sh1].className.indexOf('cred') !== -1)
				/* 给食物添加样式 */
				alldiv[sh1].className = "d1 cgreen";


			}else if(alldiv[m + 20].className.indexOf('cred') !== -1){
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0)
			}else {
				// 否则将他加入数组，但要除去最后一个方块样式，并删除它
				longs.unshift(alldiv[m + 20]);
				longs[n + 1].className = "d1";
				longs.pop();
			}
			// 所有蛇的身体方块都要染成红色
			for (var i in longs) {
				longs[i].className = "d1 cred";
			}
			m = m + 20;
			code=2;
		}, 300)
	}

	function goLeft(longs) {
		
		clearInterval(timer);
		timer = setInterval(() => {
			if(m-1<0){
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0) /* 刷新页面，重置游戏 */
			}
			if (alldiv[m - 1].className.indexOf('cgreen') !== -1) {
				longs.unshift(alldiv[m - 1])
				n = n + 1;
				document.getElementById("num1").value=document.getElementById("num1").value*1+100;

				/* 随机生成食物 */
				do {
					sh1 = Math.round(Math.random() * 400);
				} while (alldiv[sh1].className.indexOf('cred') !== -1)
				/* 给食物添加样式 */
				alldiv[sh1].className = "d1 cgreen";


			}else if(alldiv[m - 1].className.indexOf('cred') !== -1){
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0)
			} else {
				// 否则将他加入数组，但要除去最后一个方块样式，并删除它
				longs.unshift(alldiv[m - 1]);
				longs[n + 1].className = "d1";
				longs.pop();
			}
			if (m % 20 == 0) {
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0) /* 刷新页面，重置游戏 */
			}
			
			// 所有蛇的身体方块都要染成红色
			for (var i in longs) {
				longs[i].className = "d1 cred";
			}
			m = m - 1;
		}, 300)
		code=3;
	}

	function goRight(longs) {
		
		clearInterval(timer);
		timer = setInterval(() => {
			// 如果下一个方块是绿色的，被蛇吃掉，将他加入数组，且不删除蛇身最后一个方块
			if(m+1>399){
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0) /* 刷新页面，重置游戏 */
			}
			if (alldiv[m + 1].className.indexOf('cgreen') !== -1) {
				longs.unshift(alldiv[m + 1])
				n = n + 1;
				m = m + 1;
				document.getElementById("num1").value=document.getElementById("num1").value*1+100;
				/* 随机生成食物 */
				do {
					sh1 = Math.round(Math.random() * 400);
				} while (alldiv[sh1].className.indexOf('cred') !== -1)
				/* 给食物添加样式 */
				alldiv[sh1].className = "d1 cgreen";

			/* 饥不择食把自己咬死了 */
			}else if(alldiv[m + 1].className.indexOf('cred') !== -1){
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0) /* 刷新页面，重置游戏 */
			}else {
				// 否则将他加入数组，但要删除蛇身最后一个方块
				longs.unshift(alldiv[m + 1]);
				longs[n + 1].className = "d1";
				longs.pop();
				m = m + 1;
			}
			// 所有蛇的身体方块都要染成红色
			for (var i in longs) {
				longs[i].className = "d1 cred";
			}
			// 碰壁  判定蛇被撞死了
			if (m % 20 == 0) {
				clearInterval(timer)
				alert('游戏失败，再接再厉！')
				window.history.go(0) /* 刷新页面，重置游戏 */
			}
			
		}, 300)
		code=4
		
		
	}

	export default {
		data() {
			return {
				fs: 0,
				longs: [],
				active: "暂停"
			}
		},
		
		methods: {
			again() {
				window.history.go(0)
			},
			actives(){
				if (this.active == '暂停') {
					this.active = "继续"
					clearInterval(timer)
				} else {
					this.active = "暂停"
					this.start()
				}
			},
			start() {
				
				//element.className.indexOf('rgb196') !== -1
				/* 寻找初始蛇头所在位置 */
				
				if(this.longs.length===0){
					for (var i = 0; i < alldiv.length; i++) {
						if (alldiv[i].className.indexOf('cred') !== -1) {
							m = i;
							break;
						}
					}
					//将蛇头加入数组longs  
					this.longs.unshift(alldiv[m]);
				}
				


				if (code === 1) {
					goTop(this.longs)
				} else if (code === 2) {
					goDown(this.longs)
				} else if (code === 3) {
					goLeft(this.longs)
				} else if (code === 4) {
					goRight(this.longs)
				}

				/* 根据按下的键来决定蛇如何移动 */
				document.onkeydown = () => {
					if (event.keyCode === 87 || event.keyCode === 38) { /* 向上移动   W  和  向上箭头 */
						if (code === 2) {
							return 0;
						} else {
							goTop(this.longs)
						}



					} else if (event.keyCode === 83 || event.keyCode === 40) { /* 向下移动 */

						if (code === 1) {
							return 0;
						} else {
							goDown(this.longs)
						}


					} else if (event.keyCode === 65 || event.keyCode === 37) { /* 向左移动 */
						if (code === 4) {
							return 0
						} else {
							goLeft(this.longs)
						}


					} else if (event.keyCode === 68 || event.keyCode === 39) { /* 向右移动 */
						if (code === 3) {
							return 0
						} else {
						goRight(this.longs)
						}

					}
				}

			}


		}
	}
</script>

<style>
	input {
		width: 150px;
		height: 20px;
		padding: 5px;
		font-size: 18px;
		color: #008000;
		margin-left: 15px;
		margin-top: 50px;
		outline: none;
	}

	button {
		width: 100px;
		height: 50px;
		font-size: 20px;
		font-weight: bold;
		margin-top: 30px;
		margin-left: 50px;
		color: black;
	}
</style>
