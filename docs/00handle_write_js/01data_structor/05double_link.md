---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 5.双向链表
order: 5
---
# 🍐 五、双向链表

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/18e10d687ef04ade9fcf729627cc3bda~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)
## 1.理论知识
双向链表（Doubly Linked List），每个节点除了包含指向下一个节点的指针外，还包含指向前一个节点的指针。这使得双向链表可以从任一端开始遍历，并且在插入和删除节点时更加灵活。双向链表跟单向链表是类似的，只是需要维护两个指针域。
### 基本操作：
跟单链表一致，增加如下方法：

+ `forwardString`: 正向遍历转成字符串的方法
+ `reverseString`: 反向遍历转成字符串的方法

### 特点：

1.  **双向遍历**：双向链表可以从前向后或从后向前遍历。
1.  **插入和删除高效**：在已知节点的情况下，插入和删除操作的时间复杂度为 O(1)。
1.  **占用额外空间**：每个节点需要额外的指针空间来存储前一个节点的地址，会占用一定的空间。
1.  **实现简单**：相对于单向链表，双向链表在插入和删除节点时不需要修改前一个节点的指针，实现更加简单。

### 实现方式：

双向链表的节点结构包含三个部分：数据域、指向前一个节点的指针和指向后一个节点的指针。链表的头部和尾部分别用一个指针来表示。

### 应用场景：

1.  **LRU缓存**：双向链表常用于LRU缓存淘汰算法中的数据存储结构。
1.  **编辑器的撤销功能**：编辑器中的撤销功能可以使用双向链表来保存编辑操作的历史记录。
1.  **双向队列**：双向链表可以用于实现双向队列，支持在队头和队尾进行插入和删除操作。

## 2.优缺点
### 优点：

1.  **双向遍历**：可以从前向后或从后向前遍历，灵活性高。
1.  **插入和删除高效**：在已知节点的情况下，插入和删除操作的时间复杂度为 O(1)。
1.  **删除操作更方便**：相对于单向链表，删除节点时无需遍历查找前一个节点，实现更加简单。
1.  **支持反向查找**：可以从后向前查找节点，某些场景下可以提高效率。

### 缺点：

1.  **占用额外空间**：每个节点需要额外的指针空间来存储前一个节点的地址，增加了内存开销。
1.  **实现复杂度高**：相对于单向链表，双向链表的实现稍显复杂，需要额外考虑前一个节点的指针。

## 3.单链表&双链表对比
1.  **插入和删除操作**：

    -   单链表：插入和删除节点时，需要修改前一个节点的指针指向新节点或删除节点的下一个节点，操作稍显复杂。
    -   双链表：插入和删除节点时，不仅需要修改前一个节点的指针，还需要修改后一个节点的前向指针，但删除节点的操作相对更简单。

1.  **访问效率**：

    -   单链表：访问任意位置的节点时，需要从头开始逐个遍历，时间复杂度为 O(n)。
    -   双链表：可以从前向后或从后向前遍历，访问效率更高，但需要额外的空间存储前一个节点的指针。

1.  **空间复杂度**：

    -   单链表和双链表在存储同样数量的节点时，双链表需要更多的存储空间，因为每个节点多了一个指向前一个节点的指针。

