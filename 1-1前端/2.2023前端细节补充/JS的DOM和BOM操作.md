# 1.DOM操作及定时器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM操作及Timer</title>

    <style>
        .add{
            width: 100px;
            height: 100px;
            background-color: aqua;
        }
    </style>
</head>
<body>
    <div class="box" id="box">
        <div class="box-child">1</div>
        <p class="p">2</p>
    </div>
    <script>
        let a = document.querySelector('.box-child') //根据选择器获取匹配到的第一个元素
        let b = document.querySelectorAll('.box-child') //根据选择器获取匹配到的所有元素
        let c = document.getElementById('box') //根据id名称获取元素
        let d = document.getElementsByClassName('p') //根据类名获取元素
        let e = document.getElementsByTagName('div') //根据标签名获取元素

        let f = a.parentNode // 根据子元素获取父元素
        let g = f.childNodes  // 根据父元素获取子元素(包括空白)
        let h = f.children  // 根据父元素获取子元素(不包括空白)
        // a.parentNode.removeChild(a) // 移除子节点

        // 设置样式
        a.style.color = 'red'
        // 添加类名
        a.className = 'add'

        // 文本处理
        // a.innerHTML = 'abc' // 添加文本
        // a.innerHTML = '<p>2</p>' //可以添加标签
        a.textContent = 'adv'  // 只能添加文本
        

        // 事件处理
        // 这种方式会前面的事件覆盖后面的事件
        a.onclick = function(){
            alert(1)
        }

        // 这种方式不会产生事件覆盖
        a.addEventListener('click',() => {
            console.log(1);
        })

        // timer
        // 这种定时器会一直重复执行 但是会容易阻塞 一般不用 用setTimeout模拟
        // let timer = setInterval(()=>{
        //     console.log(123);
        // },3000)
        // clearInterval(timer) // 关闭定时器

        let timer = setTimeout(function auto () {
            clearTimeout(timer) // 每一次开始前关闭上一次定时器
            console.log(123)
            timer = setTimeout(auto, 3000) // 上一次回调结束时再次调用 这样可以确保时间永远一样
        }, 3000)
    </script>
</body>
</html>
```



轮播图案例

```html
<!DOCTYPE html>
<html>
<head>
	<title>1</title>
	<style type="text/css">
		*{
			margin: 0;
			padding: 0;
		}

		.box{
			width: 100px;
			height: 100px;
			position: relative;
			list-style: none;
		}

		.box li{
			opacity: 0;
		}

		.box li:nth-child(1){
			width: 100px;
			line-height: 100px;
			background-color: red;
			position: absolute;
			text-align: center;
		}
		.box li:nth-child(2){
			width: 100px;
			line-height: 100px;
			background-color: yellow;
			position: absolute;
			text-align: center;
		}
		.box li:nth-child(3){
			width: 100px;
			line-height: 100px;
			background-color: tomato;
			position: absolute;
			text-align: center;
		}
		.box li:nth-child(4){
			width: 100px;
			line-height: 100px;
			background-color: pink;
			position: absolute;
			text-align: center;
		}
		.box li:nth-child(5){
			width: 100px;
			line-height: 100px;
			background-color: blue;
			position: absolute;
			text-align: center;
		}
		
		.box li.active{
			opacity: 1;
		}
	</style>
</head>
<body>
	<ul class="box">
		<li class="active">1</li>
		<li>2</li>
		<li>3</li>
		<li>4</li>
		<li>5</li>
	</ul>
	<button class="prev">上一张</button>
	<button class="next">下一张</button>

	<script type="text/javascript">
		let father = document.querySelector('.box')
		let childs = father.children
		// console.log(childs)
		let prevBtn = document.querySelector('.prev')
		let nextBtn = document.querySelector('.next')
		// console.log(prevBtn,nextBtn)


		let index = 0
		prevBtn.addEventListener('click',function () {
			clearTimeout(timer)
			childs[index].className = ''
			if (index === 0) {
				index = childs.length
			}
			index--
			childs[index].className = 'active'
		})

		function nextFn () {
			childs[index].className = ''
			if (index === childs.length-1) {
				index = -1
			}
			index++
			childs[index].className = 'active'
		}


        let timer
         function open(){
            timer = setTimeout(function auto(){
                clearTimeout(timer)
				nextFn()
				timer = setTimeout(auto,1500)
            },1500)
         }
		open()

        // 鼠标移入暂停
        father.addEventListener('mouseenter', function(){
            clearTimeout(timer)
           
        })

        // 鼠标移出开始
        father.addEventListener('mouseleave', function(){
            clearTimeout(timer)
            open()
        });

        // 点击时切换下一张
        nextBtn.addEventListener('click',function () {
			// clearTimeout(timer)
			nextFn()
		})
        // 鼠标移入暂停
        nextBtn.addEventListener('mouseenter', function(){
            clearTimeout(timer)
        })

        // 鼠标移出开始
        nextBtn.addEventListener('mouseleave', function(){
            clearTimeout(timer)
            open()
        });
	</script>
</body>
</html>
```

