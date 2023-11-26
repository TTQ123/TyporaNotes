**业务场景:我们需要打开俩个标签页,当一个标签页修改了以后，另一个标签页实时更新它更新的内容**

**我们可以利用storage事件来实现，但是要在相同域中才能实现,例如127.0.0.1和127.0.0.1/news**



`A页面  发送消息`

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<script>
		// 接收消息
		function sendMsg(type, payload) {
			localStorage.setItem(
				// 键名 --> key
				'__' + type,
				JSON.stringify({
					// 消息 --> newValue
					payload,
					// 避免消息冲突
					temp: Date.now()
				})
			)
		}
	
		setTimeout(()=>{
			sendMsg('add-temp', {
				msg: '消息1'
			})
		},3000)
	</script>
</body>
</html>
```

`B页面  监听消息`

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<div class="box">我是监听页面</div>
	<script>
		// 监听消息
		function listenMsg (handler) {
			// 监听事件触发时的函数
			const storageHandler = e => {
				const data = JSON.parse(e.newValue)
				handler(e.key.substring(2), data.payload)
			}
			window.addEventListener('storage', storageHandler)
			return () => {
                  // 返回的函数用来取消监听,减少开销
				window.removeEventListener('storage', storageHandler)
			}
		}

		let box = document.querySelector('.box')

		// 开始监听
		let msg = listenMsg((type, payload) => {
			if (type !== null) {
                 // 更新文本
				box.innerText = type
			}
			// 移出监听(在组件中我们就在卸载组件时移除监听,这里直接移除，节约系统开支)
			msg()
		})
	</script>
</body>
</html>
```



**正常在前端工程项目中，我们要封装成一个函数，这里只是演示效果**

`封装`

```js
// 发送消息
export function sendMsg(type, payload) {
	localStorage.setItem(
		// 键名 --> key
		'__' + type,
		JSON.stringify({
			// 消息 --> newValue
			payload,
			// 避免消息冲突,连续点击就会出现payload一样设置不了消息(可以使用uuid更合适)
			temp: Date.now()
		})
	)
}

// 监听消息
export function listenMsg (handler) {
	// 监听事件触发时的函数
	const storageHandler = e => {
		const data = JSON.parse(e.newValue)
		handler(e.key.subString(2), data.payload)
	}
	window.addEventListener('storage', storageHandler)
	return () => {
		window.removeEventListener('storage', storageHandler)
	}
}
```

