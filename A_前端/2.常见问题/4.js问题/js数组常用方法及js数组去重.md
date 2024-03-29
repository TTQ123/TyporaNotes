# 1.数组常用方法

## 1.filter 过滤删除用

```js
//将数组中符合条件的元素保存到一个新数组中返回
//参数1:当前元素值 参数2:当前元素索引 参数3:当前元素属于的数组对象(self就是arr)
        function del(id) {
            const arr = [
                { id: 1, name: '跑步一公里' },
                { id: 2, name: '跳绳一百次' },
                { id: 3, name: '跳远十次' }
            ]
            let newArr = []
            newArr = arr.filter(item => item.id !== id)  //删除传入的id对应的项
            console.log(newArr);  
        }
        del(1)
```

## 2.reduce 求和用

![image-20230821021556560](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230821021556560.png)

```js
    //可以用来将一个数组中的所有元素整合为一个值    
 function sum() {
            const arr = [
                { id: 1, price:30 },
                { id: 2, price:30 },
                { id: 3, price:30 }
            ]
            let newArr = []
            newArr = arr.reduce((total,cur) => {
                return total + cur.price
            },0)  
            console.log(newArr);  
        }
        sum()
```

## 3.map 数组需要特殊处理

1.数据提取

```js
        function changeObj() {//根据当前数组生成一个新数组
            const arr = [
                { id: 1, price: 30 },
                { id: 2, price: 30 },
                { id: 3, price: 30 }
            ]
            let newArr = []
            newArr = arr.map((item) =>  item.id, 0)
            console.log(newArr);
        }
        changeObj()
```

2.数据转换

```js
        function changeObj() {
            const arr = [1,2,3,4,5]
            let newArr = []
            newArr = arr.map((item) => item * 2, 0)
            console.log(newArr);
        }
        changeObj()
```

![image-20230821022543101](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230821022543101.png)

## 4.slice 截取数组或者浅复制数组

![image-20230821022905315](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230821022905315.png)

## 5.find 查找数组

```js
        function changeObj(id) {
            const arr = [{id:1},{id:2}]
            let newArr = []
            newArr = arr.find((item) => item.id === id, 0) //查找id一致的
            console.log(newArr);
        }
        changeObj(1)
```

## 6.splice 删除替换插入数组中的元素

![image-20230821023323022](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230821023323022.png)

```js
        function changeObj() {
            const arr = [1,2,3,4,5,6,7]
            arr.splice(arr.length,0,8,9)
            console.log(arr); //[1, 2, 3, 4, 5, 6, 7, 8,9]
        }
        changeObj()
```

## 7.reverse 反转数组

## 8.foreach

![image-20230821024104955](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230821024104955.png)

```js
        function changeObj() {
            const arr = [1,2,3,4,5,6,7]
            arr.forEach((element,index) => console.log(arr[index]));
        }
        changeObj()
```

# 2.数组去重

## 1.set

```java
const arr = [1, 2, 3, 3, 4, 4, 5];
const uniqueArr = [...new Set(arr)]; //set会保存唯一的值,创建set即只保留123456 将其转为数组即可
console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

## 2.filter

```js
const arr = [1, 2, 3, 3, 4, 4, 5];
const uniqueArr = arr.filter((value, index, self) => { //参数1:当前元素值 参数2:当前元素索引 参数3:当前元素属于的数组对象(self就是arr)
   return self.indexOf(value) === index; //遍历数组时检查当前元素在数组中的第一个索引位置，如果与当前索引位置相同(表示是第一次出现的该元素值)，则保留该元素
   });
console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

## 3.reduce

```js
const arr = [1, 2, 3, 3, 4, 4, 5];
const uniqueArr = arr.reduce((prev, crr) => { //prev累加值 crr当前元素 传一个空数组作为累加起始
      // includes() 方法用于判断字符串是否包含指定的子字符串。
      return prev.includes(crr) ? prev : [...prev, crr]; //如果累加值包含当前项则返回,不包含当前值则添加到数组中
    }, []);
console.log(uniqueArr); // [1, 2, 3, 4, 5]
```

## 4.for+includes

```js
        const arr = [1, 2, 3, 3, 4, 4, 5];
        const newArr = []
        for(let i = 0; i<arr.length; i++){
            if (!newArr.includes(arr[i])) {
                newArr.push(arr[i])
            }
        }
        console.log(newArr);
```

## 5.for+indexOf

```js
        const arr = [1, 2, 3, 3, 4, 4, 5];
        const newArr = []
        for(let i = 0; i<arr.length; i++){
            if (arr.indexOf(arr[i]) === i) { //如果第一次出现的元素等于i 证明当前元素是第一次出现在arr数组中
                newArr.push(arr[i])
            }
        }
        console.log(newArr);
```

## 6.第三方库

```js
//使用时要安装load库
let list = ['你是最棒的1', 8, 8, 1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 1, 2, 3, 4, 5, 6, 7, 8, '你是最棒的1',]
let result = _.uniq(list);//_.uniq(list)会返回一个新的数组，其中只包含了原始数组中的唯一元素。
```

## 7.使用对象对象去重

```js
        let list = [8, 8, 1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 1, 2, 3, 4, 5, 6, 7, 8]
        let result = {};
        list.forEach(item => {
            result[item] = "sss"; //将数组中的元素作为键，赋值为"sss"作为值，将其添加到result对象中(对象中的键是唯一的，这样可以实现去重操作)
        })
        // Object.keys()方法获取键的数组，然后使用map()方法对数组进行操作
        result = Object.keys(result).map(item => Number(item)); //获取对象的建并转为number数组
        console.log(result);
```

# 27种常用的数组方法

[27个重要的JavaScript数组函数整理汇总 (qq.com)](https://mp.weixin.qq.com/s?__biz=MjM5MDA2MTI1MA==&mid=2649118986&idx=1&sn=a20751891391d24879e145357ac205a0&chksm=be587ea7892ff7b10d3f169b6032bfdb79a7186570489943083fdd033d2ec133a70d4f64d5aa&scene=27)



```bash
1.concat() 方法用于合并两个或多个数组。

2.every()。该方法测试输入数组中的所有元素是否都通过了实现的条件。它返回一个布尔值。
const arr1 = [89, 0, -4, 34, -1, 10];
const arr2 = [89, 0, 45, 34, 1, 100];
arr1.every(arrItem => arrItem >= 0);
// false
arr2.every(arrItem => arrItem >= 0);
// true

3.forEach 方法的行为类似于 for 循环。但是您不必定义它将执行多少次迭代，因为它将执行与输入数组中的项目数相等的迭代。

4.map() 方法的行为类似于 forEach，但主要区别在于，它返回一个新数组作为结果。

5.filter() 方法的行为类似于 map() 并返回一个数组作为结果。但正如名称所描述的，它返回一个过滤后的结果数组。

6.我们列表中的下一个方法是 some()。这个方法和every()完全一样。不同之处在于我们检查输入数组的所有元素的条件，如果有任何元素满足条件，则返回 true。

7.find() 方法返回通过测试（函数内判断）的数组的第一个元素的值

8.findIndex() 方法返回输入数组中满足 find 方法 callbackFn 中给定条件的第一个元素的索引。否则返回-1，表示没有数组项通过条件检查。语法将与 find() 方法保持相同，只是返回结果会有所不同。

9.pop() 方法从数组中删除最后一项并返回该项。输入数组的长度减1。
```

