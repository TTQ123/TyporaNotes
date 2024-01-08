**js提升渠道**

[JavaScript半知半解 · 看云 (kancloud.cn)](https://www.kancloud.cn/dennis/tgjavascript)



FileAPI的使用 扩展了可拖拽效果

场景:图片的获取

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FileAPI</title>
</head>

<body>
    <!-- 文件输入框，支持多选 -->
    <!-- multiple表示可以多选文件 dragenter表示可以拖拽 -->
    <input type="file" id="fileInput" multiple dragenter>
    <!-- 图片预览区域 -->
    <div id="preview"></div>

    <script>
        // 获取文件输入框和图片预览区域的 DOM 元素
        const fileInput = document.getElementById('fileInput');
        const preview = document.getElementById('preview');

        // 监听文件输入框的 change 事件
        fileInput.addEventListener('change', function () {
            // 清空图片预览区域
            preview.innerHTML = '';

            // 遍历用户选择的每一个文件
            for (let i = 0; i < fileInput.files.length; i++) {
                const file = fileInput.files[i];

                // 如果用户选择了文件
                if (file) {
                    // 创建一个 FileReader 对象
                    const reader = new FileReader();

                    // reader.onload 是 FileReader 对象的一个事件处理程序属性，它在读取操作完成时触发。
                    // 当 FileReader 完成文件读取时，会触发 load 事件，并调用 onload 回调函数。
                    // 在这个回调函数中，你可以访问文件的数据，例如 Data URL 或 ArrayBuffer。
                    reader.onload = function (e) {
                        // 读取创建一个图片元素
                        const img = document.createElement('img');
                        // e.target.result 是 FileReader 对象读取文件后的结果。
                        // 对于图片文件，这个结果通常是一个 Data URL，它包含了文件的内容以及文件类型等信息。
                        console.log(e.target.result)
                        // 设置图片的 src 属性为文件的 Data URL
                        img.src = e.target.result;
                        // 将图片添加到图片预览区域
                        preview.appendChild(img);
                    };

                    // 以 Data URL 格式读取文件(图片的读取模式)
                    reader.readAsDataURL(file);
                }
            }
        })
    </script>
</body>

</html>
```

