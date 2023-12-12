# 1. 两数之和 #哈希表 
## 题目描述：
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出和为目标值 target  的那两个整数，并返回它们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
你可以按任意顺序返回答案。
## 解题思路
![](photo&pdf/Pasted%20image%2020230915154820.png)
## 解题代码
```javascript
var twoSum = function(nums, target) {
    const map=new Map();
    for(let i=0;i<nums.length;i++){
        const complement=target - nums[i];
        if(map.has(complement)){
            return [i,map.get(complement)]}
        else{
            map.set(nums[i],i)
    }
    }
};
```
# 2.两数相加 #链表
## 描述：
![|320](photo&pdf/Pasted%20image%2020230915164131.png)
## 思路:
## 代码:
```JavaScript
var addTwoNumbers = function(l1, l2) {
    let dummy=new ListNode(0);
    let current=dummy;
    let carry=0;
    while(l1!==null ||l2!== null){
        let sum=0;
        if(l1!=null){
            sum+=l1.val; #l1的节点值
            l1=l1.next;
        }
        if(l2!=null){
            sum+=l2.val;
            l2=l2.next;
        }      
        sum+=carry;
        current.next=new ListNode(sum%10);
        carry=Math.floor(sum/10);
        current=current.next;
    }
    if (carry>0){
        current.next=new ListNode(carry);
    }
    return dummy.next;
};
```
让我逐步解释这段代码的执行过程：
1. 首先，我们创建了一个虚拟节点 `dummy`，它的值被初始化为 `0`。这个虚拟节点在遍历过程中会作为结果链表的头节点，并且它的值没有实际意义，只是用来简化操作。
2. 我们定义了一个指针 `current`，初始化为 `dummy`，用来在遍历过程中构建结果链表。
3. 我们定义了一个变量 `carry`，用来表示进位。初始时，进位值为 `0`。
4. 进入 `while` 循环，循环条件是只要 `l1` 或 `l2` 中至少有一个节点没有遍历完，就继续执行。
5. 在每次循环迭代中，我们首先初始化 `sum` 为 `0`，用来存储当前位置上 `l1` 和 `l2` 的节点值之和。
6. 如果 `l1` 不为空，则将 `l1` 的节点值加到 `sum` 中，并将 `l1` 移向下一个节点。
7. 如果 `l2` 不为空，则将 `l2` 的节点值加到 `sum` 中，并将 `l2` 移向下一个节点。
8. 将当前进位值 `carry` 加到 `sum` 中。
9. 创建一个新的节点 `current.next`，其值为 `sum % 10`，这是因为每个节点的值应该在 0 到 9 之间。
10. 更新进位值 `carry`，它等于 `Math.floor(sum / 10)`，表示下一位的进位值。
11. 将 `current` 指针移向下一个节点，准备处理下一位。
12. 循环结束后，如果最高位有进位（`carry > 0`），则创建一个额外的节点来存储进位。
13. 最后，返回 `dummy.next`，这是结果链表的头节点。
这段代码的关键思想是模拟了手工相加两个整数的过程，通过逐位相加并处理进位，得到结果链表。这是一个非常常见且有实际应用的链表问题。
创建新链表时，指针位置在0，假设链表第一个位置是1的话。
# 3. 无重复字符的最长子串 #滑动窗口法 
## 题目描述
给定一个字符串 s ，请你找出其中不含有重复字符的最长子串的长度
![|350](photo&pdf/Pasted%20image%2020230919145430.png)
## 思路：
#滑动窗口法
![](photo&pdf/Pasted%20image%2020230919153423.png)
![](photo&pdf/Pasted%20image%2020230919153454.png)

