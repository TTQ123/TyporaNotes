利用set求并集交集差集

```js
const arr1 = [33, 33, 44, 1, 2, 5]
const arr2 = [33, 5, 7, 8, 9]

// 求并集
// 思路是 将arr1和arr2存入一个数组中放进set就自动去重了
const bj = [...new Set([...arr1, ...arr2])]  


// 求交集
// 思路是将arr1去重,然后通过filter找出arr2中和arr1相同的
const jj = [...new Set(arr1)].filter(item => arr2.includes(item))

// 求差集
// 差集就是并集减去交集
// 并集直接过滤掉交集
const cj = bj.filter(item => !jj.includes(item))
```

