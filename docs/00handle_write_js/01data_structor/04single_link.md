---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 4.单向链表
order: 4
---
# 🍑 四、单向链表
## 1.理论知识
单向链表（Singly Linked List）是一种常见的链式存储结构，它由一系列节点（Node）组成，每个节点包含两部分：数据部分和指针部分。数据部分用来存储节点的值，指针部分指向下一个节点，实现节点之间的连接。
### 基本操作：

-   `append(element)`：向列表尾部添加一个新的项
-   `insert(position, element)`：向列表的特定位置插入一个新的项。
-   `remove(element)`：从列表中移除一项。
-   `indexOf(element)`：返回元素在列表中的索引。如果列表中没有该元素则返回`-1`。
-   `removeAt(position)`：从列表的特定位置移除一项。
-   `isEmpty()`：如果链表中不包含任何元素，返回`true`，如果链表长度大于0则返回`false`。
-   `size()`：返回链表包含的元素个数。与数组的`length`属性类似。
-   `toString()`：由于列表项使用了`Node`类，就需要重写继承自JavaScript对象默认的`toString`方法，让其只输出元素的值。


### 特点：

1.  **动态性**：链表的长度可以动态变化，不像数组有固定的长度限制。
1.  **插入和删除高效**：在已知节点的情况下，插入和删除操作的时间复杂度为 O(1)。
1.  **空间利用率低**：链表的每个节点需要额外的指针空间来存储下一个节点的地址，会占用一定的空间。
1.  **访问效率低**：访问链表中的任意节点需要从头开始遍历，时间复杂度为 O(n)。

### 实现方式：

单向链表可以通过节点的结构来实现，每个节点包含一个数据域和一个指针域，指针指向下一个节点。链表的头部可以用一个指针来表示。

### 应用场景：

1.  **LRU缓存**：使用链表实现LRU缓存淘汰算法中的数据存储结构。
1.  **编辑器的撤销功能**：编辑器中的撤销功能可以使用链表来保存编辑操作的历史记录。
1.  **图的邻接表**：图的邻接表表示中，每个顶点的邻接点可以用链表来表示。

## 2.优缺点
### 优点：

1.  **动态性**：链表的长度可以动态变化，不像数组有固定的长度限制。
1.  **插入和删除高效**：在已知节点的情况下，插入和删除操作的时间复杂度为 O(1)。
1.  **不需要移动元素**：与数组相比，删除和插入元素时无需移动其他元素，操作简单高效。
1.  **存储空间不浪费**：链表在插入和删除元素时，不会浪费额外的存储空间。

### 缺点：

1.  **访问效率低**：访问链表中的任意节点需要从头开始遍历，时间复杂度为 O(n)。
1.  **空间复杂度高**：每个节点需要额外的指针空间来存储下一个节点的地址，会占用一定的空间。
1.  **不支持随机访问**：链表不支持像数组那样通过索引直接访问元素，需要从头开始逐个访问。
1.  **缓存不友好**：由于访问效率低，对于需要频繁访问的数据，使用链表存储会导致缓存命中率降低。

## 3.数组&链表对比
数组和链表是两种常见的数据结构，它们在存储和访问数据时有着不同的特点和适用场景：
-   数组:
    -   优点:
        -   提供了便利的[]语法来访问元素。
        -   内存连续，访问速度快。
    -   缺点:
        -   大小固定，需要扩容时需申请新内存并复制元素。
        -   插入和删除元素时需要移动其他元素。
-   链表:
    -   优点:
        -   内存不连续，灵活利用内存空间。
        -   大小动态，无需预先分配内存。
        -   插入和删除元素时间复杂度为 O(1)，效率高。
    -   缺点:
        -   访问任意位置元素需从头开始遍历。
        -   无法直接通过下标访问元素，需要遍历查找。

数组适合元素访问频繁、大小固定的场景；而链表适合大小不固定、插入和删除操作频繁的场景。

## 4.实现单向链表结构
### 1.定义链表类&节点结构

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/5c665a98aa47466e88bc61f0a078c775~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)
```js
class Node {
  // 数据
  elem;
  // 下一个节点指针
  next;
  constructor(elem) {
    this.elem = elem;
    this.next = null;
  }
}

class LinkedList {
  // 头指针
  head = null;
  length = 0;
}
```

### 2.`append`尾部追加数据
尾部增加共两种情况，如下：
-   链表本身为空, 新添加的数据时唯一的节点.
-   链表不为空, 需要向其他节点后面追加节点.

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/bcea1a7d1cdb415eb71dd323073159b6~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)
```js
 // 队尾增加方法
  append(elem) {
    // 根据传入的elem创建节点
    const newNode = new Node(elem);
    // 判断是否为空链表
    if (this.head === null) {
      this.head = newNode;
    } else {
      // 找到最后一个节点的位置
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
    // 链表长度加1
    this.length++;
  }
```

### 3.`toString`方法
从头节点开始遍历节点，然后拼接成字符串。

```js
 toString() {
    let current = this.head;
    let listString = "";
    while (current) {
      listString += "," + current.elem;
      current = current.next;
    }
    return listString.slice(1);
  }
```

### 4.`insert(position, element)`任意位置插入
插入位置可以分为三种，我们使用的是没有虚拟头节点的链表，所以需要特殊处理头部位置插入，另外两种可以合并为一种。因为是但链表，所以我们需要两个指针定位节点。
+ 头部位置插入

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/896b2e9ad87847b5aebafb998b1d0347~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)
+ 中间位置插入