## 代码
```javascript
  var lengthOfLongestSubstring = function (s) {
    const set = new Set();
    let i = 0,
      j = 0,
      maxlength = 0;
    if (s.length == 0) {
      return 0;
    }

    for (i; i < s.length; i++) {
      if (!set.has(s[i])) {
        set.add(s[i]);
        maxlength = Math.max(maxlength, set.size);
      } else {
        while (set.has(s[i])) {
          set.delete(s[j]);
          j++;
        }
        set.add(s[i]);
      }
    }
    return maxlength;
  };
```
# 4. 最长回文字串(第五题)
## 时间
9.19
## 题目描述:
给你一个字符串 s，找到 s 中最长的回文子串。
如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。
示例 1：
输入：s = "babad" 输出："bab"
解释："aba" 同样是符合题意的答案。
示例 2：
输入：s = "cbbd"
输出："bb"
## 解题思路:
![](photo&pdf/Pasted%20image%2020230919162826.png)
# 解题代码:
```JavaScript
  var longestPalindrome = function (s) {
    if (s.length < 2) {
      return s;
    }
    let start = 0;
    let maxLength = 1;
    function helper(left, right) {
      while (left >= 0 && right < s.length && s[left] === s[right]) {
        if (right - left + 1 > maxLength) {
          start = left;
          maxLength = right - left + 1;
        }
        left--;
        right++;
      }
    }
    
    for (let i = 0; i < s.length; i++) {
      helper(i - 1, i + 1);
      helper(i, i + 1);
    }
    return s.substring(start, start + maxLength);
  };
```
## `===` & `==`
在 JavaScript 中，`===` 和 `==` 是两种比较操作符，它们之间有明显的区别：
1. `===`（严格相等）：
   - `===` 用于比较两个值是否严格相等，包括值和数据类型。
   - 如果两个操作数的值和数据类型都相等，比较返回 `true`。
   - 如果值或数据类型不相等，比较返回 `false`。
   - 例如：`3 === 3` 返回 `true`，`"3" === 3` 返回 `false`。
2. `==`（相等）：
   - `==` 用于比较两个值是否相等，但不考虑数据类型。
   - 如果两个操作数的值相等（在弱类型转换后），比较返回 `true`。
   - 如果值不相等，或者数据类型不同但可以进行弱类型转换得到相等的值，则比较返回 `true`。
   - 例如：`3 == 3` 返回 `true`，`"3" == 3` 也返回 `true`，因为 `"3"` 会被弱类型转换为 `3` 进行比较。
总结区别：
- `===` 执行严格相等比较，要求值和数据类型都相等。
- `==` 执行相等比较，会进行弱类型转换，只要值在弱类型转换后相等，就返回 `true`。
# 5.三数之和(第15题) #数组
## 时间
9.19
## 题目描述:
给你一个整数数组 nums ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j、i != k 且 j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请你返回所有和为 0 且不重复的三元组。
# 思路:
![](photo&pdf/Pasted%20image%2020230919200823.png)
## 代码:
```JavaScript
 var threeSum = function (nums) {
    nums.sort((a, b) => a - b);#排序
    const result = [];
    for (let i = 0; i < nums.length - 2; i++) {
      if (i === 0 || nums[i] != nums[i - 1]) {
        let start = i + 1;
        let end = nums.length - 1;
        while (start < end) {
          const sum = nums[i] + nums[start] + nums[end];
          if (sum === 0) {
            result.push([nums[i], nums[start], nums[end]]);
            start++;
            end--;
            while (start < end && nums[start] === nums[start - 1]) {
              start++;
              while (start < end && nums[end] === nums[end + 1]) {
                end--;
              }
            }
          } else if (sum < 0) {
            start++;
          } else {
            end--;
          }
        }
      }
    }
    return result;
  };
```
## 总结
"三数之和"（3Sum）是一道经典的数组问题，要求在给定整数数组中找出所有不重复的三元组，使得三元组的元素之和等于0。
解决这个问题的一种常见方法是使用双指针和排序，以下是解题的关键步骤和注意事项：
1. **排序数组：** 首先对输入的整数数组进行排序。排序是为了方便后续的双指针操作，并且有助于处理重复元素。
2. **双指针法：** 使用两个指针 `left` 和 `right` 分别指向数组中的元素，从头尾开始向中间靠拢。同时，使用一个额外的指针 `i` 来遍历数组中的每个元素。
3. **遍历数组：** 在外层循环中，遍历数组中的每个元素 `nums[i]`（注意，循环范围通常是 `0` 到 `nums.length - 3`，以避免越界）。
4. **处理重复元素：** 在内层循环中，需要处理重复元素的情况。如果当前元素 `nums[i]` 与前一个元素相同（即 `i > 0 && nums[i] === nums[i - 1]`），则**跳过当前元素**，以避免重复计算相同的三元组。
5. **双指针求解：** 在内层循环中，使用双指针 `left` 和 `right` 来寻找符合条件的三元组。具体操作如下：
   - 计算当前三元组的和 `sum = nums[i] + nums[left] + nums[right]`。
   - 如果 `sum === 0`，则找到一个符合条件的三元组，将其添加到结果数组中，并分别将 `left` 和 `right` 向中间移动一位，**同时跳过重复元素**，以避免重复计算。
   - 如果 `sum < 0`，说明当前和偏小，需要增大和，将 `left` 右移一位。
   - 如果 `sum > 0`，说明当前和偏大，需要减小和，将 `right` 左移一位。
