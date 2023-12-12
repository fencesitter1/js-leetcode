# 赛码网
- 情况1: 固定输入规模,只有一组输入(单行或者多行)
```js
let n = readInt();
let arr = [];
for(let i = 0; i < n; i++) {
    arr[i] = read_line();
}
```
- 不限制规模,可能要接受多组输入
```js
let line;
while(line = read_line()) {    // 如果读到输入文件结尾，就不会再进入循环了
    solve(line);    // 处理一组输入。如果一组输入有不止一行，那就在这里面再读几行。
}
```

![](photo&pdf/Pasted%20image%2020231210132031.png)
# 卡码网 
- `process.stdin` 和 `process.stdout`

在 Node.Js 环境中，`process.stdin` 和 `process.stdout` 是两个可用于标准输入和标准输出的流对象。
- `process.stdin`：代表标准输入流，它是一个可读流（Readable Stream），用于读取用户输入。
- `process.stdout`：代表标准输出流，它是一个可写流（Writable Stream），用于向控制台输出信息。

```js
const readline = require('readline');   
const rl = readline.createInterface({  
    input: process.stdin,
    output: process.stdout
});
let inputArr = [];

rl.on('line', (input) => {
    inputArr.push(input.trim().split(' ').map(Number));
    processfunction() 
	 rl.close();
	 });
```

- 输入多行数据输出一个结果
输入:
6 1
2 2 3 1 5 2
2 3 1 5 4 3
输出:
5
```js
const readline = require('readline');   
const rl = readline.createInterface({  
    input: process.stdin,
    output: process.stdout
});

let inputArr = [];

rl.on('line', (input) => {
    inputArr.push(input.trim().split(' ').map(Number)); 
    if(inputArr.length === 3) {
        let [m, n] = inputArr[0];
        let weight = inputArr[1];
        let value = inputArr[2];
        }
        console.log(dp[m - 1][n]);
        rl.close();
    }
})
```

- 输入一行输出一个结果
输入:
3 4
11 40
输出:
7
51

```js
// 引入readline模块来读取标准输入
const readline = require('readline');

// 创建readline接口
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

function preoceeInput() {
    rl.on('line', (input) => {
        const [a, b] = input.split(' ').map(Number);
        // # 遇到 0, 0 则中断
        if (a === 0 && b === 0) {
            return;
        } else {
            console.log(a + b);
        }
    });
}
preoceeInput()
```