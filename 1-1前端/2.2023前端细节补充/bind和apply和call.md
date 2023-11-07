```js
<script>
        function fun(){
            console.log(this) // 输出window
            console.log(this.name)
        }
        let cat = {name: '喵喵'}

        // 此时我可以通过call 让cat 和 fun建立联系
        // fun.call(cat) // 输出 喵喵

        // 更复杂的场景下
        let dog = {
            name: '狗狗',
            sayName(){
                console.log(this.name)
            },
            food(food){
                console.log(this)
                console.log('我喜欢'+ food);
            }
        }

        // dog.sayName() //输出狗狗

        // 我希望猫可以调用狗的方法,可以通过call 第一个参数代表this,后面的参数就是狗狗函数中需要的参数
        // 1.call的传参是用逗号隔开的，并且会立即执行函数。
        dog.food.call(cat, '鱼肉')  // 指向猫 -- 输出我喜欢鱼肉

        // 2.apply传参是用数组传参，并且会立即执行函数
        dog.food.apply(cat, ['鱼肉']) // 指向猫 -- 输出我喜欢鱼肉

        // 3.bind传参是用逗号隔开，并且不会立即调用函数，它会返回一个函数，便于我们多次调用。
        const returnFn = dog.food.bind(cat, '鱼肉')
        returnFn() // 指向猫 -- 输出我喜欢鱼肉
</script>
```