6. **返回结果：** 最终，返回结果数组，其中包含所有不重复的三元组，使得它们的和等于0。

## 跳过重叠元素
在这段代码中，后面两种情况不需要特别考虑重复元素的问题，因为在 `sum < 0` 和 `sum > 0` 的情况下，当前的 `sum` 不等于零，所以不会构成符合条件的三元组，因此也不会涉及到重复的三元组。
1. 当 `sum < 0` 时，这表示当前三个元素的和偏小，为了使 `sum` 等于 0，我们需要增加 `sum`。因此，将 `start` 右移一步，将 `nums[start]` 的值增大，这有助于使 `sum` 更接近 0。
2. 当 `sum > 0` 时，这表示当前三个元素的和偏大，为了使 `sum` 等于 0，我们需要减小 `sum`。因此，将 `end` 左移一步，将 `nums[end]` 的值减小，同样有助于使 `sum` 更接近 0。
在这两种情况下，即使 `start` 或 `end` 指向的元素与前一个元素相同，也不会导致构成符合条件的三元组，因为当前的 `sum` 不等于 0，所以不会加入结果数组。只有在 `sum === 0` 的情况下，才会添加符合条件的三元组，而添加三元组的时候，已经考虑了跳过重复元素的逻辑。
因此，只有在 `sum === 0` 的情况下需要特别处理重复元素，而在其他情况下不需要考虑。这是为了避免重复计算相同的三元组。

