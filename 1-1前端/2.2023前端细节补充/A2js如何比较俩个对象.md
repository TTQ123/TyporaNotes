## 1.js对比俩个对象是否相等

### 1.严谨比较

#### 1.封装函数

```js
// 检查俩个对象是否完全相等
        function isEquivalent(obj1, obj2){
            // 1.如果两个对象是相同的引用，则它们相等，返回 true
            if (obj1 === obj2) {
                return true
            }

            // 2.检查两个对象是否都是对象类型
            if(typeof obj1 !== 'object' || obj1 === null || typeof obj2 !== 'object' || obj2 === null){
                // 如果两个对象不是对象类型或者其中一个为 null，它们不相等，返回 false
                return false
            }

            // 3.检查两个对象的属性数量是否相同
            const keys1 = Object.keys(obj1);
            const keys2 = Object.keys(obj2);
            if (keys1.length !== keys2.length) {
                // 如果两个对象的属性数量不同，它们不相等，返回 false
                return false;
            }

            // 4.遍历对象的属性并比较它们的值和类型 
            for(const key of keys1){
                // 如果key2的值在key1中不存在 或者 俩者的值不相等(调用自己封装的函数来判断)
                // obj1[key]  obj2[key]取出来的是值
                // 要传key的原因是判断俩个对象在key相等时值相不相等
                if(!keys2.includes(key) || !isEquivalent(obj1[key], obj2[key])){
                    return false;  
                }
            }

            // 5.所有情况都检查了 返回true
            return true
        }


    let obj1 = {  
        key1: "value1",  
        key2: "value2",  
        key3: "value3",  
    };
    let obj2 = {  
        key1: "value",  
        key2: "value2",  
        key3: "value3",  
    };

    // obj1 和 obj2 的键名相同，值不同  
    console.log(isEquivalent(obj1, obj2)); // 输出：false  
```

#### 2.调用三方库

![image-20230926120225333](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230926120225333.png)



### 2.不严谨比较

#### 1.JSON.stringify()

![image-20230926120254426](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230926120254426.png)

#### 2.遍历对象

![image-20230926120327110](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230926120327110.png)





## 2.在 JavaScript 中，您可以使用以下方法来获取对象中的值：

1. 使用点表示法：

```js
let obj = {  
  key: "value"  
};

let value = obj.key;  
```

2. 使用方括号表示法：

```js
let obj = {  
  key: "value"  
};

let value = obj["key"];  
```

3. 使用`Object.keys()`方法获取对象的键数组，然后遍历键数组来获取值：

```js
let obj = {  
  key1: "value1",  
  key2: "value2"  
};

let keys = Object.keys(obj);

for (let key of keys) {  
  console.log(key + ": " + obj[key]);  
}
```

4. 使用`for...in`循环遍历对象的属性：

```js
let obj = {  
  key1: "value1",  
  key2: "value2"  
};

for (let key in obj) {  
  console.log(key + ": " + obj[key]);  
}
```

5. 使用`Object.entries()`方法将对象转换为键值对数组，然后遍历数组来获取值：

```js
let obj = {  
  key1: "value1",  
  key2: "value2"  
};

for (let [key, value] of Object.entries(obj)) {  
  console.log(key + ": " + value);  
}
```