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