# 6. L19 删除链表的倒数第 N 个结点 #链表
## 题目描述:
给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。
## 思路:
双指针固定间隔
## 代码:
```JavaScript
  var removeNthFromEnd = function (head, n) {
    let dummy = new ListNode();
    dummy.next = head;
    let n1 = dummy;
    let n2 = dummy;
    for (let i = 0; i <= n; i++) {
      n2 = n2.next;
    }
    while (n2 !== null) {
      n2 = n2.next;
      n1 = n1.next;
    }
    n1.next = n1.next.next;
    return dummy.next;
  };
```
# 7.L20有效的括号
## 时间:
2023-9-21
## 题目:
给定一个只包括 `'('，')'，'{'，'}'，'['，']'` 的字符串 s ，判断字符串是否有效。
有效字符串需满足：
左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
每个右括号都有一个对应的相同类型的左括号。
## 思路:
#stack
![](photo&pdf/Pasted%20image%2020230921221938.png)
只有左右括号前后关系才会返回，所以如果栈顶输出的内容(上一个字符对于的右括号)与当前字符不一样，那么一定错误
## 解答:
```JavaScript
var isValid = function(s) {
const map=new Map();
const stack=[];
map.set('(',')');
map.set('{','}');
map.set('[',']');
for(let i=0;i<s.length;i++){
    if(map.has(s[i])){
        stack.push(map.get(s[i]))
    }else{
        poped=stack.pop();
        if(poped!==s[i]){
            return false;
        }
    }
}
if(stack.length!==0){
    return false;
}else{
    return true;
}
};
```
###解法2:
```javascript
Var isValid = function(s) {
    Const stack = [];
    For (let val of s) {
        Console.Log(stack)
        If (val === '(') stack.Push(')');
        Else if (val === '[') stack.Push(']');
        Else if (val === '{') stack.Push('}');
        Else if (stack.Length === 0 || val !== stack.Pop()) return false;
    }
    Return stack.Length === 0;
};
```
## stack 栈:
栈（Stack）是一种常见的数据结构，它遵循后进先出（Last-In-First-Out，LIFO）的原则，类似于现实生活中的一叠盘子或者一摞书。栈通常支持两种基本操作：入栈（Push）和出栈（Pop）。
以下是栈的主要特点和操作：
1. **入栈（Push）：** 将元素添加到栈的顶部，使其成为新的栈顶元素。
2. **出栈（Pop）：** 从栈的顶部移除元素，栈顶元素被弹出。
3. **栈顶（Top）：** 获取栈顶元素，但不移除它。
4. **空栈（Empty）：** 检查栈是否为空。
5. **栈的大小（Size）：** 获取栈中元素的数量。
栈的应用非常广泛，它常常用于解决需要后进先出顺序的问题，例如：
- 函数调用栈：用于跟踪函数的调用和返回。
- 表达式求值：用于解析和计算数学表达式。
- 浏览器的前进和后退功能：用于记录浏览历史记录。
- 编译器和解释器：用于解析和执行程序代码。
在 JavaScript 中，你可以使用数组模拟栈的行为，具体来说，使用 `push()` 方法入栈，`pop()` 方法出栈，`peek()` 方法获取栈顶元素，`length` 属性获取栈的大小，以及检查数组是否为空来实现栈的操作。以下是一个简单的示例：
```javascript
// 创建一个空栈
const stack = [];

// 入栈
stack.push(1);
stack.push(2);
stack.push(3);

// 出栈
const popped = stack.pop(); // 弹出栈顶元素，popped 等于 3

// 获取栈顶元素
const top = stack[stack.length - 1]; // 获取栈顶元素，top 等于 2

// 检查栈是否为空
const isEmpty = stack.length === 0; // isEmpty 等于 false

// 获取栈的大小
const size = stack.length; // size 等于 2
```
# 8. L21 合并两个有序链表 #链表 
## 时间:
2023-9-22
## 题目描述:
将两个升序链表合并为一个新的升序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
## 思路:
1. 迭代
![](photo&pdf/Pasted%20image%2020230923144608.png)
2. 递归
直接用 mergeTwoLists 当作递归函数：
- 递归边界：如果其中一个链表为空，直接返回另一个链表作为合并后的结果。
- 如果两个链表都不为空，则比较两个链表当前节点的值，并选择较小的节点作为新链表的当前节点。例如 list1的节点值更小，那么递归调用 mergeTwoLists(list1.Next, list2)，将递归返回的链表接在 list1的末尾。
## 代码:
```js
var mergeTwoLists = function(list1, list2) {
    let dummy = new ListNode(); // 用哨兵节点简化代码逻辑
    let cur = dummy; // cur 指向新链表的末尾
    while (list1 && list2) {
        if (list1.val < list2.val) {
            cur.next = list1; 
            %或者% cur.next = new ListNode(list1.val);// 把 list1 加到新链表中
            list1 = list1.next;
        } else { // 注：相等的情况加哪个节点都是可以的
            cur.next = list2; // 把 list2 加到新链表中
            list2 = list2.next;
        }
        cur = cur.next;
    }
    cur.next = list1 ? list1 : list2; // 拼接剩余链表
    return dummy.next;
};

```
```js
Var mergeTwoLists = function (list1, list2) {
    If (list1 === null) return list2; // 注：如果都为空则返回空
    If (list2 === null) return list1;
    If (list1.Val < list2.Val) {
        List1.Next = mergeTwoLists(list1.Next, list2);
        Return list1;
    }
    List2.Next = mergeTwoLists(list1, list2.Next);
    Return list2;
};
```
# 9 . L24 两两交换链表中的节点
## 时间:
2023-9-24
## 题目描述:
给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。
## 思路:
![](photo&pdf/Pasted%20image%2020230924134653.png)
## 代码:
```js
var swapPairs = function(head) {
let dummy=new ListNode();
dummy.next=head;
let cur=dummy;
while(cur.next!==null && cur.next.next!==null){
    let n1=cur.next;
    let n2=cur.next.next;
    cur.next=n2;
    n1.next=n2.next;
    n2.next=n1;
    cur=n1;

}
return dummy.next;
};
```
## 10. L49 字母异位词分组
## 时间:
2023-9-26
## 题目描述:
给你一个字符串数组，请你将字母异位词组合在一起。可以按任意顺序返回结果列表。
字母异位词是由重新排列源单词的所有字母得到的一个新单词。
## 思路&代码:
思路1:排序
```js
var groupAnagrams = function(strs) {
const map= new Map();
for (let str of strs){
const sortedStr = str.split('').sort().join('');
if(map.has(sortedStr)){
map.set(sortedStr,[...map.get(sortedStr),str])
}else{
    map.set(sortedStr,[str])
}
}
return [...map.values()];
};
```
思路2:  计数法 #哈希表 
![](photo&pdf/Pasted%20image%2020230927105912.png)
```js
var groupAnagrams = function(strs) {
if (strs.length==0){
    return [];
}
const map =new Map();
for (const str of strs){
    const asciii=new Array(26).fill(0);
    for(let i=0;i<str.length;i++){
        const a="a";
        const asciicode=str.charCodeAt(i)-a.charCodeAt(0);
        asciii[asciicode]++;
    }
    const key=asciii.join("");#把单独的字符连接成一个字符串
    if(map.has(key)){
        map.set(key,[...map.get(key),str])
    }else{
        map.set(key,[str])
    }
}
return [...map.values()]
};
```
## ascii
在 JavaScript 中，你可以使用以下方式来处理 ASCII 字符和编码：
1. **获取字符的 ASCII 编码：**
   - 使用 JavaScript 的 `charCodeAt()` 方法可以获取一个字符的 ASCII 编码值。
   - 示例：
   ```javascript
   const char = 'A';
   const asciiCode = char.charCodeAt(0);
   console.log(asciiCode); // 输出：65
   ```