## 4.实现双链表结构
### 1.定义双链表类&节点类
```js
class DbLinkedList {
  length = 0;
  // 头结点
  head = null;
  // 尾结点
  tail = null;
}

class MyNode {
  elem;
  // 上一个节点指针
  pre;
  // 下一个节点指针
  next;
  constructor(elem) {
    this.elem = elem;
    this.pre = null;
    this.next = null;
  }
}
```
### 2.`append`尾部追加数据
+ 链表为空

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/5dfde4ecf9014a75b4c215f63b28b398~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 链表不为空，插入在中间、插入在尾部

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/bb1d1fd512df44929e813dad44982b8b~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)
![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/42e34b176cda4615a727e6c9f6273032~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

```js
append(elem) {
    const newNode = new MyNode(elem);
    if (this.head === null) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      // 连接节点
      this.tail.next = newNode;
      // 处理pre指针
      newNode.pre = this.tail;
      // 将tail移动到新增的节点
      this.tail = newNode;
      // 置空next
      this.tail.next = null;
    }
    this.length++;
  }
```

### 3.`forwordString`正向遍历
```js
// 正向遍历转成字符串的方法
  forwardString() {
    let current = this.head;
    let resultStr = "";
    while (current) {
      resultStr += "," + current.elem;
      // 这里指针是next
      current = current.next;
    }
    return resultStr.slice(1);
  }
```
### 4.`reverseString`反向遍历
```js
// 反向遍历转成字符串的方法
  reverseString() {
    let current = this.tail;
    let resultStr = "";
    while (current) {
      resultStr += "," + current.elem;
      // 注意这里指针是pre
      current = current.pre;
    }
    return resultStr.slice(1);
  }
```
### 5.`toString`
```js
// 正向遍历转成字符串的方法
  toString() {
    this.forwardString();
  }
```

### 6.`insert`任意位置插入
+ 头部插入的两种情况

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/945547f3604d4726ac47705e381a02e8~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 插入到尾部，为空上面头部的时候已经判断过了，这里直接插入

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/d067b7269c6d49a6bd807a1b5aff7aa6~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 插入到中间

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/aad5fc887911439cb6073a894ab30ece~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

```js
// 任意位置插入
  insert(position, element) {
    if (position < 0 || position > this.length) return false;
    const newNode = new MyNode(element);

    if (position === 0) {
      if (this.head === null) {
        this.head = newNode;
        this.tail = newNode;
      } else {
        // 连接新节点
        this.head.pre = newNode;
        newNode.next = this.head;
        // 移动头指针到新节点
        this.head = newNode;
      }
    } else if (position === this.length) {
      // 连接节点
      this.tail.next = newNode;
      newNode.pre = this.tail;
      // 移动指针tail到新节点
      this.tail = newNode;
    } else {
      let index = 0;
      let current = this.head;
      let preview = null;

      while (index++ < position) {
        preview = current;
        current = current.next;
      }

      // 连接前面两个指针
      current.pre.next = newNode;
      newNode.pre = current.pre;

      // 连接后面两个指针
      newNode.next = current;
      current.pre = newNode;
    }
    this.length++;
    return true;
  }
```

### 7.`removeAt`指定位置移除
+ 删除头结点，两种情况

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/0a2db635608e4f09b062b77eb9757e92~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 删除尾结点

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/21af029894c04267baf9d4e67f5f5b9d~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 删除中间的节点


![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/84e45a98f9c74f30a23171fe7e4ca63a~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

```js
//任意位置移除
  removeAt(position) {
    if (position < 0 || position >= this.length || this.length === 0)
      return null;

    let current = this.head;
    if (position === 0) {
      if (this.length === 1) {
        this.head = null;
        this.tail = null;
      } else {
        // 先移动指针到下一个为止
        this.head = this.head.next;
        // 断开前一个的指针
        this.head.pre.next = null;
        this.head.pre = null;
      }
    } else if (position === this.length - 1) {
      current = this.tail;
      // 先断开前一个指针的next，这样还可以通过pre找到
      this.tail.pre.next = null;
      // 移动到前一个
      this.tail = this.tail.pre;
      // 断开next
      this.tail.next = null;
    } else {
      let index = 0;
      let previous = null;
      while (index++ < position) {
        previous = current;
        current = current.next;
      }
      // 断开current
      current.pre.next = current.next;
      current.next.pre = current.pre;
    }
    this.length--;
    return current.elem;
  }

```

### 8.`indexOf`获取元素位置
```js
// 获取元素位置
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
### 9.`remove`删除指定元素
```js
// 根据元素删除
  remove(element) {
    const index = this.indexOf(element);
    return this.removeAt(index);
  }
```

### 10.其他方法
```js
// 判断是否为空
  isEmpty() {
    return this.length === 0;
  }

  // 获取链表长度
  size() {
    return this.length;
  }

  // 获取第一个元素
  getHead() {
    return this.head.elem;
  }

  // 获取最后一个元素
  getTail() {
    return this.tail.elem;
  }
```
### 11.完整代码
```js
class DbLinkedList {
  length = 0;
  head = null;
  tail = null;

  append(elem) {
    const newNode = new MyNode(elem);
    if (this.head === null) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      // 连接节点
      this.tail.next = newNode;
      // 处理pre指针
      newNode.pre = this.tail;
      // 将tail移动到新增的节点
      this.tail = newNode;
      // 置空next
      this.tail.next = null;
    }
    this.length++;
  }

  // 正向遍历转成字符串的方法
  forwardString() {
    let current = this.head;
    let resultStr = "";
    while (current) {
      resultStr += "," + current.elem;
      current = current.next;
    }
    return resultStr.slice(1);
  }
  // 反向遍历转成字符串的方法
  reverseString() {
    let current = this.tail;
    let resultStr = "";
    while (current) {
      resultStr += "," + current.elem;
      current = current.pre;
    }
    return resultStr.slice(1);
  }
  // 正向遍历转成字符串的方法
  toString() {
    this.forwardString();
  }

  // 任意位置插入
  insert(position, element) {
    if (position < 0 || position > this.length) return false;
    const newNode = new MyNode(element);

    if (position === 0) {
      if (this.head === null) {
        this.head = newNode;
        this.tail = newNode;
      } else {
        // 连接新节点
        this.head.pre = newNode;
        newNode.next = this.head;
        // 移动头指针到新节点
        this.head = newNode;
      }
    } else if (position === this.length) {
      // 连接节点
      this.tail.next = newNode;
      newNode.pre = this.tail;
      // 移动指针tail到新节点
      this.tail = newNode;
    } else {
      let index = 0;
      let current = this.head;
      let preview = null;

      while (index++ < position) {
        preview = current;
        current = current.next;
      }

      // 连接前面两个指针
      current.pre.next = newNode;
      newNode.pre = current.pre;

      // 连接后面两个指针
      newNode.next = current;
      current.pre = newNode;
    }
    this.length++;
    return true;
  }

  //任意位置移除
  removeAt(position) {
    if (position < 0 || position >= this.length || this.length === 0)
      return null;

    let current = this.head;
    if (position === 0) {
      if (this.length === 1) {
        this.head = null;
        this.tail = null;
      } else {
        // 先移动指针到下一个为止
        this.head = this.head.next;
        // 断开前一个的指针
        this.head.pre.next = null;
        this.head.pre = null;
      }
    } else if (position === this.length - 1) {
      current = this.tail;
      // 先断开前一个指针的next，这样还可以通过pre找到
      this.tail.pre.next = null;
      // 移动到前一个
      this.tail = this.tail.pre;
      // 断开next
      this.tail.next = null;
    } else {
      let index = 0;
      let previous = null;
      while (index++ < position) {
        previous = current;
        current = current.next;
      }
      // 断开current
      current.pre.next = current.next;
      current.next.pre = current.pre;
    }
    this.length--;
    return current.elem;
  }

  // 获取元素位置
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
  remove(element) {
    const index = this.indexOf(element);
    return this.removeAt(index);
  }

  // 判断是否为空
  isEmpty() {
    return this.length === 0;
  }

  // 获取链表长度
  size() {
    return this.length;
  }

  // 获取第一个元素
  getHead() {
    return this.head.elem;
  }

  // 获取最后一个元素
  getTail() {
    return this.tail.elem;
  }
}

class MyNode {
  elem;
  pre;
  next;
  constructor(elem) {
    this.elem = elem;
    this.pre = null;
    this.next = null;
  }
}

// 1.创建双向链表对象
const DBLink = new DbLinkedList();

// 2.追加元素
DBLink.append("abc");
DBLink.append("cba");
DBLink.append("nba");
DBLink.append("mba");

// 3.获取所有的遍历结果
// console.log("✅ ~ DBLink.forwardString():", DBLink.forwardString());
// console.log("✅ ~ DBLink.reverseString():", DBLink.reverseString());
// console.log("✅ ~ DBLink:", DBLink);

// 4.insert方法测试
DBLink.insert(0, "100");
DBLink.insert(2, "200");
DBLink.insert(6, "300");
console.log("✅ ~ DBLink.forwardString():", DBLink.forwardString());

// 5.removeAt方法测试
console.log("✅ ~ DBLink.removeAt(0):", DBLink.removeAt(0));
console.log("✅ ~ DBLink.removeAt(1):", DBLink.removeAt(1));
console.log("✅ ~ DBLink.removeAt(4):", DBLink.removeAt(4));

```
