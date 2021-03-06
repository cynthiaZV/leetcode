## 买卖股票的最佳时机
### 题目描述

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

**示例 1:**
```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2:**
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

### 解法
可以将整个数组中的数画到一张折现图中, 需要求的就是从图中找到一个波谷和一个波峰, 使其二者的差值最大化(其中波谷点需要在波峰点之前)。

我们可以维持两个变量, minprice(可能产生最大差值的波谷)初始值最大整数((1 << 31) -1), maxprofit(产生的最大差值)初始值 0, 然后迭代处理数组中的每个数进而优化两个变量的值; 如果数组元素`prices[i]`不比`minprice`大, 那就是目前为止最小波谷, 将 `minprice=prices[i]`;如果数组元素`prices[i]`比`minprice`大, 那就判断`prices[i]`与`minprice`的差值是否比`maxprofit`大, 如果是就更新`maxprofit=prices[i]-minprice`, 并且`minprice`即为波谷, `prices[i]`为波谷; 否的话继续处理下一个数组元素。