2. **获取 ASCII 编码对应的字符：**
   - 使用 JavaScript 的 `String.fromCharCode()` 方法可以将 ASCII 编码值转换为相应的字符。
   - 示例：

   ```javascript
   const asciiCode = 65;
   const char = String.fromCharCode(asciiCode);
   console.log(char); // 输出：'A'
   ```
3. **遍历字符串的字符和 ASCII 编码：**
   - 你可以使用循环来遍历字符串的每个字符，并获取它们的 ASCII 编码。
   - 示例：
   ```javascript
   const str = 'Hello';
   for (let i = 0; i < str.length; i++) {
       const char = str[i];
       const asciiCode = char.charCodeAt(0);
       console.log(`Character: ${char}, ASCII Code: ${asciiCode}`);
   }
   ```
## 连接成一个字符串
假设 `c` 是一个包含字符的数组，例如：
```javascript
const c = ['a', 'b', 'c', 'd'];
```
然后，`c.join("")` 将把数组中的字符连接在一起，形成一个字符串：
```javascript
const key = c.join(""); // key 的值为 "abcd"
```
所以，`key` 最终的值将是数组 `c` 中的所有字符按顺序连接在一起的字符串。这对于将字符数组转换为字符串非常有用，特别是在处理密码、密钥或其他需要字符串表示的数据时。
## 字符串排序
### 法1: 数组
如果你想对单个字符串中的字母进行排序，可以将字符串拆分为字符数组，然后使用数组的排序方法进行排序。以下是一个示例：
```javascript
const str = "banana";
const sortedStr = str.split('').sort().join('');
console.log(sortedStr); // 输出：'aaabnn'
```
在上述示例中：
1. `str.split('')` 将字符串 `str` 拆分为字符数组，每个字符成为数组的一个元素。结果是 `['b', 'a', 'n', 'a', 'n', 'a']`。
2. `sort()` 方法对字符数组进行默认的字典顺序排序。
3. `join('')` 方法将排序后的字符数组重新连接成一个字符串。
法2:
```js
let array = Array.from(str);//字符转成数组
array.sort();//排序
let key = array.toString();
```
# 11. L53 最大子序列和
# 时间:
2023-9-28
## 题目描述:
## 思路:
#动态规划 
我们使用两个变量 maxSum 和 currentSum(dp[i])来跟踪最大和和当前子数组的最大和。我们从数组的第二个元素开始遍历数组，对于每个元素，我们要么选择开始一个新的子数组，要么将当前元素加入当前子数组，以便找到最大和。最终，maxSum 将包含最大和的值。
## 代码:
```js
var maxSubArray = function(nums) {
const dp=new Array(nums.length);
let max=nums[0];
if(nums.length===1){
return nums[0]
}
dp[0]=nums[0]
for(i=1;i<nums.length;i++){
    dp[i]=Math.max(dp[i-1]+nums[i],nums[i])
    max=Math.max(dp[i],max)
}
return max;
};
```
# 12.L54 螺旋矩阵
## 时间:
2023-9-28
## 思路:
遍历到底


