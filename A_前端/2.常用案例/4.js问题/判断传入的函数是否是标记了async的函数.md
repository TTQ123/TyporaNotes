这种方法是一种常见的检测数据类型的方式，通过调用对象的 `toString` 方法来获取其类型信息。在 JavaScript 中，每个对象都有一个 `toString` 方法，当你调用 `toString` 方法时，它会返回一个表示对象的类型的字符串。

在这种方法中，`Object.prototype.toString.call([])` 的作用是调用 `Object` 原型上的 `toString` 方法，并将 `this` 指向 `[]`（即一个空数组），这样就可以获取到 `[]` 的类型信息。

下面是一个示例：

```js
console.log(Object.prototype.toString.call([])); // 输出: [object Array]
console.log(Object.prototype.toString.call({})); // 输出: [object Object]
console.log(Object.prototype.toString.call("hello")); // 输出: [object String]
console.log(Object.prototype.toString.call(123)); // 输出: [object Number]
```

通过这种方法，你可以得到对象的类型信息，然后通过字符串的形式来判断对象的具体类型。这种方法在一些情况下可以用于更精确地判断对象的类型，特别是在处理一些特殊的对象类型时。



![image-20231121143552315](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121143552315.png)



因为标记了async的函数的原型上设置了一个知名符号

![image-20231121144804067](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121144804067.png)

所以解决方式

![image-20231121143617642](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121143617642.png)