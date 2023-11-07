```js
// 小知识  js中字符串的多个空格 解析器会认为只是一个空格 但是打印的时候还是会打印多个
// 去除前后空格用trim 如果要去除整个字符串的 需要用正则表达式  s = s1.replace('/\s*/g', '')

let str = "   这    是    一 个      有 空 格 的 字 符 串        ";  
let trimmedStr = str.replace(/\s*/g,''); // 参数1为匹配所有空格,参数2使用''替换
console.log(trimmedStr);  // 这是一个有空格的字符串
```



计算最后一个单词的长度

```js
var lengthOfLastWord = function(s) {
    let index = s.length - 1;
    // 小知识  js中字符串的多个空格 解析器会认为只是一个空格 但是打印的时候还是会打印多个
    // 这个判断用来解决要是字符串结束位置有多个空格的情况
    while (s[index] === ' ') {
        index--;
        console.log('我是空格');
    }
    let wordLength = 0;
    while (index >= 0 && s[index] !== ' ') {
        wordLength++;
        index--;
    }
    console.log(wordLength);
    return wordLength;
};
let s ="moon     "
lengthOfLastWord(s)
```

