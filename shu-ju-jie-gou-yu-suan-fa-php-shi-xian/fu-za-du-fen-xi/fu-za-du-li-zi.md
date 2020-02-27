# 复杂度例子

在计算时间复杂度的时候 , 首先需要找出算法的基本操作 , 然后根据相应的各语句确定它的执行次数 , 再找出T\(n\)的同数量级 , 找出后f\(n\) = 该数量级 , 若T\(n\)/f\(n\)求极限可得到一常数c , 则时间复杂度 T\(n\) = O\(f\(n\)\) .

**O\(1\) : 常数复杂度\(Constant Complexity\)**

```py
n = 1000
print(n)
```

**O\(log\(n\)\) : 对数复杂度\(Logarithmic Complexity\)**

```py
i = 1
n = 1000
while i < n:
  print(i)
  i = i * 2 # 终止条件为对数
```

**O\(n\) : 线性复杂度\(Linear Complexity\)**

```py
n = 1000
for i in range(n):
  print(i)
```

**平方复杂度\(N Square Complexity\)**

**立方复杂度\(N Cube Complexity\)**

**指数复杂度\(Exponential Growth\)**

**阶乘复杂度\(Factorial Complexity\)**

