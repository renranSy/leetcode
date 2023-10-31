# LeetCode题解之路

> 2023年10月28日，我通过这样的方式来记录自己的拙劣的题解，那天晚上，我下定了冲大厂的决心——黄沙百战穿金甲，不破楼兰终不还！

## 80. 删除有序数组中的重复项

### （1）计数

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let mark = 0;
    let index = 0;
    while (index < nums.length) {
        if (mark === 0) {
            mark++
            index++
        } else if (mark === 1) {
            if (nums[index] !== nums[index - 1]) {
                mark = 0
            } else {
                mark++
                index++
            }
        } else {
            if (nums[index] !== nums[index - 1]) {
                mark = 0
            } else {
                nums.splice(index, 1)
            }
        }
    }
}
```

### （2）双指针

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let left = 0
    let right = 1
    while (right < nums.length) {
        if (nums[right] === nums[left] && right - left < 2) {
            right++
        } else if (nums[right] === nums[left]) {
            nums.splice(right, 1)
        } else {
            left = right
            right++
        }
    }
}
```

## 169. 多数元素

### （1）先排序，后找到多数元素

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function (nums) {
    nums.sort()
    let index = 0
    let mark = 1
    while (index < nums.length && mark < nums.length / 2) {
        if (nums[index] === nums[index + 1]) {
            mark++
        } else {
            mark = 1
        }
        index++
    }
    return nums[index]
};
```

### （2）Boyer-Moore 投票算法

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function (nums) {
    let index = 1
    let value = nums[0]
    let count = 1
    while (index < nums.length) {
        if (count === 0) {
            value = nums[index]
        }
        if (nums[index] === value) {
            count++
        } else {
            count--
        }
        index++
    }
    return value
};
```

## 189. 轮转数组

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var rotate = function(nums, k) {
    Array.from({ length: k % nums.length }, () => nums.unshift(nums.pop()))
};
```

## 121. 买卖股票的最佳时机

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let profit = 0
    for (let i = 0; i < prices.length - 1; i++) {
        for (let j = i + 1; j < prices.length; j++) {
            if (prices[j] - prices[i] > profit) {
                profit = prices[j] - prices[i]
            }
        }
    }
    return profit
};
```

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let maxProfit = 0
    let minPrice = prices[0]

    for (let i = 0; i < prices.length; i++) {
        if (prices[i] < minPrice) {
            minPrice = prices[i]
        } else if (prices[i] - minPrice > maxProfit) {
            maxProfit = prices[i] - minPrice
        }
    }
    return maxProfit
};
```

## 125. 验证回文串

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    const regex = /[^a-z0-9]/gi
    s = s.replace(regex, '').toLowerCase()
    for (let i = 0; i < s.length / 2; i++) {
        if (s[i] !== s[s.length - 1 - i]) {
            return false
        }
    }
    return true
};
```

