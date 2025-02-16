# NOTE

## 总结
经过一周的的 leetcode 的做题训练，以前没有进行过像这种算法题的训练，作为一个计算机专业毕业的，上学的时候也没有进行过系统的训练，而是写业务代码多一点，学过 Android，做过 python，总是去写一些小项目，这个系统那个系统的，忽略了写代码的基本功。做了老师布置的题目，刚开始完全没有思路，有时候连题目的意思都没有理解清楚，操作的数组的方法，例如快慢指针，完全不知道。不过这几道题下来，慢慢的感觉到了里面的一些套路，还需自己多总结，多练习，自古深情留不住，唯有套路得人心。这周对快慢指针法影响比较深刻，需要多进行专项训练，熟练掌握这种方法。

做题思路  
1. 先暴力法解一遍。
2. 空间换时间，找一个中间变量，例如重新定义一个数组。
3. 把掌握的其他方法套一遍，看能不能解。
4. 想不出来就直接看答案。

目前工作中主要以 `Node.js` 为主，好多 `Java` 的语法都忘光了，老师课后布置的分析优先级队列的源码，还没有完全看懂，留个坑吧，后面再填。

## 数组
| 操作    | 时间复杂度 |
| ------- | :--------: |
| prepend |    O(1)    |
| append  |    O(1)    |
| lookup  |    O(1)    |
| insert  |    O(n)    |
| delete  |    O(n)    |

数组，连续的存储空间，可以根据下标实现随机访问，在数组的前面和后面删除或增加元素不需要移动其他元素，所以时间复杂度是 `O(1)`

## 链表
| 操作    | 时间复杂度 |
| ------- | :--------: |
| prepend |    O(1)    |
| append  |    O(1)    |
| lookup  |    O(n)    |
| insert  |    O(1)    |
| delete  |    O(1)    |

链表应为在存储是不连续的地址空间存储，每个结点包括值和后继指针，表示下一个元素的位置。所以在删除，插入等操作的时间复杂度是 `O(1)`，不需要移动元素，但是因为元素的不连续存储，只能遍历整个链表才能查询到元素，所以查询时间复杂度是`O(1)`

## 跳表
| 操作   | 时间复杂度 | 空间复杂度 |
| ------ | :--------: | :--------: |
| lookup |  O(logn)   |    O(n)    |
为了给链表的查询加速，从而设计了跳表。  
思想：升维 + 以空间换时间  
在链表的基础上增加索引，可以增加多级索引。每一个结点的后继不一定只指向下一个，可以是指向下下个，跳着指向。第一级索引指向下下个，第二级索引指向下下下个，依次类推。

## 栈
| 操作   | 时间复杂度 |
| ------ | :--------: |
| lookup |    O(n)    |
| insert |    O(1)    |
| delete |    O(1)    |
特点：先进后出

## 队列
特点：先进先出
双端队列 队头和队尾都可以进行入队和出队操作
优先级队列 按照元素优先级进行出队
| 操作   | 时间复杂度 |
| ------ | :--------: |
| search |    O(n)    |
| insert |    O(1)    |
| delete |    O(1)    |

## 用 `addFirst` 或`addLast`改写`Deque`代码
```java
Deque<String> deque = new LinkedList<String>();

deque.addFirst("a");
deque.addFirst("b");
deque.addFirst("c");

String str = deque.peek();
System.out.println(str);
System.out.println(deque);

while (deque.size() > 0) {
  System.out.println(deque.pop());
}
System.out.println(deque);
```

## `Queue` 源码分析
在 `Java`中`Queue`是接口形式存在的，继承自`Collection`，`LinkedList`实现了`Queue`接口中的方法。
| 操作             | 失败时抛出异常 | 失败时返回特殊值 |
| ---------------- | :------------: | :--------------: |
| 队列尾部添加元素 |    add(E e)    |    offer(E e)    |
| 队列头部删除元素 |    remove()    |      poll()      |
| 查看队列头部元素 |   element()    |      peek()      |

## `PriorityQueue` 源码分析
基于堆这种数据结构实现的，堆分为大根堆和小根堆，大根堆就是子节点小于根节点，小根堆就是子节点大于根节点。`Java` 实现的默认为我们创建了大小为 11 的数组，你也可以指定队列大小。  
### 插入队列
`boolean add(E e)` 源码中 `add()` 方法调用的是 `offer()` 方法，首先插入元素为 `null`，会报空指针异常，然后`modCount++`，如果大小超过队列的长度，会进行扩容操作，否则大小加 1，如果队列为空，直接给第一个元素赋值，否则调用`siftUp()`，判断`comparator`是否为空，为空调用`siftUpComparable()`，不为空调用`siftUpUsingComparator`，这两个方法目前为止还没看懂，先留下坑，待填。