鼠标事件的bug

```bash
1.在使用鼠标事件的时候，我们不能只能监听同一个容器的鼠标抬起事件，这样会产生bug，当我鼠标移出这个容器在抬起，就会产生bug，不触发事件。
```

![image-20231017213517839](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231017213517839.png)

```bash
1.我们应该把鼠标抬起事件加给window，并且是在鼠标按下以后才监听鼠标抬起事件。
2.事件源e应该沿用外层的，保持事件源一致。
```

![image-20231017213802587](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231017213802587.png)



键盘事件的bug

键盘事件不能通过防抖解决

原始代码

![image-20231017214129167](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231017214129167.png)

怎么修改:我们通过一个数组，保存已经按下的按键，然后在键盘抬起的时候删除掉该按键即可

![image-20231017214349180](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231017214349180.png)

实例

```js
 // 存放已经按下的数组
        const codeIn = new Set()
        window.onkeydown = function(e){
            const code = e.key
            // 如果code存在且code不是数组中有的
            if(code && !codeIn.has(code)){
                console.log('鼠标按下了',code)
                // 添加进数组
                codeIn.add(code)
            }
        }

        window.onkeyup = function(e){
            const code = e.key
            if (code) {
                console.log('鼠标抬起删除code', code);
                // 鼠标抬起 删除
                codeIn.delete(code)
            }
        }
        console.log('我是数组',codeIn)
```

