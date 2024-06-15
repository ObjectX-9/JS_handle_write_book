---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 2.栈
order: 2
---

# 🍒 二、栈
## 1.理论知识
栈（Stack）是一种基于先进后出（LIFO，Last In First Out）原则的数据结构，类比为堆放盘子。在栈中，元素的添加和删除操作都发生在同一端，这一端被称为栈顶，另一端被称为栈底。

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/da3bb27863a24677b7ffa01933730d5f~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

### 基本操作：

1.  **压栈（Push）** ：向栈顶添加元素。
1.  **出栈（Pop）** ：从栈顶移除元素。
1.  **查看栈顶元素（peek）** ：查看栈顶元素，但不移除。
1.  **判空（isEmpty）** ：检查栈是否为空。
2.  **清空栈元素（clear）**：移除栈里的所有元素。
3.  **获取栈大小（Size）** ：获取栈中元素的数量。

### 应用场景：

1.  **函数调用栈**：用于保存函数调用过程中的局部变量和返回地址。
1.  **表达式求值**：将中缀表达式转换为后缀表达式并计算。
1.  **浏览器历史记录**：浏览器使用栈来存储访问过的页面，可以通过后退按钮回到上一个页面。
1.  **撤销操作**：编辑器和图形软件使用栈来实现撤销操作。

### 实现方式：

1.  **数组实现**：使用数组来存储栈中的元素，栈顶对应数组的末尾。
1.  **链表实现**：使用链表来存储栈中的元素，每个节点包含一个元素和指向下一个节点的指针。

### 时间复杂度：

1.  压栈、出栈、查看栈顶元素的时间复杂度为 O(1)。
1.  判空和获取栈大小的时间复杂度为 O(1)。

## 2.优缺点
### 优点：

1.  **简单高效**：栈的操作简单明了，压栈、出栈等操作时间复杂度都是 O(1)，效率高。
1.  **内存管理**：栈内存管理由系统自动处理，无需手动分配和释放内存，减少内存泄漏的风险。
1.  **函数调用**：函数调用时使用栈来保存局部变量和返回地址，方便实现递归和函数嵌套。
1.  **逆序输出**：逆序输出数据时，栈可以提供一种简单的解决方案。

### 缺点：

1.  **容量限制**：栈的大小在创建时固定，无法动态扩展，可能会导致栈溢出。
1.  **局限性**：栈只能在栈顶进行操作，限制了一些数据结构的操作，如队列的快速插入和删除。
1.  **不灵活**：由于栈的特性，一些场景下可能需要额外的数据结构来实现更复杂的功能，增加了复杂性和内存消耗。

## 3.实现栈结构
这里通过数组来实现，当然你也可以用链表来实现，思路是一致的，需要关注的地方在注释中。
```js
/**
 * 以数组尾部作为栈顶
 */
class BaseStack {
  stackData = [];

  initStackByArr(arr) {
    this.stackData = arr;
  }

  push(elem) {
    this.stackData.push(elem);
  }

  pop() {
    const elem = this.stackData.pop();
    return elem;
  }

  peek() {
    return this.stackData[this.stackData.length - 1];
  }

  isEmpty() {
    return this.stackData.length === 0;
  }

  size() {
    return this.stackData.length;
  }

  printf() {
    console.log(this.stackData);
  }
}

const stack = new BaseStack();
// 情况下代码模拟
stack.push(6);
stack.push(5);
stack.printf();
stack.pop(); // 5
stack.printf();
stack.push(4);
stack.printf();
stack.pop(); // 4
stack.push(3);
stack.printf();
stack.pop(); // 3
stack.pop(); // 6
stack.push(2);
stack.push(1);
stack.printf();
stack.pop(); // 1
stack.pop(); // 2

stack.printf();

```
