```vue
<template>
	<div class="container">
		<div class="area">{{ selectedName }}</div>
		<button class="btn-primary" @click="toggleRunning">
			<!-- 按钮的文本根据 isRunning 的值来确定，如果正在运行，则显示 "结束"，否则显示 "开始"。 -->
			{{ isRunning ? '结束' : '开始' }}
		</button>
	</div>
</template>

<script setup>
	import {
		ref
	} from 'vue';

	let timer = null; // 定时器
	// 数组
	const names = [
		'李一',
		'屈二',
		'谢三',
		'张四'
	];
	// 开局显示第一组
	const selectedName = ref(names[0]);
	// 是否运行
	const isRunning = ref(false);
	
    // 代码逻辑
	// 点击开始时进入else 此时页面开始滚动名字 开始替换为结束
	// 此时点击结束 执行if的代码 清除定时器 选择一个随机名字展示并将其在数组删除 结束替换为开始
	const toggleRunning = () => {
		// 运行时 -> isRunning.value = true
		if (isRunning.value) {
			clearInterval(timer);
			// 随机选一个数来展示
			let randomIndex = Math.floor(Math.random() * names.length);
			selectedName.value = names[randomIndex];
			names.splice(randomIndex, 1); // 从数组中删除已经被点名的人
			if (names.length === 0) {
				names.push('李一',
					'屈二',
					'谢三',
					'张四')
			}
		} else {
			// 非运行时 -> isRunning.value = false
			// 第一次点击的时候是未运行状态  开启定时器
			timer = setInterval(() => {
				let randomIndex = Math.floor(Math.random() * names.length);
				selectedName.value = names[randomIndex];
			}, 100);
		}
		// 切换状态
		isRunning.value = !isRunning.value;
	}
</script>

<style>
	.area {
		text-align: center;
		font-size: 20px;
		width: 150rpx;
		height: 150px;
		line-height: 150px;
		background-color: antiquewhite;
		margin: 0 auto;
	}
</style>
```

