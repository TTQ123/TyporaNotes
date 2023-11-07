```js
    <script>
        /*
         * 如何优化if-else分支结构
        */
        function speak(name) {
            // 利用map结构
            const mapArray = [
                [
                    () => name.includes('牛'), () => console.log('我是牛') //第一项表示条件,第二项表示条件成立执行的函数
                ],
                [
                    () => name.length <= 3 && name.endsWith('虎'), () => console.log('我是虎')
                ]
            ];
            //会分别执行每个小数组的第一个函数,条件成立返回true(带着对应的那一个小数组)
            const target = mapArray.find(m => m[0]()) //通过find寻找数组的所有第一项 满足返回那一个对应的数组(里面有俩项)
            

            if (target) {
                target[1]() //执行条件成立的函数
            }else{
                console.log('没有满足条件的情况');
            }   
            // console.log(mapArray[1][1]);
        }

        speak('虎')
        
    </script>
```

```js
/*
         * 如何优化if-else分支结构
        */

        function calculate(action, num1, num2) {
            const actions = {
                add: (a, b) => a + b,
                subtract: (a, b) => a - b,
                multiply: (a, b) => a * b,
                divide: (a, b) => a / b,
            }
           
            // hasOwnProperty检查是否是对象的自有属性
            // 检查 actions 对象是否包含传入的操作符 action  
            if (actions.hasOwnProperty(action)) {
                // 如果 actions 对象包含传入的操作符，则返回对应的函数执行结果  
                return actions[action](num1, num2); //actions[action]会找到对应的属性
            } else {
                // 如果 actions 对象不包含传入的操作符，则抛出错误  
                throw new Error(`Invalid action: ${action}`);
            }
        }

        console.log(calculate('add',5,3));
```

