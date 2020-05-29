# LeetCode

[https://leetcode.com/](https://leetcode.com/) - 英文站点

[https://leetcode-cn.com/](https://leetcode-cn.com/) - 中文站点

#### 使用介绍

**首页** - 登录后首页会有很多当前的消息 .

**探索** - 探索中有很多学习卡片 .

**题库** - 目前已经1000+的算法题了 , 右侧还有小的Topics .





二分查找也称折半查找\(Binary Search\) , 它是一种效率较高的查找方法 . 但是 , 折半查找要求线性表必须采用顺序存储结构 , 而且表中元素按关键字有序排列 . 

#### 查找过程

首先 , 假设表中元素是按升序排列 , 将表中间位置记录的关键字与查找关键字比较 , 如果两者相等 , 则查找成功 . 否则利用中间位置记录将表分成前、后两个子表 , 如果中间位置记录的关键字大于查找关键字 , 则进一步查找前一子表 , 否则进一步查找后一子表 . 重复以上过程 , 直到找到满足条件的记录 , 使查找成功 , 或直到子表不存在为止 , 此时查找不成功 . 

#### 算法要求

* 必须采用顺序存储结构 . 
* 必须按关键字大小有序排列 . 

#### 算法复杂度

二分查找的基本思想是将n个元素分成大致相等的两部分 , 取a\[n/2\]与x做比较 , 如果x=a\[n/2\] , 则找到x , 算法中止 ; 

如果x&lt;a\[n/2\] , 则只要在数组a的左半部分继续搜索x , 如果x&gt;a\[n/2\] , 则只要在数组a的右半部搜索x . 

时间复杂度即是while循环的次数 . 

#### PHP代码

```php
/**
 * 二分查找前提
 * 该数组已经是一个有序数组
 * 必须先排序再查找
 *
 * @param $array
 * @param $findVal
 * @param $leftIndex
 * @param $rightIndex
 */
function binarySearch(&$array, $findVal, $leftIndex, $rightIndex)
{
    $middleIndex = round(($rightIndex + $leftIndex) / 2);
    if ($leftIndex > $rightIndex) {
        echo '查无此数<br/>';

        return;
    }
    if ($findVal > $array[$middleIndex]) {
        binarySearch($array, $findVal, $middleIndex + 1, $rightIndex);
    } elseif ($findVal < $array[$middleIndex]) {
        binarySearch($array, $findVal, $leftIndex, $middleIndex - 1);
    } else {
        echo "找到数据:index=$middleIndex;value=$array[$middleIndex]<br/>";
        if ($array[$middleIndex + 1] == $array[$middleIndex] && $leftIndex < $rightIndex) {
            binarySearch($array, $findVal, $middleIndex + 1, $rightIndex);
        }
        if ($array[$middleIndex - 1] == $array[$middleIndex] && $leftIndex < $rightIndex) {
            binarySearch($array, $findVal, $leftIndex, $middleIndex - 1);
        }
    }
}
```



