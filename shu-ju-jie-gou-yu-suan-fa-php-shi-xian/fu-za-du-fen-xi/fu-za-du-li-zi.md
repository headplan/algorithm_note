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

**O\(n^2\) : 平方复杂度\(N Square Complexity\)**

```py
n = 1000
for i in range(n):
  for j in range(n):
    print(i+j)
```

**O\(n^2\) : 立方复杂度\(N Cube Complexity\)**

```py
n = 1000
for i in range(n):
  for j in range(n):
    for k in range(n):
      print(i+j+k)
```

**O\(2^n\) : 指数复杂度\(Exponential Growth\)**

```py
import math

i = 1
n = 1000
while i < math.pow(2,n): # 终止条件为指数
  print(i)
```

**O\(n!\) : 阶乘复杂度\(Factorial Complexity\)**

```py
i = 1
n = 1000
while i < factorial(n): # 终止条件为指数
  print(i)

def factorial(n):
  if n == 0 or n == 1:
      return 1
  else:
      return (n * factorial(n - 1))
```

![](/assets/fuzadufenxi.png)

