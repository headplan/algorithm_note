# 查找算法

#### 顺序查找

也就是遍历查找 . 顺序查找也叫线性查找 , 它从第一个记录开始 , 逐个进行比较 , 是最基本的查找技术 .

```php
<?php
# $array为数组,$key为要查找的值
function search($array,$value)
{
    $n = count($array);
    for ($i = 0;$i < $n; $i++) {
        if ($array[$i] == $value) { # 逐一比较
            return $i;
        }
    }
    return false;
}

$items = [32,55,33,213,415,35,66,22];
var_dump(search($items, 4));
```

#### 二分查找

![](/assets/erfenchazhao.png)

```
算法思想：
用Low、High和Mid表示待查找区间的下界、上界和中间位置 ；
取中间位置 Mid= (Low+High)/2 ；
比较中间位置记录的关键字与给定的K值：
① 相等：查找成功；
② 大于：待查记录在区间的前半段，修改上界： High=Mid-1，转1 ；
③ 小于：待查记录在区间的后半段，修改下界：Low=Mid+1 ，转1 ；
直到越界(Low>High)，查找失败。
```



