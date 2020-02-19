# 最好 , 最坏 , 平均 , 均摊时间复杂度

* 最好情况时间复杂度\(best case time complexity\)
* 最坏情况时间复杂度\(worst case time complexity\)
* 平均情况时间复杂度\(average case time complexity\)
* 均摊时间复杂度\(amortized time complexity\)

#### 最好、最坏情况时间复杂度

看一下下面代码的时间复杂度

```c
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



