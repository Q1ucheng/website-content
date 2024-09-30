# Lab08's Optional Problems

## Q5 Cycles
Link类可以表示带有循环的链表。也就是说，一个链表可以包含自身作为子链表。

```python
>>> s = Link(1, Link(2, Link(3)))
>>> s.rest.rest.rest = s
>>> s.rest.rest.rest.rest.rest.first
3
```

实现 `has_cycle` 函数，该函数返回其参数（一个Link实例）是否包含循环。

> 提示：遍历链表，并尝试记录你已经见过哪些Link对象。

记得之前在leecode上看过一种方法叫快慢指针，如果链表中有环，快指针会先于慢指针，并困于环中，慢指针进入环后必将有一个时刻，即快指针追上慢指针（套圈）：

```python
def has_cycle(link):
    slow = link
    fast = link.rest
    while slow and fast:
        if slow is fast:
            return True
        slow = slow.rest
        fast = fast.rest.rest
    return False
```

但是作业提示的方法有点不太会，不太清楚该用什么来存储已经遍历过的节点，遂询问GPT：

!!! success "GPT-4o's Answer"

    ```python
    def has_cycle(link):
        seen = set()
        while link is not Link.empty:
            if link in seen:
                return True
            seen.add(link)
            link = link.rest
        return False
    ```

但我不太理解为什么可以`if link in seen`，GPT回答道：

!!! Note

    在 Python 中，集合（set）是基于哈希表实现的，因此它能够快速地检查一个对象是否存在于集合中。对于 Link 类的实例，Python 会默认使用对象的内存地址来计算哈希值和进行比较。
    
    在 has_cycle 函数中，link 是一个 Link 类的实例，每个 Link 实例在内存中都有一个唯一的地址。这样，集合 seen 可以使用这些唯一的对象地址来判断一个 Link 实例是否已经存在于集合中。==换句话说，集合可以利用对象的唯一标识来判断其是否已被访问过。==
    
    为什么 if link in seen 能够工作？
    - 对象的唯一性: 每个 Link 对象在内存中的地址是唯一的，因此 link 对象在 seen 集合中是通过其唯一的内存地址来进行比较的。
    - 集合的哈希机制: 集合会计算对象的哈希值（通常是对象的内存地址），然后通过哈希值快速查找对象是否存在。

相比之下，快慢指针的空间复杂度为*O*(1)，只使用了两个指针的额外空间，而后一种方法空间复杂度为*O*(*N*)，其中 *N* 是链表中的节点数。主要为集合的开销（最坏情况下需要将每个节点都记录到集合中一次）

----

## Q6 Reverse

编写一个函数 `reverse_other`，该函数会改变树的结构，==使得每一层（奇数深度）的标签顺序被反转。==例如，`Tree(1, [Tree(2, [Tree(4)]), Tree(3)])` 变成 `Tree(1, [Tree(3, [Tree(4)]), Tree(2)])`。注意，这里反转的是标签而不是节点本身。

没什么好的想法，需要引入奇偶的标记就构造辅助函数：

```python
def reverse_other(t):
    """Mutates the tree such that nodes on every other (odd-depth) level
    have the labels of their branches all reversed.

    >>> t = Tree(1, [Tree(2), Tree(3), Tree(4)])
    >>> reverse_other(t)
    >>> t
    Tree(1, [Tree(4), Tree(3), Tree(2)])
    >>> t = Tree(1, [Tree(2, [Tree(3, [Tree(4), Tree(5)]), Tree(6, [Tree(7)])]), Tree(8)])
    >>> reverse_other(t)
    >>> t
    Tree(1, [Tree(8, [Tree(3, [Tree(5), Tree(4)]), Tree(6, [Tree(7)])]), Tree(2)])
    """
    def help_func(t, mark):
        if t.is_leaf():
            pass
        else:
            if mark:
                org_tree_list = [b.label for b in t.branches]
                new_tree_list = org_tree_list[::-1]
                for i in range(len(org_tree_list)):
                    t.branches[i].label = new_tree_list[i]
        for b in t.branches:
            help_func(b, not mark)
    help_func(t, True)
```

