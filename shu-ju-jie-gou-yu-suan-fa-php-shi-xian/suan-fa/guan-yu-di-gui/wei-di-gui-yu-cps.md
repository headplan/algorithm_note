# 尾递归与CPS

> 与普通递归相比 , 由于尾递归的调用处于方法的最后 , 因此方法之前所积累下的各种状态对于递归调用结果已经没有任何意义 , 因此完全可以把本次方法中留在堆栈中的数据完全清除 , 把空间让给最后的递归调用 . 这样的优化便使得递归不会在调用堆栈上产生堆积 , 意味着即使是"无限"递归也不会让堆栈溢出 . 这便是尾递归的优势 .
>
> **尾递归的本质 , 其实是将递归方法中的需要的"所有状态"通过方法的参数传入下一次调用中 . **

```c
int factorial(int n)
{
    if (n <= 2) {
        return 1;
    } else {
        return factorial(n-1) + factorial(n-2)
    }
}

int facorial_tail(int n, int acc1, int acc2)
{
    if (n < 2) {
        return acc1;
    } else {
        return factorial_tail(n-1, acc2, acc1+acc2);
    }
}
```

#### Continuation Passing Style的概念

所谓Continuation , 其实本来是一个函数调用机制 .

后续内容设计函数式概念较多 , 暂时到这 . 



参考 :

[http://www.defmacro.org/2006/06/19/fp.html](http://www.defmacro.org/2006/06/19/fp.html)

[https://github.com/justinyhuang/Functional-Programming-For-The-Rest-of-Us-Cn/blob/master/FunctionalProgrammingForTheRestOfUs.cn.md](https://github.com/justinyhuang/Functional-Programming-For-The-Rest-of-Us-Cn/blob/master/FunctionalProgrammingForTheRestOfUs.cn.md)