![](photo&pdf/Pasted%20image%2020230928155741.png)
## 代码:
```js
  var spiralOrder = function (matrix) {
    let left = 0;
    let right = matrix[0].length - 1;
    let top = 0;
    let bottom = matrix.length - 1;
    let result = [];
    while (left <= right && top <= bottom) {
      if (direction == "right") {
        for (let i = left; i <= right; i++) {
          result.push(matrix[top][i]);
        }
        top++;
        direction = "down";
      } else if (direction == "down") {
        for (let i = top; i <= bottom; i++) {
          result.push(matrix[i][right]);
        }
        right--;
        direction = "left";
      } else if (direction === "left") {
        for (let i = right; i >= left; i--) {
          result.push(matrix[bottom][i]);
        }
        bottom--;
        direction = "up";
      } else if (direction === "up") {
        for (let i = bottom; i >= top; i--) {
          result.push(matrix[i][left]);
        }
        left++;
        direction = "right";
      }
    }
    return result;
  };
```
## 二维数组的形状:
```js
// 创建一个形状为 3x4 的二维数组
const twoDArray = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12]
];

// 获取二维数组的行数和列数
const numRows = twoDArray.length; // 获取行数，此处 numRows 为 3
const numCols = twoDArray[0].length; // 获取列数，假设所有一维数组具有相同的长度，此处 numCols 为 4
```
# 13. L55 跳跃游戏
## 题目描述:
给你一个非负整数数组 nums ，你最初位于数组的第一个下标。数组中的每个元素代表你在该位置可以跳跃的最大长度。
判断你是否能够到达最后一个下标，如果可以，返回 true ；否则，返回 false 。
## 时间:
2023-9-30
## 思路:
https://leetcode.cn/problems/jump-game/solutions/1143641/tan-xin-dong-tai-gui-hua-dong-hua-tu-jie-47ie/
#动态规划 #贪心 
1.  反向查找
解题思路：
![|410](photo&pdf/Pasted%20image%2020230930122731.png)
```js
var canJump = function (nums) {
	let end=nums.length-1;
	for(let i=nums.length-2;i>=0;i--){
	if(end-i<=nums[i]){
		end=i;
	}
	}
	return end==0;
}
```
2. 贪心
思路：不用考虑每一步跳跃到那个位置，而是尽可能的跳跃到最远的位置，看最多能覆盖的位置，不断更新能覆盖的距离。
![](photo&pdf/Pasted%20image%2020230930123126.png)
```js
    var canJump = function (nums) {
	if(nums.length===1) return true;
	let cover =nums[0];
	for(let i=0;i<=cover;i++){
	    cover=Math.max(nums[i]+i,cover)
	    if(cover>=nums.length-1){
	        return true;
	    }
	}
	return false;
}
```
# 14. L56 合并区间
## 时间:
2023-9-30
## 题目:
![](photo&pdf/Pasted%20image%2020231001152444.png)
https://leetcode.cn/problems/merge-intervals/description/
## 思路&代码:
https://leetcode.cn/problems/merge-intervals/solutions/1958491/by-finedaybreak-wr2x/
```js
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function(intervals) {
    // 先进行排序 （区间第一个元素）从小到大
    const sortedIntervals = intervals.sort((a, b) => a[0] - b[0]);
    const result = [];
    // 取出第一个区间
    let current = sortedIntervals[0];
    for (let i = 1; i < sortedIntervals.length; i++) {
        // 循环比较后面的区间
        const interval = sortedIntervals[i];
        // 如果下一个区间的最小值 存在于当前比较的区间（小于当前区间的最大值） 则合并
        if (interval[0] <= current[1]) {
            // 合并取两个区间最大值的最大者
            current[1] = Math.max(current[1], interval[1]); // case 1
        } else {
            // 如果不在前一个区间内 说明当前区间与下一个区间不连续 则把当前区间添加到结果集
            result.push(current);
            // 更新比较的当前区间为下一个区间
            current = interval; // case 2
        }
    }
    // 遍历结束之后两种情况 
    // case 1 最后一个区间被合并，则需要将current添加到结果集
    // case 2 最后一个区间没有被合并，也需要将current添加到结果集
    result.push(current);
    return result;
};
```
# 15. L62不同路径
## 题目描述:
https://leetcode.cn/problems/unique-paths/
![|320](photo&pdf/Pasted%20image%2020231001153550.png)
## 时间:
2023-7-10
## 思路&代码:
```js
var uniquePaths = function (m, n) {
  const meno = new Array(m);
  for (let i = 0; i < m; i++) {
    memo[i] = new Array(n);
  }
  #创建二维数组的两种方法
  const meno = new Array(m).fill(0).map(() => new Array(n).fill(0));
  
  for (let row = 0; row < m; row++) {
    meno[row][0] = 1;
  }
  for (let cols = 0; cols < n; cols++) {
    meno[0][cols] = 1;
  }
  for (let row = 1; row < m; row++) {
    for (let cols = 1; cols < n; cols++) {
      meno[row][cols] = meno[row - 1][cols] + meno[row][cols - 1];
    }
  }
  return meno[m - 1][n - 1];
};
```
## 创建二维数组:
创建一个(m,n)的数组
```js
  #创建二维数组的两种方法
  for (let i = 0; i < m; i++) {
    memo[i] = new Array(n);
  }

  const meno = new Array(m).fill(0).map(() => new Array(n).fill(0));
```
# 16.L66 加一
## 时间:
2023-10-7
## 题目描述:
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。
最高位数字存放在数组的首位，数组中每个元素只存储单个数字。
你可以假设除了整数 0 之外，这个整数不会以零开头。
## 思路&代码:
![|470](photo&pdf/Pasted%20image%2020231007164807.png)
```js
var plusOne = function(digits) {
    const len = digits.length;
    for(let i = len - 1; i >= 0; i--) {
        digits[i]++;
        digits[i] %= 10;
        if(digits[i]!=0)
            return digits;
    }
    digits = [...Array(len + 1)].map(_=>0);;
    digits[0] = 1;
    return digits;
	return [1,...digits];
};
链接：https://leetcode.cn/problems/plus-one/
```
# 17. L70 爬楼梯
## 时间:
2023-7-10
## 题目描述:
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
https://leetcode.cn/problems/climbing-stairs/description/
## 思路&代码:
1. 动态规划
假设 n = 5，有 5 级楼梯要爬
题意说，每次有2种选择：爬1级，或，爬2级。
如果爬1级，则剩下4级要爬。
如果爬2级，则剩下3级要爬。
这拆分出 2 个问题：
爬4级楼梯有几种方式？
爬3级楼梯有几种方式？
于是，爬 5 级楼梯的方式数 = 爬 4 级楼梯的方式数 + 爬 3 级楼梯的方式数。
```js
var climbStairs = function(n) {
	let dp=[];
	dp[0]=0;
	dp[1]=1;
	dp[2]=2;
	for(i=3;i<=n;i++){
	    dp[i]=dp[i-1]+dp[i-2]
	}
	return dp[n]
};
```
# 18.  L746  使用最小花费爬楼梯
## 时间:
2023-10-7
## 题目:
给你一个整数数组 cost ，其中 cost[i] 是从楼梯第 i 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。
你可以选择从下标为 0 或下标为 1 的台阶开始爬楼梯。
请你计算并返回达到楼梯顶部的最低花费。
https://leetcode.cn/problems/min-cost-climbing-stairs/description/
## 思路&代码:
#动态规划
```js
var minCostClimbingStairs = function(cost) {
	let dp=[];
	const n=cost.length;
	dp[0]=0;
	dp[1]=0;
	for(i=2;i<=n;i++){
	    dp[i]=Math.min(dp[i-1]+cost[i-1],dp[i-2]+cost[i-2])
	}
	return dp[n]
	};
```
# 19. L73 矩阵置零 set matrix zeroes
## 时间:
2023-10-12
## 思路&题解:
一个容易得到的方法是：遍历一次矩阵，记录一下每行、列是否出现了 0；如果出现了 0，最终将此行列置为 0。
```js
  var setZeroes = function (matrix) {
    const m = matrix.length;
    const n = matrix[0].length;
    const row = new Set();
    const col = new Set();
    for (let i = 0; i < m; i++) {
      for (let j = 0; j < n; j++) {
        if (matrix[i][j] === 0) {
          row.add(i);
          col.add(j);
        }
      }
    }
    for (let i = 0; i < m; i++) {
      for (let j = 0; j < n; j++) {
        if (col.has(i) || col.has(j)) {
          matrix[i][j] = 0;
        }
      }
    }
  };
```
# 20.L78 子集
## 时间:
2023-10-13
## 思路&题解:
#回溯 
![](photo&pdf/Pasted%20image%2020231013155754.png)
https://leetcode.cn/problems/subsets/solutions/420458/shou-hua-tu-jie-zi-ji-hui-su-fa-xiang-jie-wei-yun-/
![|410](photo&pdf/Pasted%20image%2020231013161221.png)
```js
  var subsets = function (nums) {
    const len = nums.length;
    const result = [];
    function backtrack(start, curr) {
      result.push([...curr]);
      for (let i = 0; i < nums.length; i++) {
        curr.push(nums[i]);
        backtrack(i + 1, curr);
        curr.pop();
      }
    }
    backtrack(0, []);
    return result;
  };
  
  const subsets = (nums) => {
	  const res = [];
	  const dfs = (index, list) => {
	    res.push(list.slice());     // 调用子递归前，加入解集
	    for (let i = index; i < nums.length; i++) { // 枚举出所有可选的数
	      list.push(nums[i]);       // 选这个数
	      dfs(i + 1, list);         // 基于选这个数，继续递归，传入的是i+1，不是index+1
	      list.pop();               // 撤销选这个数
	    }
	  };
	  dfs(0, []);
	  return res;
};
```
# 21. L83 删除排序链表中的重复元素 #链表
## 时间:
2023-10-14
## 思路&代码:
![](photo&pdf/Pasted%20image%2020231014205707.png)
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var deleteDuplicates = function(head) {
let cur=head;
while(cur !=null && cur.next != null) {
if(cur.val == cur.next.val){
    cur.next=cur.next.next;
}else{
    cur=cur.next;
}
}
return head;
};
```
#  22.   L90.子集Ⅱ #回溯
# 时间:
2023-10-30
# 思路:
子集+排序+去重
```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function(nums) {
 const res=[];
 const n=nums.length;
  nums=nums.sort((a,b)=>a-b);
 function backtrack(index,list){
     res.push(list.slice());
     for(let i=index;i<n;i++){
         if(i>index&&nums[i]==nums[i-1]){
             continue;
         }
         list.push(nums[i]);
         backtrack(i+1,list);
         list.pop();
     }
 }
 backtrack(0,[]);
 return res;
};
```