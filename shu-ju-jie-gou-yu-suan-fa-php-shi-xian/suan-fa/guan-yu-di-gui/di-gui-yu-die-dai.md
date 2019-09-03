# 递归与迭代

#### 迭代

迭代算法是用计算机解决问题的一种基本方法 . 它利用计算机运算速度快、适合做重复性操作的特点 , 让计算机对一组指令\(或一定步骤\)进行重复执行 , 在每次执行这组指令\(或这些步骤\)时 , 都从变量的原值推出它的一个新值 . 

利用迭代算法解决问题 , 需要做好以下三个方面的工作 : 

1. 确定迭代变量 . 在可以用迭代算法解决的问题中 , 至少存在一个直接或间接地不断由旧值递推出新值的变量 , 这个变量就是迭代变量 . 
2. 建立迭代关系式 . 所谓迭代关系式 , 指如何从变量的前一个值推出其下一个值的公式\(或关系\) . 迭代关系式的建立是解决迭代问题的关键 , 通常可以使用递推或倒推的方法来完成 . 
3. 对迭代过程进行控制 . 在什么时候结束迭代过程 ? 这是编写迭代程序必须考虑的问题 . 不能让迭代过程无休止地重复执行下去 . 
   迭代过程的控制通常可分为两种情况 : 
   1. 一种是所需的迭代次数是个确定的值 , 可以计算出来 ; 
   2. 另一种是所需的迭代次数无法确定 . 

   对于前一种情况 , 可以构建一个固定次数的循环来实现对迭代过程的控制 . 对于后一种情况 , 需要进一步分析出用来结束迭代过程的条件 . 

可以用迭代的算法有很经典的问题 , 比如兔子产子问题 : 

> 假定你有一雄一雌一对刚出生的兔子 , 它们在长到一个月大小时开始交配 , 在第二月结束时 , 雌兔子产下另一对兔子 , 过了一个月后它们也开始繁殖 , 如此这般持续下去 . 每只雌兔在开始繁殖时每月都产下一对兔子 , 假定没有兔子死亡 , 在一年后总共会有多少对兔子 ? 
>
> 还有上楼梯的走法问题 : 有一段楼梯有10级台阶 , 规定每一步只能跨一级或两级 , 要登上第10级台阶有几种不同的走法 ?

#### 循环和迭代是一回事吗 ? 

**loop , iterate , traversal , recursion**

这几个词是计算机技术书中经常会出现的几个词汇 . 分别翻译为 , 循环 , 迭代 , 遍历 , 递归 . 乍一看 , 这几个词好像都与重复\(repeat\)有关 , 但有的又好像不完全是重复的意思 . 看一下解释 : 

* 循环\(loop\) : 指的是在满足条件的情况下 , 重复执行同一段代码 . 比如 , while语句 . 
* 迭代\(iterate\) : 指的是按照某种顺序逐个访问列表中的每一项 . 比如 , for语句 . 
* 遍历\(traversal\) : 指的是按照一定的规则访问树形结构中的每个节点 , 而且每个节点都只访问一次 . 
* 递归\(recursion\) : 指的是一个函数不断调用自身的行为 . 比如 , 以编程方式输出著名的斐波那契数列 . 

##### 迭代与循环

循环 : 不变的重复 . 

```php
for($i=0; $i < 8; $i++){
	echo 'Welcome to NowaMagic';
}
```

迭代 : "迭" , 轮流 , 轮番 , 替换 , 交替 , 更换 . "代" : 代替 . 所以迭代的意思是 , 变化的循环 , 这种变化就是轮番代替 , 轮流代替 . 



个人认为迭代是[循环](http://www.nowamagic.net/librarys/veda/tag/%E5%BE%AA%E7%8E%AF)的一种，循环体代码分为固定循环体，和变化的循环体。


