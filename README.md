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



