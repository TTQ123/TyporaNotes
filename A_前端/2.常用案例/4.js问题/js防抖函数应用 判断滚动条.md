```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>监听dom元素滚动条.html</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            display: grid;
            place-items: center;
            min-height: 100vh;
        }
        div[class^="content"] {
            padding: 20px;
            background: #10ac84;
            color: #fff;
            height: calc(100vh - 0px);
            width: 100vw;
            overflow: auto;
        }
        section {
            height: 200px;
        }
    </style>
</head>
<body>
    <div class="content">
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
        <section>如何监听元素滚动条</section>
   </div>
   <script>
        const content = document.querySelector('.content')
        content.onscroll = Debounce(watchCallBack, 500)

        // 回调函数
        function watchCallBack () {
            // scrollHeight 实际内容高度，包括溢出导致的视图中不可见内容。
            const contentHeight = content.scrollHeight
            // 可见高度 height
            const { left, top, height, width } = content.getBoundingClientRect()
            // 滚动高度，滚动条可以滚动的高度
            const scrollH = content.scrollTop
            if(contentHeight - height - scrollH <= 110) { //当滚动到距离底部100px时,
                console.log(contentHeight, scrollH, height);
            }
        }
       
	    //防抖函数的原理是在一定时间内，如果事件持续触发，则重新计时；如果事件停止触发，等待一段时间后才执行事件处理函数。
        // 防抖函数(参数1:回调函数,参数2:执行时间)
        function Debounce (debounce, timeDelay) {
            let timer = null
            return function () {
                if (timer) clearTimeout(timer) //如果当前事件正在执行时 清除定时器  
                timer = setTimeout(debounce, timeDelay) //如果当前事件结束  触发定时
            }
        }
   </script>
</body>
</html>
```

