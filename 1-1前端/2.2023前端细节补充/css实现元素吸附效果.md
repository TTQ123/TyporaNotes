



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 吸附效果默认谁占的大吸附到哪 */
        .content{
            display: flex;
            width: 100vw;
            overflow-x: scroll;
            /* 添加x轴吸附效果 */
            scroll-snap-type: x mandatory;
        }
        .content::-webkit-scrollbar{
            /* 隐藏滚动条 */
            width: 0;
        }
        .box1{
            width: 100%;
            height: 200px;
            background-color: aqua;
        }
        .box2{
            width: 100%;
            height: 200px;
            background-color: yellow;
        }
        .box3{
            width: 100%;
            height: 200px;
            background-color: red;
        }
        .item{
            display: flex;
            flex-shrink: 0;
            /* 吸附开始 */
            scroll-snap-align: start;
            scroll-snap-stop: always;
        }
    </style>
</head>
<body>
    <div class="content">
        <div class="box1 item"></div>
        <div class="box2 item"></div>
        <div class="box3 item"></div>
    </div>
</body>
</html>
```

