# 单链表代码

```php
<?php

# 构建链表节点
class Node
{
    public $data;
    public $next;
    
    public function __construct($data, $next)
    {
        $this->data = $data;
        $this->next = $next;
    }
}

# 构建单链表
class SingleLinkList
{
    # 头插法创建链表
    # n为节点总数
    public function headInsert($n)
    {
        # 新建一个节点
        $head = new Node(null, null);
        for ($i = $n; $i > 0; $i--) {
            $newNode = new Node($i, null);
            $head->data = $newNode->data; # 新建节点赋值给头节点
            $newNode->next = $head->next; # 将头节点的后续节点作为新建节点
            $head->next = $newNode;
        }
        return $head;
    }
}
```



