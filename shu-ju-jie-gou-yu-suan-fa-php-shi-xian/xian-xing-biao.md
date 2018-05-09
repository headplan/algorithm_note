# 线性表

定义 : 零个或多个数据元素的**有限序列** .

除首尾外 , 均只有一个直接前驱和直接后继 . 直接前驱和直接后继 , 意思是前面后面只有一个 .

一个数组元素可以有若干数据项组成 .

线性表**有顺序存储\(比如数组\)**和**链式存储\(比如链表\)**两种存储结构 .

堆栈、队列、串、数组等都是线性表 .

---

#### 顺序存储方式

**线性结构**的**顺序表示**指的是用一组地址连续的存储单元依次存储线性结构的数据元素 . 在PHP中我们可以通过数组模拟这一特征 .

在PHP中可以通过数组模拟这一特征 :

```php
<?php

/**
 * Linear seq 就是线性序列的意思
 */
class Linear_seq
{
    # 顺序存储体
    protected $cache;

    public function __construct($cache = [])
    {
        $this->cache = $cache;
    }

    # 获取线性结构的长度
    public function length()
    {
        return count($this->cache);
    }

    # 判断线性结构是否为空
    public function isEmpyt()
    {
        return empty($this->cache);
    }

    /**
     * 向顺序结构中插入元素
     * @param $value 要插入的节点
     * @param $index 要插入的位置,这个位置是从零开始的
     * @return bool
     */
    public function insert($value, $index)
    {
        $length = $this->length();
        # 校验插入位置的合法性,不合法则返回false
        if ($index < 0 || $index > $length) {
            return false;
        }

        # 插入操作,把第$index的位置空出来,也就是到$index之后的位置都向后移动了一个位置
        # 索引是从0开始的,这里把$length当做移了一个位置后的最大索引,也就是$i.
        # $i > $index 这个索引位置插入到顺序结构中,不是头尾
        # $i-- 循环大于这个索引位置的索引
        for ($i = $length; $i > $index; $i--) {
            $this->cache[$i] = $this->cache[$i-1];
        }
        $this->cache[$index] = $value;

        return true;
    }

    /**
     * 插入到最后
     * @param $value
     * @return bool
     */
    public function push($value)
    {
        return $this->insert($value, $this->length());
    }

    /**
     * 插入到最前
     * @param $value
     * @return bool
     */
    public function unshift($value)
    {
        return $this->insert($value, 0);
    }

    /**
     * 从顺序结构中删除元素
     * @param $index
     * @return mixed|null
     */
    public function delete($index)
    {
        $length = $this->length();
        # 校验删除位置的合法性,不合法则返回null
        if ($index < 0 || $index > $length-1) {
            return NULL;
        }
        # 记录一下要删除的节点值
        $value = $this->cache[$index];
        # 索引值都向前移动了1,$this->cache[$i+1]获取后面的值赋值给前面的
        for ($i = $index; $i < $length - 1; $i++) {
            $this->cache[$i] = $this->cache[$i+1];
        }
        # 删除最后一个索引值
        unset($this->cache[$length-1]);

        return $value;
    }

    /**
     * 删除最后一个元素
     * @return mixed|null
     */
    public function pop()
    {
        return $this->delete($this->length()-1);
    }

    /**
     * 删除第一个元素
     * @return mixed|null
     */
    public function shift()
    {
        return $this->delete(0);
    }

    /**
     * 根据$index查找元素
     * @param $index
     * @return mixed|null
     */
    public function findValueByIndex($index)
    {
        $length = $this->length();
        if ($index < 0 || $index > $length - 1) {
            return NULL;
        }

        return $this->cache[$index];
    }

    /**
     * 根据元素查找$index
     * 根据元素找序号需要遍历,找到第一个就返回序号,遍历完没找到元素则返回-1
     * @param $value
     * @return int
     */
    public function findIndexByValue($value)
    {
        $length = $this->length();
        for ($i = 0; $i < $length; $i++) {
            if ($value === $this->cache[$i]) {
                return $i;
            }
        }

        return -1;
    }

    /**
     * 修改指定$index的值
     * @param $newValue
     * @param $index
     * @return bool
     */
    public function update($newValue, $index)
    {
        $length = $this->length();
        if ($index < 0 || $index > $length -1) {
            return false;
        }
        $this->cache[$index] = $newValue;

        return true;
    }

    /* 两个线性结构之间的操作 */

    /**
     * 将第二个线性结构合并到第一个线性结构中
     * 把第二个线性结构每一个元素都加入到第一个线性结构中
     * @param $seq
     * @return bool
     */
    public function merge($seq)
    {
        if (! ($seq instanceof Linear_seq)) {
            return false;
        }

        $length = $seq->length();
        for ($i = 0; $i < $length; $i++) {
            $this->push($seq->findValueByIndex($i));
        }

        return true;

    }

    /**
     * 求两个线性结构元素的并集
     * 把第一个线性结构的元素复制
     * 然后把第二个线性结构特有的元素添加进去
     * @param $seq1
     * @param $seq2
     * @return \Linear_seq
     */
    public static function unique($seq1, $seq2)
    {
        $seq = new Linear_seq();
        if (! ($seq1 instanceof Linear_seq) || ! ($seq2 instanceof Linear_seq)) {
            return $seq;
        }

        $length1 = $seq1->length();
        for ($i = 0; $i < $length1; $i++) {
            $seq->push($seq1->findValueByIndex($i));
        }

        $length2 = $seq2->length();
        for ($i = 0; $i < $length2; $i++) {
            $value = $seq2->findValueByIndex($i);
            if ($seq1->findIndexByValue($value) === -1) {
                $seq->push($value);
            }
        }

        return $seq;
    }

    /**
     * 求两个线性结构元素的交集
     * @param $seq1
     * @param $seq2
     * @return \Linear_seq
     */
    public static function intersection($seq1, $seq2)
    {
        $seq = new Linear_seq();
        if (! ($seq1 instanceof Linear_seq) || ! ($seq2 instanceof Linear_seq)) {
            return $seq;
        }

        $length1 = $seq1->length();
        for ($i = 0; $i < $length1; $i++) {
            $value1 = $seq1->findEleByIndex($i);
            if ($seq2->findIndexByValue($value1) !== -1) {
                $seq->push($value1);
            }
        }

        return $seq;
    }
}
```

#### 链式存储方式

线性结构的链式存储结构的特点是用一组任意的存储单元存储线性表的数据元素 .

链式存储结构有单链表 , 双链表等 , 查看下一章节内容 . 

#### 顺序存储方式和链式存储方式的比较

**顺序表**

* 顺序表有以下优点 : 存储密度大 , 无需为表示元素之间的逻辑关系额外使用存储空间 ; 根据序号查找元素很容易 . 
* 顺序表的缺点是插入和删除元素需要移动大量的操作 . 

**链表**

* 链表优点是插入和删除操作只需要修改相关指针域 , 不需要移动元素 . 
* 链表的缺点是存储密度小 , 需要额外的字段表示元素间的关系 ; 根据序号查找元素需要从头找起 . 



