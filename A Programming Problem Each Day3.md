# 每日一题 Week4
### 排序数组 Medium 2019.3.31
给你一个整数数组 nums，请你将该数组升序排列
<https://leetcode-cn.com/problems/sort-an-array/>

**示例 1：**

```
输入：nums = [5,2,3,1]
输出：[1,2,3,5]

```


**注意：**

- 几种常用的排序算法以及其复杂度


### 代码 Python

```python3
class Solution:
    def merge(self, nums, l, m, r):
        help = [None] * (r - l + 1)
        i = 0
        left = l
        right = m + 1
        while left <= m and right <= r:
            if nums[left] < nums[right]:
                help[i] = nums[left]
                i += 1
                left += 1
            else:
                help[i] = nums[right]
                i += 1
                right += 1
        while left <= m:
            help[i] = nums[left]
            i += 1
            left += 1
        while right <= r:
            help[i] = nums[right]
            i += 1
            right += 1
        for j in range(len(help)):
            nums[l + j] = help[j]
        return nums


    def sortProcess(self, nums, L, R):
        if L == R:
            return
        mid = L + (R - L)//2
        self.sortProcess(nums, L, mid)
        self.sortProcess(nums, mid+1, R)
        self.merge(nums, L, mid, R)



    def sortArray(self, nums: List[int]) -> List[int]:
        if len(nums) < 2:
            return nums
        self.sortProcess(nums, 0, len(nums) - 1)
        return nums

```

### 字符串转换整数 Medium 2019.4.3
请你来实现一个 atoi 函数，使其能将字符串转换成整数。

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。接下来的转化规则如下：
如果第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字字符组合起来，形成一个有符号整数。
假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成一个整数。
该字符串在有效的整数部分之后也可能会存在多余的字符，那么这些字符可以被忽略，它们对函数不应该造成影响。
注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换，即无法进行有效转换。
在任何情况下，若函数不能进行有效的转换时，请返回 0 。
提示：
本题中的空白字符只包括空格字符 ' ' 。
假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−2^31,  2^31 − 1]。如果数值超过这个范围，请返回  INT_MAX (2^31 − 1) 或 INT_MIN (−2^31) 。

<https://leetcode-cn.com/problems/string-to-integer-atoi>

**示例 1：**

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。

```

**示例 2：**

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。

```

### 代码 Python

```python3
class Solution:
    def myAtoi(self, str: str) -> int:
        if len(str) == 0:
            return 0

        #flag = False
        start = True
        sign = 1
        res = []
        nums = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'}

        for i in range(len(str)):
            if str[i] == ' ' and start == True:
                continue
            #elif str[i] == ' ' and start == False:
                #break
            elif str[i] == '+' and start == True:
                sign = 1
                start = False
                res.append(str[i])
            elif str[i] == '-' and start == True:
                sign = -1
                start = False
                res.append(str[i])
            elif str[i] in nums:
                res.append(str[i])
                start = False
            else:
                break
        print(res)
        if '+' in res or '-' in res:
            res = res[1:]
        if len(res) == 0:
            return 0
        res = "".join(res)
        res = sign * int(res)
        if res < -2 ** 31:
            res = -2 ** 31
        elif res > 2 ** 31 - 1:
            res = 2 ** 31 - 1
        return res

```

### 接雨水1 Hard 2019.4.4
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。
<https://leetcode-cn.com/problems/trapping-rain-water/>


### 代码 Python

```python3
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        if n == 0:
            return 0
        left = 0
        right = n -1
        res = 0
        l_max = height[0]
        r_max = height[n-1]
        while left <= right:
            l_max = max(height[left], l_max)
            r_max = max(height[right], r_max)
            if l_max < r_max:
                res += l_max - height[left]
                left += 1
            else:
                res += r_max - height[right]
                right -= 1
        return res

```

### 括号生成 Medium 2019.4.9
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。
<https://leetcode-cn.com/problems/generate-parentheses/>


### 代码 Python

```python3
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        def dfs(l, r, curStr):
            if l == 0 and r == 0:
                res.append(curStr)
                return
            if l > 0:
                dfs(l -1, r, curStr + '(')
            if l < r:
                dfs(l, r - 1, curStr + ')')
        
        dfs(n, n, '')
        return res
```
