# [两数之和](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组nums和一个目标值 target , 请你在该数组中找出和为目标值的那两个整数 , 并返回他们的数组下标 .

你可以假设每种输入只会对应一个答案 . 但是 , 你不能重复利用这个数组中同样的元素 .

> 示例:  
> 给定 nums = \[2, 7, 11, 15\], target = 9  
> 因为 nums\[0\] + nums\[1\] = 2 + 7 = 9  
> 所以返回 \[0, 1\]

#### 方法一：暴力法

暴力法很简单 , 遍历每个元素x , 并查找是否存在一个值与\(target - x\)相等的目标元素 .

```php
<?php

class Solution
{
    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target)
    {
        foreach ($nums as $k1 => $v1) {
            foreach ($nums as $k2 => $v2) {
                if ($k1 === $k2) {
                    continue;
                }
                if ($v2 === $target - $v1) {
                    return [$k1, $k2];
                }
            }
        }
    }
}
```

```php
<?php

class Solution
{
    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target)
    {
        for ($i = 0; $i < count($nums); $i++) {
            for ($j = $i + 1; $j < count($nums); $j++) {
                if ($nums[$j] === $target - $nums[$i]) {
                    return [$i, $j];
                }
            }
        }
    }
}
```