![image-20240615205441109](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/image-20240615205441109.png)

+ 尾部位置插入


![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/417836cf474e4f0b86df3bec066b3e9c~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

```js
// 任意位置增加: 需要两个指针一个计数器
  insert(position, element) {
    if (position < 0 || position > this.length) return false;
    const newNode = new Node(element);
    let current = this.head;
    let preview = null;
    // 计数器
    let index = 0;
    if (position === 0) {
      newNode.next = current;
      this.head = newNode;
    } else {
      // 查找节点位置
      while (index++ < position) {
        preview = current;
        current = current.next;
      }
      // 插入节点
      preview.next = newNode;
      newNode.next = current;
    }
    // 链表长度+1
    this.length++;
    return true;
  }
```

### 5.`removeAt(position)`根据位置删除元素
删除也是三种情况，头部，尾部、中间位置

+ 移除头部元素

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/387391903f384a2a810735f989b48e78~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 移除中间元素

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/985f0320ee344b0e9f1fa6c62286c224~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 移除尾部元素

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/4f280cb9fcd2489dbc0550a9e2ef6d5c~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

```js
// 任意位置删除: 需要两个指针一个计数器
  removeAt(position) {
    // 下标从0开始
    if (position < 0 || position >= this.length) return null;

    let current = this.head;
    let previous = null;
    let index = 0;
    if (position === 0) {
      this.head = current.next;
    } else {
      while (index++ < position) {
        previous = current;
        current = current.next;
      }
      previous.next = current.next;
    }
    this.length--;
    return current.elem;
  }
```
### 6.`indexOf`获取元素位置
遍历查找判断就行了
```js
// 获取元素位置: 需要一个计数器，从头结点开始找
  indexOf(elem) {
    let current = this.head;
    let index = 0;
    while (current) {
      if (current.elem === elem) return index;
      index++;
      current = current.next;
    }
    return -1;
  }
```
### 7.`remove`根据元素删除
```js
remove(elem) {
    const index = this.indexOf(elem);
    return this.removeAt(index);
}
```
### 8.其他方法
```js
isEmpty() {
    return this.length === 0;
}

size() {
    return this.length;
}

getFirst() {
    return this.head.elem;
}
```

### 完整代码

```js
class LinkedList {
  head = null;
  length = 0;

  // 队尾增加方法
  append(elem) {
    const newNode = new Node(elem);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
    this.length++;
  }

  // 任意位置增加: 需要两个指针一个计数器
  insert(position, element) {
    if (position < 0 || position > this.length) return false;
    const newNode = new Node(element);
    let current = this.head;
    let preview = null;
    // 计数器
    let index = 0;
    if (position === 0) {
      newNode.next = current;
      this.head = newNode;
    } else {
      while (index++ < position) {
        preview = current;
        current = current.next;
      }

      preview.next = newNode;
      newNode.next = current;
    }
    this.length++;
    return true;
  }

  // 任意位置删除: 需要两个指针一个计数器
  removeAt(position) {
    // 下标从0开始
    if (position < 0 || position >= this.length) return null;

    let current = this.head;
    let previous = null;
    let index = 0;
    if (position === 0) {
      this.head = current.next;
    } else {
      while (index++ < position) {
        previous = current;
        current = current.next;
      }
      previous.next = current.next;
    }
    this.length--;
    return current.elem;
  }

  // 获取元素位置: 需要一个计数器，从头结点开始找
  indexOf(elem) {
    let current = this.head;
    let index = 0;
    while (current) {
      if (current.elem === elem) return index;
      index++;
      current = current.next;
    }
    return -1;
  }

  // 根据元素删除
  remove(elem) {
    const index = this.indexOf(elem);
    return this.removeAt(index);
  }

  isEmpty() {
    return this.length === 0;
  }

  size() {
    return this.length;
  }

  getFirst() {
    return this.head.elem;
  }

  toString() {
    let current = this.head;
    let listString = "";
    while (current) {
      listString += "," + current.elem;
      current = current.next;
    }
    return listString.slice(1);
  }
}

class Node {
  elem;
  next;
  constructor(elem) {
    this.elem = elem;
    this.next = null;
  }
}

// 测试链表
// 1.创建链表
const list = new LinkedList();

// 2.追加元素
list.append(15);
list.append(10);
list.append(20);
console.log(list.toString());

list.insert(0, 100);
list.insert(4, 200);
list.insert(2, 300);

// 3.打印链表的结果
console.log(list.toString());

// 5.测试removeAt方法
list.removeAt(0);
list.removeAt(1);
list.removeAt(3);

// 3.打印链表的结果
console.log(list.toString());

// 6.测试indexOf方法
console.log("✅ ~ list.indexOf(15):", list.indexOf(15)); // 0
console.log("✅ ~ list.indexOf(10) :", list.indexOf(10)); // 1
console.log("✅ ~ list.indexOf(20):", list.indexOf(20)); // 2
console.log("✅ ~ list.indexOf(100):", list.indexOf(100)); // -1

list.remove(15);
// 3.打印链表的结果
console.log(list.toString());

console.log("✅ ~ list.isEmpty():", list.isEmpty());
console.log("✅ ~ list.size():", list.size());
console.log("✅ ~ list.getFirst():", list.getFirst());

```
