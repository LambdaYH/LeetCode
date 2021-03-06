---
title: 121. Best Time to Buy and Sell Stock
date: 2021-03-20 15:35:50 +0800
categories: leetcode
---
#### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minPrice = INT_MAX;
        int maxProfit = 0;
        for(size_t i = 0; i < prices.size(); ++i)
        {
            if(prices[i] < minPrice)
            {
                minPrice = prices[i];
            }
            if(prices[i] - minPrice > maxProfit )
            {
                maxProfit = prices[i] - minPrice;
            }
        }
        return maxProfit;
    }
};
```
##### [Kadane’s Algorithm](https://zh.wikipedia.org/wiki/%E6%9C%80%E5%A4%A7%E5%AD%90%E6%95%B0%E5%88%97%E9%97%AE%E9%A2%98)
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxCur = 0;
        int maxSoFar = 0;
        for(auto i = prices.begin() + 1; i != prices.end(); ++i )
        {
            maxCur = max(0, (*i - *(i-1)) + maxCur);
            maxSoFar = max(maxCur, maxSoFar);
        }
        return maxSoFar;
    }
};
```
