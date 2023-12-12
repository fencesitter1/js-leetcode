# 9.20 
# 198.打家劫舍
## 时间:
9.21
## 题目描述:
你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。
给定一个代表每个房屋存放金额的非负整数数组，计算你不触动警报装置的情况下，一夜之内能够偷窃到的最高金额。
## 思路:
#动态规划
![|410](photo&pdf/Pasted%20image%2020230921145155.png)
## 代码:
```javascript
var rob = function(nums) {
    const len=nums.length;
    const dp=new Array(len+1);
    if(len===0){
        return 0;
    }
    dp[0]=0;
    dp[1]=nums[0];
    for(let i =2;i<=len;i++){
        dp[i]=Math.max(dp[i-1],dp[i-2]+nums[i-1])
    }
    return dp[len];
};
```
# 213.打家劫舍 II
## 时间:
9.21
## 题目描述:
你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都围成一圈，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统,如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。
给定一个代表每个房屋存放金额的非负整数数组,计算你在不触动警报装置的情况下，今晚能够偷窃到的最高金额。
## 思路:
#动态规划 
分为偷第一家和偷最后一家的情况
## 代码:
- 自己写的
```JavaScript
var rob = function(nums) {
    const len=nums.length;
    const dp=new Array(len+1);
    if(len===0){
        return 0;
    }
    if(len===1){
        return nums[0];
    }
    dp[0]=0;
    dp[1]=0;#设为0，偷最后一家
    for(let i =2;i<=len;i++){
        dp[i]=Math.max(dp[i-1],dp[i-2]+nums[i-1])
    }
    let max2=dp[len];

    dp[0]=0;
    dp[1]=nums[0];
    for(let i =2;i<=len-1;i++){
        dp[i]=Math.max(dp[i-1],dp[i-2]+nums[i-1])
    }
    #len-1,偷第一家，不考虑最后一家的情况
    let max1= dp[len-1];
    return Math.max(max1,max2)
};
```
- 题解2:
![|410](photo&pdf/Pasted%20image%2020230921154911.png)
https://leetcode.cn/problems/house-robber-ii/solutions/1851373/java-by-rerewrre-eli7/?envType=daily-question&envId=2023-09-21
```javascript
var rob = function(nums) {
    let n = nums.length
    if(n==1){
        return nums[0]
    }
    let dp = new Array(n).fill(0)
    dp[0] = nums[0]
    dp[1] = nums[0] > nums[1] ? nums[0] : nums[1]
    // 第一种情况：只遍历1~n-1的房屋，最后一个房屋不遍历
    for(let i = 2; i < n - 1; i++){
        dp[i] = Math.max(dp[i-2]+nums[i],dp[i-1])   
    }
    let max1 = dp[n-2]
    // 第二种情况：只遍历2~n的房屋，第一个房屋不遍历
    dp[1] = nums[1]
    dp[2] = nums[1] > nums[2] ? nums[1] : nums[2]
    for(let i = 3; i < n; i++){
        dp[i] = Math.max(dp[i-2]+nums[i],dp[i-1])   
    }
    let max2 = dp[n-1]
    max1 = max1 > max2 ? max1 : max2
    return max1
};

```
# 9 .22
# 2591. 将钱分给最多的儿童
## 题目描述:
给你一个整数 money ，表示你总共有的钱数（单位为美元）和另一个整数 children ，表示你要将钱分配给多少个儿童。
你需要按照如下规则分配：
所有的钱都必须被分配。
每个儿童至少获得 1 美元。
没有人获得 4 美元。
请你按照上述规则分配金钱，并返回最多有多少个儿童获得恰好 8 美元。如果没有任何分配方案，返回 -1 。
# 思路:
#贪心
结合思路中的“注意”点，一共有以下四种情况：
- 情况一：money 少于 children，怎么都得不到满足条件的结果，返回 -1
- 情况二：money 恰好分 children - 1 个小朋友 8 个，最后一个小朋友 4 个，需要最后一个小朋友减掉一个，同时选前面一个小朋友多一个，一共减了 2 个满足条件的小朋友，返回 children - 2
- 情况三：money 比每个小朋友拿 8 个还多，那剩余的钱就直接全部给其中一个小朋友，相当于减掉了 1 个满足条件的小朋友，返回 children - 1
- 情况四：（贪心策略）每个小朋友先拿 1 个，剩余钱为 money - children ，然后剩余的钱除以 7，相当于能拿 7 + 1 = 8 的小朋友数，能分几个就是几个。
作者：AF_J
链接： https://leetcode.cn/problems/distribute-money-to-maximum-children/
## 代码:
- 解法一
```JavaScript

var distMoney = function(money, children) {
   if(money < children) return-1;
   if(money === (children*8-4)) return children-2;//n-1分8，正好剩下4，要调整2个人
   if(money > children*8) return children-1;//每个人都分8，有剩余全部给一个人 
   return Math.floor((money-children)/7);
};
```
- 解法2
```JavaScript
var distMoney = function(money, children) {
if(money<children){
    return -1;
}
let left=money-children*1;
let num=0;
let ans=0;
while(left>=7){
    left-=7;
    ans++;
    if(left===3&&ans===children-1){
        ans--;
        break
    }
    if(ans===children){
        if(left>0){
            ans--
        }
        break
    }
}
    return ans
};
```
# L121.买卖股票的最佳时机
## 题目描述:

## 时间:
2023-10-1

## 思路&代码:
https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/solutions/379936/teng-xun-leetcode121mai-mai-gu-piao-de-zui-jia-shi/
#动态规划
![|380](photo&pdf/Pasted%20image%2020231001162626.png)
```js
let maxProfit = function(prices) {
    let max = 0, minprice = prices[0]
    for(let i = 1; i < prices.length; i++) {
        minprice = Math.min(prices[i], minprice)##找出最小买入点
        max = Math.max(max, prices[i] - minprice)#比较最大利润
    }
    return max
}
```
## L.122 买卖股票的最佳时机2
## 时间:
2023-10-3
## 思路:
- 思路1:状态机
视频讲解: https://www.bilibili.com/video/BV1ho4y1W7QK/?vd_source=d87fb0764722135b00d998541b55f906
![](photo&pdf/Pasted%20image%2020231003145043.png)
![](photo&pdf/Pasted%20image%2020231003145123.png)
![](photo&pdf/Pasted%20image%2020231003145143.png)
- 思路2 
https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/solutions/1115482/mai-mai-gu-piao-wen-ti-by-chen-wei-f-gc4k/
![|590](photo&pdf/Pasted%20image%2020231003150414.png)
```js
var maxProfit = function(prices) {
	let n=prices.length;
	let dp=new Array(n).fill(0).map(() =>new Array(2).fill(0));
	dp[0][0]=0;
	dp[0][1]=-prices[0]
	for(let i=1;i<prices.length;i++){
	dp[i][0]=Math.max(dp[i-1][0],dp[i-1][1]+prices[i]);
	dp[i][1]=Math.max(dp[i-1][1],dp[i-1][0]-prices[i]);
	}
	return dp[n-1][0]
};
```
状态压缩和语义化
```js
const maxProfit = function (prices) {
    let n = prices.length;
    let dp = Array.from(new Array(n), () => new Array(2));
    dp[0] = 0;
    dp[1] = -prices[0];
    for (let i = 1; i < n; i++) {
        dp[0] = Math.max(dp[0], dp[1] + prices[i]);
        dp[1] = Math.max(dp[1], dp[0] - prices[i]);
    }
    return dp[0];
};

//语意化
const maxProfit = function (prices) {
    let n = prices.length;
    let sell = 0;
    let buy = -prices[0];
    for (let i = 1; i < n; i++) {
        sell = Math.max(sell, buy + prices[i]);
        buy = Math.max(buy, sell - prices[i]);
    }
    return sell;
};

https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/
```
