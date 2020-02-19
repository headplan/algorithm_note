# 最好 , 最坏 , 平均 , 均摊时间复杂度

* 最好情况时间复杂度\(best case time complexity\)
* 最坏情况时间复杂度\(worst case time complexity\)
* 平均情况时间复杂度\(average case time complexity\)
* 均摊时间复杂度\(amortized time complexity\)

#### 最好、最坏情况时间复杂度

看一下下面代码的时间复杂度

```cpp
// n表示数组array的长度
int find(int[] array, int n, int x) {
  int i = 0;
  int pos = -1;
  for (; i < n; ++i) {
    if (array[i] == x) pos = i;
  }
  return pos;
}
```

代码要实现的功能是在一个无序的数组\(array\)中 , 查找变量 x 出现的位置 . 如果没有找到 , 就返回 -1 .

代码的复杂度是O\(n\) , 其中 , n 代表数组的长度 .

在数组中查找一个数据 , 并不需要每次都把整个数组都遍历一遍 , 因为有可能中途找到就可以提前结束循环了 . 所以 , 上面的代码并不够高效 , 优化一下 :

```cpp
// n表示数组array的长度
int find(int[] array, int n, int x) {
  int i = 0;
  int pos = -1;
  for (; i < n; ++i) {
    if (array[i] == x) {
       pos = i;
       break;
    }
  }
  return pos;
}
```

根据前面说的分析方式 , 这段优化后的代码的时间复杂度还是O\(n\) , 也就是说变量 x 可能出现在数组的任意位置 , 如果数组中第一个元素正好是要查找的变量 x , 那时间复杂度就是 O\(1\) . 不同的情况下 , 代码的时间复杂度是不一样的 . 

为了表示代码在不同情况下的不同时间复杂度 , 引入三个概念 : 最好情况时间复杂度、最坏情况时间复杂度和平均情况时间复杂度 . 

