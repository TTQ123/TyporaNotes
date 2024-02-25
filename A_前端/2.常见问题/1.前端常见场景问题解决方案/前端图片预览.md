1.传统的图片预览流程

![image-20240131022625008](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131022625008.png)



2.简化以后的流程

![image-20240131022720204](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131022720204.png)

通过dataurl来实现

![image-20240131022800293](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131022800293.png)

![image-20240131022959993](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131022959993.png)

## 1.具体实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DataURL</title>
</head>
<body>
    <!-- url是统一资源定位符 -->
    <input type="file"/>
    <img src="" id="preview"/>
    <script>
        const input = document.querySelector('input');
        const img = document.querySelector('#preview');
        console.log(input);
        input.onchange = () => {
            //取出文件信息
            const file = input.files[0];
            // 创建文件读取器
            const reader = new FileReader();
            // 将文件读取为DataURL格式 异步I/O操作
            reader.readAsDataURL(file);
            // 等待读取完成后会触发这个onload事件
            reader.onload = (e) => {
                img.src = e.target.result;
            }
        }
    </script>

    <!-- 可以动态的设置js代码  点击某一个按钮以后加上这段代码 -->
    <script src="data:application/javascript,alert(2323)"></script>
</body>
</html>
```



## 2.通过URL.CreateURL

![image-20240131023558038](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131023558038.png)

![image-20240131023610020](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131023610020.png)

具体代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <input type="file" id="input"/>
    <img src="" id="img">
    <script>
      const input = document.getElementById('input');
      input.addEventListener('change', e => {
        // 获取图片或视频数据
        const blob = input.files[0];
        // 创建一个URL对象，设置img的src属性为URL对象
        img.src = URL.createObjectURL(blob);
      })
    </script>
</body>
</html>
```

