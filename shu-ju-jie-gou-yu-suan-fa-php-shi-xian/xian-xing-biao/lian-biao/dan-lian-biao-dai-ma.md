# 单链表

![](/assets/danlianbiao.png)

![](/assets/jiediancunchuneirong.png)

* data : 数据域 , 存放结点的值
* next : 指针域 , 存放结点的直接后继的地址

**单链表的操作**

* 插入节点 : 头插/尾插 也叫前插/后插 , 其实就是head所指向节点不一样 , 当然他们的时间复杂度也不一样 , 头插O\(1\) , 尾插O\(n\)
* 删除节点 : 先找到要删除的节点位置 , 将父节点的next指向其子节点,然后删除该节点
* 查询节点 : 从head开始一级一级的往下找
* 编辑节点 : 从head开始一级一级的往下找,找到后编辑器内容
* 节点排序 : 后面说排序算法

```php
<?php

/**
 * 链表节点存储类
 * Class Node_Linded
 */
class Node_Linded
{
    # 节点数据
    public $data;
    # 下一个节点记录
    public $next = null;

    /**
     * 初始化节点数据
     * Node_Linded constructor.
     * @param null $value
     */
    public function __construct($value = null)
    {
        $this->data = $value;
    }

    public function update($newValue)
    {
        $this->data = $newValue;
    }
}

/**
 * 链表操作类
 * Class Linear_Linked
 */
class Linear_Linked
{
    # 头结点,存储Node_Linded对象,也可以是存储链表的所有Node_Linded对象信息,因为是面向对象的
    protected $head;

    /**
     * 初始化头节点
     * Linear_Linked constructor.
     */
    public function __construct()
    {
        # 初始化头节点,也就是单链表的头
        $this->head = new Node_Linded();
    }

    /**
     * 获取节点头信息,也就是获取所有Node_Linded对象信息
     */
    public function getHead()
    {
        return $this->head;
    }

    /**
     * 计算链表节点数
     * @return int
     */
    public function length()
    {
        # 初始化节点数
        $length = 0;
        # 获取头节点信息,因为其中包含下一个节点的信息
        $prev = $this->getHead();
        # 循环头节点中的next信息,不为null则将其赋值给$prev,继续循环下一个节点.
        while ($prev->next) {
            $prev = $prev->next;
            # 节点长度+1
            $length++;
        }

        return $length;
    }

    /**
     * 判断链表是否为空,就是判断头结点中是否有下一个节点信息还是为空.
     */
    public function isEmpyt()
    {
        return $this->getHead()->next === null;
    }

    /**
     * 清空链表节点
     */
    public function clear()
    {
        $this->getHead()->next = null;
    }

    /**
     * 插入节点
     * @param $value
     * @param $index
     * @return bool
     */
    public function insert($value, $index)
    {
        # 获取链表节点数
        $length = $this->length();
        # 判断要插入节点的key是否符合要求
        if ($index < 0 || $index > $length) {
            return false;
        }
        # 生成新的节点,存入节点data,也就是节点值,next指向为null
        # data=value
        # next=null
        $node = new Node_Linded($value);

        # 这里用的是头插方,所以首先获取头节点信息,当然这里在PHP对象中可以遍历所有.
        $prev = $this->getHead();
        # 如果是头插,这里$index默认为0,这一步跳过
        # 根据要插入的节点的位置,也就是$index,循环出这个位置的节点信息
        # 循环后$prev = Node{$index}{data='test',next=Node}
        for ($i = 0; $i < $index; $i++) {
            $prev = $prev->next;
        }

        # 然后把新建的节点和前面循环到的节点连接上
        # 也就是把$prev的next{data='test',next=Node}等等后续,连接到新建节点Node的next上.
        # 此时的node节点就是包含了data信息,又包含了next后续的内容的节点.
        $node->next = $prev->next;
        # 最后再将这个新的节点$node,赋值给前面for循环到的位置
        $prev->next = $node;

        return true;
    }

    /**
     * 有了前面的insert方法,实现头插和尾插就方便多了
     * 头插默认是从head后的第一个节点,也就是0节点开始插入,所以省略了for循环,一下找到了0节点,复杂度为O(1)
     * 尾插的复杂度是O(n)
     */

    /**
     * 头插
     * @param $value
     * @return bool
     */
    public function unshift($value)
    {
        return $this->insert($value, 0);
    }

    /**
     * 尾插
     * @param $value
     * @return bool
     */
    public function push($value)
    {
        return $this->insert($value,$this->length());
    }

    public function delete($index)
    {
        # 获取链表节点数
        $length = $this->length();
        # 判断要插入节点的key是否符合要求
        if ($index < 0 || $index > $length - 1) {
            return null;
        }

        $prev = $this->getHead();
        # 找到要删除的节点
        for ($i = 0; $i < $index; $i++) {
            $prev = $prev->next;
        }

        # 然后新建一个节点,其实这里就是把节点信息赋值给一个变量先存着
        $next = $prev->next;
        # 这里就是$prev->next->data;下的值,就是找到的要删除的节点的值
        $value = $next->data;
        # 这里就是把找到的节点下面的节点信息,当成找到节点下面的信息赋值,中间就剔除了删除的节点
        $prev->next = $next->next;
        # 然后清空,删除
        $next->next = NULL;
        unset($next);
        # 返回刚才删除的值
        return $value;
    }

    /**
     * 删除最后一个节点
     * @return null
     */
    public function pop()
    {
        return $this->delete($this->length()-1);
    }

    /**
     * 删除第一个节点,也就是0节点,而不是head
     * @return null
     */
    public function shift()
    {
        return $this->delete(0);
    }

    /**
     * 根据$index查找节点值
     * @param $index
     * @return null
     */
    public function findValueByIndex($index)
    {
        $length = $this->length();
        if ($index < 0 || $index > $length-1) {
            return NULL;
        }

        $prev = $this->getHead();
        for ($i = 0; $i < $index; $i++)
        {
            $prev = $prev->next;
        }

        return $prev->next->data;
    }

    /**
     * 根据value值查找$index
     * @param $value
     * @return int
     */
    public function findIndexByValue($value)
    {
        $length = $this->length();
        $prev = $this->head();
        for ($i = 0; $i < $length; $i++)
        {
            $prev = $prev->next;
            if ($prev->data === $value) {
                return $i;
            }
        }

        return -1;
    }

    /**
     * 返回序号所对应的节点的前一个节点
     * @param $index
     * @return null
     */
    public function findNodeByIndex($index)
    {
        $length = $this->length();
        if ($index < 0 || $index > $length-1) {
            return NULL;
        }

        $prev = $this->getHead();
        for ($i = 0; $i < $index; $i++) {
            $prev = $prev->next;
        }

        return $prev;
    }

    /**
     * 链表的合并就是把两个链表的头尾相连
     * @param $linked
     * @return bool
     */
    public function merge($linked)
    {
        if(! ($linked instanceof Linear_linked)) {
            return false;
        }
        # 找打输出链表$lined的头下面的节点信息,赋值给当前链表最后的next
        $this->tail()->next = $linked->getHead()->next;
        return true;
    }

    /**
     * 直接循环找到当前链表最后为null的节点
     * @return \Node_Linded|null
     */
    public function tail()
    {
        $prev = $this->getHead();
        while ($prev->next) {
            $prev = $prev->next;
        }
        return $prev;
    }

    /**
     * 节点值的更新,其实也是先找到$index节点,然后改一下value
     * @param $newValue
     * @param $index
     * @return bool
     */
    public function update($newValue, $index)
    {
        $length = $this->length();
        if ($index < 0 || $index > $length-1) {
            return false;
        }
        $prev = $this->getHead();
        for ($i = 0; $i < $index; $i++) {
            $prev = $prev->next;
        }

        $prev->next->update($newValue);
        return true;
    }

}

$a = new Linear_Linked();
$a->insert('a',0);
$a->insert('b',1);
$a->insert('c',2);
$a->push('666');

//die;
var_export($a->getHead());
```



