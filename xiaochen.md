# 动态规划
## 63. 不同路径 II
### 题目描述:
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。
机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish”）。
现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？
网格中的障碍物和空位置分别用 1 和 0 来表示。
```js
var uniquePathsWithObstacles = function (obstacleGrid) {
    const m = obstacleGrid.length;
    const n = obstacleGrid[0].length;
    const dp = Array(m).fill().map((item) => Array(n).fill(0)); //初始dp数组
    for (let i = 0; i < m && obstacleGrid[i][0] === 0; i++) {
        //初始列
        dp[i][0] = 1;
    }
    for (let i = 0; i < n && obstacleGrid[0][i] === 0; i++) {
        //初始行
        dp[0][i] = 1;
    }
    for (let i = 1; i < m; ++i) {
        for (let j = 1; j < n; ++j) {
            //遇到障碍直接返回0
            dp[i][j] = obstacleGrid[i][j] === 1 ? 0 : dp[i - 1][j] + dp[i][j - 1];
        }
    }
    return dp[m - 1][n - 1];
};
```
`&& obstacleGrid[i][0] === 0` 如果遇到1那么之后的所有都是1，简化操作
- 自己写的
```js
var uniquePathsWithObstacles = function (obstacleGrid) {
  const m = obstacleGrid.length;
  const n = obstacleGrid[0].length;
  const meno = new Array(m).fill(0).map(() => new Array(n).fill(0));
  if (obstacleGrid[0][0] === 1) {
    return 0;
  }
  meno[0][0] = 1;
  for (let i = 1; i < m; i++) {
    meno[i][0] = meno[i - 1][0];
    if (obstacleGrid[i][0] === 1) {
      meno[i][0] = 0;
    }
  }
  for (let j = 1; j < n; j++) {
    meno[0][j] = meno[0][j - 1];
    if (obstacleGrid[0][j] === 1) {
      meno[0][j] = 0;
    }
  }
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      meno[i][j] = meno[i - 1][j] + meno[i][j - 1];
      if (obstacleGrid[i][j] === 1) {
        meno[i][j] = 0;
      }
    }
  }
  return meno[m - 1][n - 1];
};
```
## 70.爬楼梯
### 时间:
2023-10-10
## 279.完全平方数
### 时间:
2023-10-10
### 题解:
https://leetcode.cn/problems/perfect-squares/solutions/1115069/279-wan-quan-ping-fang-shu-by-chen-wei-f-gwzs/
```js
var numSquares = function(n) {
const dp=new Array(n+1).fill(0);
for(let i=1;i<=n;i++){
    dp[i]=i;
    for(let j=1;i-j*j>=0;j++){
        dp[i]=Math.min(dp[i],dp[i-j*j]+1)
    }
}
    return dp[n]
};
```
## 120.三角形最小路径和
### 时间:
2023-10-11
### 题目:
https://leetcode.cn/problems/triangle/
### 题解:
![|560](photo&pdf/Pasted%20image%2020231011210316.png)
```js
  var minimumTotal = function (triangle) {
    const h = triangle.length;
    const dp = new Array(h)
      .fill(0)
      .map(() => new Array(triangle[h - 1].length));
    for (let i = h - 1; i >= 0; i--) {
      for (let j = 0; j <= triangle[i].length - 1; j++) {
        if (i == h - 1) {
          dp[i][j] = triangle[i][j];
        } else {
          dp[i][j] = Math.min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j];
        }
      }
    }
    return dp[0][0];
  };
```
