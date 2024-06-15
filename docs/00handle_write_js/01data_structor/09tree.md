---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 9.树
order: 9
---
# 一、树的基本概念
## 1.树的定义
树（`Tree`）: `n（n≥0）`个结点构成的有限集合。
1.  **树(Tree)** ：树是一种非线性数据结构，由节点组成，每个节点可以有零个或多个子节点。其中有一个特殊的节点被称为根节点，其他节点可以分为若干个不相交的子树。树是一种层次结构，常用于表示具有层次关系的数据，如组织结构、文件系统等。
1.  **二叉树(Binary Tree)** ：二叉树是一种特殊的树结构，每个节点最多有两个子节点，分别称为左子节点和右子节点。二叉树常用于实现一些高效的算法，如二叉搜索树等。
1.  **二叉搜索树(Binary Search Tree)** ：二叉搜索树是一种二叉树，其每个节点的值大于其左子树的所有节点的值，小于其右子树的所有节点的值。这种特性使得在二叉搜索树中进行查找、插入和删除操作更加高效。

## 2.树的术语
树结构中常用的术语包括：
1.  **根节点(Root)** ：树的顶层节点，是树结构中的起始节点，其他节点都通过路径与根节点相连。
1.  **父节点(Parent)** ：一个节点的直接上级节点称为其父节点，即与该节点相连的节点。
1.  **子节点(Children)** ：一个节点的直接下级节点称为其子节点，即被该节点所连接的节点。
1.  **兄弟节点(Siblings)** ：有着相同父节点的节点之间称为兄弟节点。
1.  **叶子节点(Leaf Node)** ：没有子节点的节点称为叶子节点（外部节点）。
1.  **内部节点(Internal Node)** ：除了叶子节点以外的所有节点称为内部节点。
1.  **深度(Depth)** ：从根节点到某个节点所经历的边的数量，根节点的深度为零。
1.  **高度(Height)** ：从某个节点到其子树中最远的叶子节点的路径的边数，叶子节点的高度为零。
1.  **子树(Subtree)** ：树中的任意节点和其所有后代节点构成的子树。
1.  **祖先(Ancestor)** ：某个节点向根节点方向的路径上的所有节点是该节点的祖先节点。
1.  **后代(Descendant)** ：某个节点向叶子节点方向的路径上的所有节点是该节点的后代节点。
1.  **度(Degree)** ：一个节点拥有的子节点的数量称为该节点的度。
1.  **层级(Level)** ：根节点在第一层，根的直接子节点在第二层，以此类推，节点的层级即为其深度加一。
1.  **路径(Path)** ：从一个节点到另一个节点的一系列边组成的序列称为路径。
1.  **子树排序(Subtree Ordering)** ：对节点的子树进行排序，常见的包括前序遍历、中序遍历、后序遍历。
## 3.树的表示
### 最普通的表示方式
简单代码示例
```js
// 树节点结构
class BinarySearchTree {
  root;
  constructor(key) {
    this.root = null;
  }
}

class Node {
  left;
  right;
  ...其他指针
  key;
  constructor(key) {
    this.key = key;
    this.left = null;
    this.right = null;
    ...其他指针
  }
}

// 实际树结构
const bst = new BinarySearchTree();
bst.root = new Node(A);
cons root = bst.root;
root.leftChild = new Node(B);
root.rightChild = new Node(D);
...其他指针
```

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/5d4f97f8a615465f8a7a43ed029fc173~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)


### 儿子-兄弟表示法
```js
// 树节点结构
class BinarySearchTree {
  root;
  constructor(key) {
    this.root = null;
  }
}

class Node {
  child;
  nextSibling;
  key;
  constructor(key) {
    this.key = key;
    this.child = null;
    this.nextSibling = null;
  }
}

// 实际树结构
const bst = new BinarySearchTree();
bst.root = new Node(A);
const root = bst.root;
root.child = new Node(B);
root.child.nextSibling = new Node(C);
root.child.nextSibling.nextSibling = new Node(D);
...
```

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/bf90f6ba66e446e3897f03665a5644b2~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

### 儿子-兄弟表示法旋转
跟二叉树的结构一致，只有左右两个子针
```js
// 树节点结构
class BinarySearchTree {
  root;
  constructor(key) {
    this.root = null;
  }
}

class Node {
  left;
  right;
  key;
  constructor(key) {
    this.key = key;
    this.left = null;
    this.right = null;
  }
}

// 实际树结构
const bst = new BinarySearchTree();
bst.root = new Node(A);
cons root = bst.root;
root.leftChild = new Node(B);
root.rightChild = new Node(D);
```
旋转后，就跟二叉树类似
![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/f2a7b325813b45e583c28f055fe4c280~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)


### 结论
-   所有的树本质上都可以使用二叉树模拟出来.

# 二、二叉树
如果树中每个节点最多只能有两个子节点, 这样的树就称为"二叉树".
## 1.二叉树的定义
二叉树中每个节点最多有两个子节点，通常称为左孩子和右孩子。下面是二叉树的形式定义：

**二叉树** 是一种层次结构，包含一组节点，这些节点最多有两个子节点，分别称为左孩子和右孩子。二叉树具有以下特点：

1.  每个节点最多有两个子节点，左子节点和右子节点。
1.  每个节点本身也是一棵二叉树，即子树也是二叉树。
1.  不存在重复节点。

二叉树的节点结构通常包括一个数据域和两个指针域（左孩子指针和右孩子指针），用于指向节点的左孩子和右孩子。二叉树可以是空树（没有节点），也可以是由根节点及其左右子树组成的树。

根据节点的子节点关系，二叉树可以分为多种类型，如满二叉树、完全二叉树、平衡二叉树等。在算法和数据结构中，二叉树具有广泛的应用，例如二叉搜索树、AVL树、红黑树等都是基于二叉树结构而衍生出的数据结构，用于高效地进行数据管理和搜索操作。

二叉树有五种形态:
-   因为二叉树是有左右之分的.

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/dc314844a593470bac1dad575e6c20ec~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

## 2.二叉树的特性
+ 一个二叉树第 i 层的最大结点数为：`2^(i-1), i >= 1`;

+ 深度为k的二叉树有最大结点总数为： `2^k - 1, k >= 1`;

+ 对任何非空二叉树 T，若n0表示叶结点的个数、n2是度为2的非叶结点个数，那么两者满足关系`n0 = n2 + 1`。


![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/058e0e8cb25249799a2652bf3cd0c3f1~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)


## 3.二叉树特性推导
### 特性1：一个二叉树第 i 层的最大结点数为：`2^(i-1), i >= 1`;

二叉树是每个节点最多有两个子节点的树结构，通常被称作左子节点和右子节点。在二叉树的第 i 层（根节点为第一层），每一层的最大节点数可以递归地定义为上一层节点数的两倍。这是因为在完美二叉树（Perfect Binary Tree）中，每个节点都有两个子节点。

我们可以用数学归纳法来推理：

0.  基础情况： 当 i = 1 时，即树的第一层，只有根节点。因此，第一层的最大结点数为 1，这也符合 `2^(1-1) = 2^0 = 1`。
0.  归纳假设： 假设在第 k 层（其中 k >= 1），最大结点数为 `2^(k-1)`。
0.  归纳步骤： 接下来需要证明在第 k+1 层，最大结点数为 `2^k`。

由于二叉树的定义，每个节点最多有两个子节点，那么如果第 k 层已经达到最大结点数 `2^(k-1)`，那么第 k+1 层每个节点都会有两个子节点。因此，第 k+1 层的最大结点数将是第 k 层的两倍。

我们将第 k 层的最大结点数乘以 2 ，得到第 k+1 层的最大节点数：

```
2 * (最大结点数在第 k 层) = 2 * 2^(k-1) = 2^1 * 2^(k-1) = 2^(k+1-1) = 2^k
```

因此，第 k+1 层的最大结点数确实是 `2^k`。

所以，根据这个归纳步骤，我们可以证明对任何 i >= 1，第 i 层的最大结点数都是 `2^(i-1)`。这正是我们要证明的结果。
### 特性2：深度为k的二叉树有最大结点总数为： `2^k - 1, k >= 1`;
深度为 k 的二叉树有最大结点总数为 `2^k - 1`：

-   **基础情况：** 当 k=1 时，树只有一个结点（根节点），所以总结点数为 1，即 `2^1 - 1 = 2 - 1 = 1`，公式成立。
-   **归纳假设：** 假设对于某个正整数 n，深度为 n 的二叉树有最大结点总数为 `2^n - 1` 成立。
-   **归纳步骤：** 考虑深度为 n+1 的二叉树，**根据性质1，第 n+1 层的最大结点数为 `2^n`**。而前 n 层的最大结点总数为 `2^n - 1`。所以深度为 n+1 的二叉树的最大结点总数为 `2^n + (2^n - 1) = 2*2^n - 1 = 2^(n+1) - 1`。因此，深度为 n+1 的二叉树有最大结点总数为 `2^(n+1) - 1`，公式成立。
-   根据数学归纳法，对于所有的正整数 k，深度为 k 的二叉树有最大结点总数为 `2^k - 1`。

### 特性3：对于任何非空二叉树 T，叶结点的个数 n0 与度为 2 的非叶结点个数 n2 满足关系 `n0 = n2 + 1`
要证明对于任何非空二叉树T，n0（叶节点的个数）和n2（度数为2的非叶节点的个数）满足关系`n0 = n2 + 1`，我们可以类似地使用归纳法来推导：

在二叉树中，节点的度数指的是该节点拥有的子节点数量。除了叶节点（度数为0）和度数为2的节点，还有可能有度数为1的节点（即只有一个子节点的非叶节点）。

设n1表示度数为1的非叶节点数量，总节点数n可以表示为：

```
n = n0 + n1 + n2
```

在二叉树中，总的边数e（也就是父子关系的数目）是总节点数减1，因为除了根节点，每个节点有一个父节点：

```
e = n - 1 = n0 + n1 + n2 - 1
```

另一方面，总边数也可以根据节点的度数来计算。每个度为1的节点贡献了1条边，每个度为2的节点贡献了2条边。叶节点（度数为0）不贡献边，所以总边数也可以表示为：

```
e = n1 + 2*n2
```

由于这两种情况描述的是同一个树的总边数，它们必须相等，所以我们有：

```
n0 + n1 + n2 - 1 = n1 + 2*n2
```

整理这个等式，我们得到：

```
n0 = n2 + 1
```

这就是需要证明的关系。

另一种更直观的解释方法是：

-   树中每添加一个度为2的节点，会增加2个子节点。
-   这两个子节点中，一个会成为新的叶节点，而另一个则取代了原有的叶节点的位置。
-   因此，每次增加一个度为2的节点，叶节点的数量增加的数量总比度数为2的节点的数量多1。
-   一个只有根节点的树将会有1个叶节点（根节点本身）且没有度数为2的节点，提供了这个性质的基础情况。
-   当树逐渐增长，上述性质保持不变，因为叶节点和度数为2的节点之间总是保持n0 = n2 + 1的关系。

## 4.特殊二叉树
### 满二叉树
完美二叉树(Perfect Binary Tree) , 也称为满二叉树(Full Binary Tree）
-   在二叉树中, 除了最下一层的叶结点外, 每层节点都有2个子结点, 就构成了满二叉树.

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/e8cf061959f146539445ead047fa29b3~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

### 完全二叉树
完全二叉树(`Complete Binary Tree`)

-   除二叉树最后一层外, 其他各层的节点数都达到最大个数.
-   且最后一层从左向右的叶结点连续存在, 只缺右侧若干节点.
-   完美二叉树是特殊的完全二叉树.

下面不是完全二叉树, 因为D节点还没有右结点, 但是E节点就有了左右节点.


![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/95be58143a1c48c9856dd696247645fc~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)


## 5.二叉树的存储
-   二叉树的存储常见的方式是数组和链表.
### 1.使用数组存储
-   完全二叉树: 按从上至下、从左到右顺序存储

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/09aa091b76da456cab385d519af9799a~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

-   非完全二叉树:
    -   非完全二叉树要转成完全二叉树才可以按照上面的方案存储.
    -   但是会造成很大的空间浪费


![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/af93fc161b454a53a017d2c2a7f0982b~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

### 2.链表存储
-   二叉树最常见的方式还是使用链表存储.
-   每个结点封装成一个Node, Node中包含存储的数据, 左结点的引用, 右结点的引用.

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/46a272434057407a8f0a2813bd49e264~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

# 三、二叉树的常见方法
## 1.二叉搜索树

二叉搜索树（`BST，Binary Search Tree`），也称二叉排序树或二叉查找树

二叉搜索树是一颗二叉树, 可以为空；如果不为空，满足以下性质：

-   非空左子树的所有键值小于其根结点的键值。
-   非空右子树的所有键值大于其根结点的键值。
-   左、右子树本身也都是二叉搜索树。

下面哪些是二叉搜索树, 哪些不是?
只有没有标绿的一个是二叉搜索树

![image.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/90a001cebb464e52b06fba9ee962b401~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)


## 2.二叉搜索树的特点

二叉搜索树的特点就是相对较小的值总是保存在左结点上, 相对较大的值总是保存在右结点上.

## 3.二叉搜索树的操作

-   `insert(key)`：向树中插入一个新的键。
-   `search(key)`：在树中查找一个键，如果结点存在，则返回`true`；如果不存在，则返回`false`。
-   `inOrderTraverse`：通过中序遍历方式遍历所有结点。
-   `preOrderTraverse`：通过先序遍历方式遍历所有结点。
-   `postOrderTraverse`：通过后序遍历方式遍历所有结点。
-   `min`：返回树中最小的值/键。
-   `max`：返回树中最大的值/键。
-   `remove(key)`：从树中移除某个键。

# 四、实现二叉树
## 1.除删除外的其他全部方法
这些方式是使用递归的方式写的，都比较简单，就不解释了，我们主要解释二叉树的删除。
```js
/** 节点类：保存节点信息和指针 */
class Node {
  left;
  right;
  key;
  constructor(key) {
    this.key = key;
    this.left = null;
    this.right = null;
  }
}

/** 二叉搜索树 */
class BinarySearchTree {
  root;
  constructor(key) {
    this.root = null;
  }

  /**
   * 插入节点
   * @param {*} key
   */
  insert(key) {
    const newNode = new Node(key);
    // 如果根节点为空
    if (this.root === null) {
      this.root = newNode;
    } else {
      this.insertNode(this.root, newNode);
    }
  }

  /**
   * 插入节点的方法
   * @param {*} root
   * @param {*} newNode
   */
  insertNode(root, newNode) {
    // 如果已经有了，则禁止插入
    if (root.key === newNode.key) {
      console.log("======>该节点已经插入过了");
    } else if (root.key > newNode.key) {
      // 左侧查找
      if (root.left === null) {
        root.left = newNode;
      } else {
        this.insertNode(root.left, newNode);
      }
    } else {
      // 右侧查找
      if (root.right === null) {
        root.right = newNode;
      } else {
        this.insertNode(root.right, newNode);
      }
    }
  }

  /**
   * 先序遍历
   * @param {*} root
   * @param {*} handler
   */
  preOrderTraversal(handler) {
    this.preOrderTranversalNode(this.root, handler);
  }

  preOrderTranversalNode(root, handler) {
    // 边界判断
    if (!root) return;
    // 访问根节点
    handler(root.key);
    // 访问左子树
    this.preOrderTranversalNode(root.left, handler);
    // 访问右子树
    this.preOrderTranversalNode(root.right, handler);
  }

  /**
   * 中序遍历
   * @param {*} handler
   */
  inOrderTraversal(handler) {
    this.inOrderTraversalNode(this.root, handler);
  }

  inOrderTraversalNode(root, handler) {
    if (!root) return;
    this.inOrderTraversalNode(root.left, handler);
    handler(root.key);
    this.inOrderTraversalNode(root.right, handler);
  }

  /**
   * 后序遍历
   * @param {*} handler
   */
  postOrderTraversal(handler) {
    this.postOrderTraversalNode(this.root, handler);
  }

  postOrderTraversalNode(root, handler) {
    if (!root) return;
    this.postOrderTraversalNode(root.left, handler);
    this.postOrderTraversalNode(root.right, handler);
    handler(root.key);
  }

  min() {
    let node = this.root;
    while (node.left !== null) {
      node = node.left;
    }
    return node.key;
  }

  max() {
    let node = this.root;
    while (node.right !== null) {
      node = node.right;
    }
    return node.key;
  }

  // 递归的方式
  search(key) {
    return this.searchNode(this.root, key);
  }

  searchNode(root, key) {
    if (!root) return false;
    if (root.key < key) {
      return this.searchNode(root.right, key);
    } else if (root.key > key) {
      return this.searchNode(root.left, key);
    } else {
      return true;
    }
  }

  // 非递归的方式
  searchV2(key) {
    return this.searchNodeV2(this.root, key);
  }

  searchNodeV2(root, key) {
    if (!root) return false;
    while (root !== null) {
      if (root.key < key) {
        root = root.right;
      } else if (root.key > key) {
        root = root.left;
      } else {
        return true;
      }
    }
    return false;
  }
}

// 测试代码
const bst = new BinarySearchTree();

// 插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);

// 测试前序遍历结果
let resultString = "";
bst.preOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 先序遍历resultString:", resultString); // 11 7 5 3 6 9 8 10 15 13 12 14 20 18 25

resultString = "";
bst.inOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 中序遍历resultString:", resultString); // 3 5 6 7 8 9 10 11 12 13 14 15 18 20 25

resultString = "";
bst.postOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 后序遍历resultString:", resultString); // 3 6 5 8 10 9 7 12 14 13 18 25 20 15 11

// 获取最值
console.log("✅ ~ bst.min():", bst.min());
console.log("✅ ~ bst.max():", bst.max());

// 查找特定的值
console.log("✅ ~ bst.search(10):", bst.search(10));
console.log("✅ ~ bst.search(21):", bst.search(21));

// 查找特定的值
console.log("✅ ~ bst.searchV2(10):", bst.searchV2(10));
console.log("✅ ~ bst.searchV2(21):", bst.searchV2(21));
```
## 2.二叉树的删除
原始树
![原始树.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/8311768c1134412e8dacf7cea75dbf94~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

整体就是根据删除节点子节点的数量来分类，然后对应细分情况，维护二叉树的合理性。
### 查找要删除的节点
也没什么可说的就是二分查找的思路
```js
remove(key) {
// 当前遍历到的节点
let current = this.root;
// 当前节点的父级节点，因为需要更改父级指针
let parent = this.root;
// 记录是父级节点的左子节点还是右子节点
let isLeftChild = false;
// 查找需要删除的节点
while (current.key !== key) {
  parent = current;
  // 左子树查找
  if (key < current.key) {
    isLeftChild = true;
    current = current.left;
  } else {
    // 右子树查找
    isLeftChild = false;
    current = current.right;
  }

  if (current === null) return false;
}
```
### 情况1：无子节点
可删除的节点如下所示：
![树的删除：情况1，没有子节点：current.left === null && current.right === null.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/97a3ff4442294a09b11105546f1a8bbe~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

举例删除3节点和10节点
+ 3节点，parent的左子树
+ 10节点，parent的右子树
![情况1_ 举例删除3节点和删除10节点.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/fa3637eb16cd4a0ab39c6ea2bd548c77~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

代码如下：
```js
// 1.第一种情况，删除的是叶节点，考虑是否为根元素和非根元素两种情况
// 如果是根元素直接删除，如果不是根则根据isLeftChild，将parent的left||right置为null
if (current.left === null && current.right === null) {
  // 只有一个根元素
  if (current === this.root) {
    this.root = null;
  } else if (isLeftChild) {
    parent.left = null;
  } else {
    parent.right = null;
  }
}
```
### 情况2：有一个子节点
针对这种情况，又细分为以下四种情况
可删除节点如下所示
![树的删除：情况二，只有一个子节点，可能是右，也可能是左_ current.right === null __ current.left === null.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/9fd96c1ceed5446ab775232764fb483d~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况1：5节点：只有一个左子节点，并且是父级的左子树的情况

![5节点：只有一个左子节点，并且是父级的左子树的情况.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/7f5f45137ba84d8291808984262734db~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况2：9节点：只有一个左子节点，并且是父级的右子树的情况举例

![9节点：只有一个左子节点，并且是父级的右子树的情况举例.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/e771eb05f34d4b5a8f53611c1b4ff0c8~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况3：18节点：只有一个右子节点，并且是父级左子树的情况

![18节点：只有一个右子节点，并且是父级左子树的情况.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/e6ff9a3dc9004e0d99bbf4bfc0e71019~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况4：14节点：只有一个右子节点，并且是父级右子树的情况

![14节点：只有一个右子节点，并且是父级右子树的情况.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/3385c6b5663e4e0bbd0fcda4daf64ded~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

代码如下
```js
// 2.第二种情况，当前遍历到的节点有一个子节点，考虑current是否为根和非根两种情况
// 左子树不为null，current只有左子树，这里赋值的都是current.left;
else if (current.right === null) {
  if (current === this.root) {
    // 这里是因为右子树为null
    this.root = current.left;
  } else if (isLeftChild) {
    // 注意isLeftChild是用来决定使用的是parent的哪个指针
    parent.left = current.left;
  } else {
    parent.right = current.left;
  }
} else if (current.left === null) {
  // 右子树不为null，current只有左子树，这里赋值的都是current.left;
  if (current === this.root) {
    this.root = current.right;
  } else if (isLeftChild) {
    parent.left = current.right;
  } else {
    parent.right = current.right;
  }
}
```
### 情况3：有两个子节点
两个子节点的时候可以选择用前驱或者后继去替换被删除的节点，然后重新维护二叉树，我们这里使用后继
针对这种情况，又细分两种情况：第一种后继是直接子级，第二种后继不是直接子级【这里又有两种情况，即有无剩余节点需要处理】
可删除节点如下所示
![情况3：删除的节点有两个子节点.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/f622ebc80b014dd292dca6543b33106d~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况1：删除9节点，用10替代，这种情况替换完成后无其他多余节点
![情况1：删除9节点.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/0648d4a47a3f4e1880f7d328a73f4026~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况2：删除7节点，用8替代，也是没有多余节点
![情况2：删除7节点.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/ad029267ed4c473f84d5dadc776450aa~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

+ 情况3：删除15节点，用18替代，有多余19节点

![情况3：删除15节点.png](https://cdn.jsdelivr.net/gh/ObjectX-9/DrawingBed/imgMac/2c7e8f68602c41af936f7ca08e7e828b~tplv-k3u1fbpfcp-jj-mark%3A0%3A0%3A0%3A0%3Aq75.png)

代码如下：
```js
// 3.第三种情况，左右子树都有，这时候需要考虑使用查找前驱、后继节点来替换删除的节点
// 前驱：比current小一点点的节点, 称为current节点的前驱.
// 后继：比current大一点点的节点, 称为current节点的后继.
else {
  // 1.获取后继节点
  let successor = this.getSuccessor(current);

  // 2.判断是否是根节点
  if (current == this.root) {
    this.root = successor;
  } else if (isLeftChild) {
    parent.left = successor;
  } else {
    parent.right = successor;
  }

  // 3.将删除节点的左子树赋值给successor
  successor.left = current.left;
}

getSuccessor(delNode) {
    let parent = delNode;
    let target = delNode;
    // 从右子树开始
    let current = delNode.right;
    // 查找后继，左子树最小节点
    while (current !== null) {
      parent = target;
      target = current;
      current = current.left;
    }

    // 对于跨域层级的删除，删除7 || 15，比如删除15，就是吧19连接到20的左子节点去
    // 在这里处理的原因是因为需要后继节点的parent，也可以将parent也返回在上面的判断中去处理
    if (target != delNode.right) {
      parent.left = target.right;
      target.right = delNode.right;
    }

    return target;
}
```
# 五、完整代码
```js
/** 节点类：保存节点信息和指针 */
class Node {
  left;
  right;
  key;
  constructor(key) {
    this.key = key;
    this.left = null;
    this.right = null;
  }
}

/** 二叉搜索树 */
class BinarySearchTree {
  root;
  constructor(key) {
    this.root = null;
  }

  /**
   * 插入节点
   * @param {*} key
   */
  insert(key) {
    const newNode = new Node(key);
    // 如果根节点为空
    if (this.root === null) {
      this.root = newNode;
    } else {
      this.insertNode(this.root, newNode);
    }
  }

  /**
   * 插入节点的方法
   * @param {*} root
   * @param {*} newNode
   */
  insertNode(root, newNode) {
    // 如果已经有了，则禁止插入
    if (root.key === newNode.key) {
      console.log("======>该节点已经插入过了");
    } else if (root.key > newNode.key) {
      // 左侧查找
      if (root.left === null) {
        root.left = newNode;
      } else {
        this.insertNode(root.left, newNode);
      }
    } else {
      // 右侧查找
      if (root.right === null) {
        root.right = newNode;
      } else {
        this.insertNode(root.right, newNode);
      }
    }
  }

  /**
   * 先序遍历
   * @param {*} root
   * @param {*} handler
   */
  preOrderTraversal(handler) {
    this.preOrderTranversalNode(this.root, handler);
  }

  preOrderTranversalNode(root, handler) {
    // 边界判断
    if (!root) return;
    // 访问根节点
    handler(root.key);
    // 访问左子树
    this.preOrderTranversalNode(root.left, handler);
    // 访问右子树
    this.preOrderTranversalNode(root.right, handler);
  }

  /**
   * 中序遍历
   * @param {*} handler
   */
  inOrderTraversal(handler) {
    this.inOrderTraversalNode(this.root, handler);
  }

  inOrderTraversalNode(root, handler) {
    if (!root) return;
    this.inOrderTraversalNode(root.left, handler);
    handler(root.key);
    this.inOrderTraversalNode(root.right, handler);
  }

  /**
   * 后序遍历
   * @param {*} handler
   */
  postOrderTraversal(handler) {
    this.postOrderTraversalNode(this.root, handler);
  }

  postOrderTraversalNode(root, handler) {
    if (!root) return;
    this.postOrderTraversalNode(root.left, handler);
    this.postOrderTraversalNode(root.right, handler);
    handler(root.key);
  }

  min() {
    let node = this.root;
    while (node.left !== null) {
      node = node.left;
    }
    return node.key;
  }

  max() {
    let node = this.root;
    while (node.right !== null) {
      node = node.right;
    }
    return node.key;
  }

  // 递归的方式
  search(key) {
    return this.searchNode(this.root, key);
  }

  searchNode(root, key) {
    if (!root) return false;
    if (root.key < key) {
      return this.searchNode(root.right, key);
    } else if (root.key > key) {
      return this.searchNode(root.left, key);
    } else {
      return true;
    }
  }

  // 非递归的方式
  searchV2(key) {
    return this.searchNodeV2(this.root, key);
  }

  searchNodeV2(root, key) {
    if (!root) return false;
    while (root !== null) {
      if (root.key < key) {
        root = root.right;
      } else if (root.key > key) {
        root = root.left;
      } else {
        return true;
      }
    }
    return false;
  }

  remove(key) {
    // 当前遍历到的节点
    let current = this.root;
    // 当前节点的父级节点，因为需要更改父级指针
    let parent = this.root;
    // 记录是父级节点的左子节点还是右子节点
    let isLeftChild = false;
    // 查找需要删除的节点
    while (current.key !== key) {
      parent = current;
      // 左子树查找
      if (key < current.key) {
        isLeftChild = true;
        current = current.left;
      } else {
        // 右子树查找
        isLeftChild = false;
        current = current.right;
      }

      if (current === null) return false;
    }
    // 1.第一种情况，删除的是叶节点，考虑是否为根元素和非根元素两种情况
    // 如果是根元素直接删除，如果不是根则根据isLeftChild，将parent的left||right置为null
    if (current.left === null && current.right === null) {
      // 只有一个根元素
      if (current === this.root) {
        this.root = null;
      } else if (isLeftChild) {
        parent.left = null;
      } else {
        parent.right = null;
      }
    }
    // 2.第二种情况，当前遍历到的节点有一个子节点，考虑current是否为根和非根两种情况
    // 左子树不为null，current只有左子树，这里赋值的都是current.left;
    else if (current.right === null) {
      if (current === this.root) {
        // 这里是因为右子树为null
        this.root = current.left;
      } else if (isLeftChild) {
        // 注意isLeftChild是用来决定使用的是parent的哪个指针
        parent.left = current.left;
      } else {
        parent.right = current.left;
      }
    } else if (current.left === null) {
      // 右子树不为null，current只有左子树，这里赋值的都是current.left;
      if (current === this.root) {
        this.root = current.right;
      } else if (isLeftChild) {
        parent.left = current.right;
      } else {
        parent.right = current.right;
      }
    }

    // 3.第三种情况，左右子树都有，这时候需要考虑使用查找前驱、后继节点来替换删除的节点
    // 前驱：比current小一点点的节点, 称为current节点的前驱.
    // 后继：比current大一点点的节点, 称为current节点的后继.
    else {
      // 1.获取后继节点
      let successor = this.getSuccessor(current);

      // 2.判断是否是根节点
      if (current == this.root) {
        this.root = successor;
      } else if (isLeftChild) {
        parent.left = successor;
      } else {
        parent.right = successor;
      }

      // 3.将删除节点的左子树赋值给successor
      successor.left = current.left;
    }
    return true;
  }

  getSuccessor(delNode) {
    let parent = delNode;
    let target = delNode;
    // 从右子树开始
    let current = delNode.right;
    // 查找后继，左子树最小节点
    while (current !== null) {
      parent = target;
      target = current;
      current = current.left;
    }

    // 对于跨域层级的删除
    if (target != delNode.right) {
      parent.left = target.right;
      target.right = delNode.right;
    }

    return target;
  }
}

// 测试代码
const bst = new BinarySearchTree();

// 插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);

// 测试前序遍历结果
let resultString = "";
bst.preOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 先序遍历resultString:", resultString); // 11 7 5 3 6 9 8 10 15 13 12 14 20 18 25

resultString = "";
bst.inOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 中序遍历resultString:", resultString); // 3 5 6 7 8 9 10 11 12 13 14 15 18 20 25

resultString = "";
bst.postOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 后序遍历resultString:", resultString); // 3 6 5 8 10 9 7 12 14 13 18 25 20 15 11

// 获取最值
console.log("✅ ~ bst.min():", bst.min());
console.log("✅ ~ bst.max():", bst.max());

// 查找特定的值
console.log("✅ ~ bst.search(10):", bst.search(10));
console.log("✅ ~ bst.search(21):", bst.search(21));

// 查找特定的值
console.log("✅ ~ bst.searchV2(10):", bst.searchV2(10));
console.log("✅ ~ bst.searchV2(21):", bst.searchV2(21));

// 删除测试
console.log("✅ ~ bst.searchV2(10):", bst.remove(7));
resultString = "";
bst.postOrderTraversal(function (key) {
  resultString += key + " ";
});
console.log("✅ ~ 后序遍历resultString:", resultString); // 3 6 5 8 10 9 7 12 14 13 18 25 20 15 11

```

# 🍎 推荐阅读
## 工程化
本系列是一个从0到1的实现过程，如果您有耐心跟着实现，您可以实现一个完整的`react18 + ts5 + webpack5 + 代码质量&代码风格检测&自动修复 + storybook8 + rollup + git action`实现的一个完整的组件库模板项目。如果您不打算自己配置，也可以直接clone[组件库仓库](https://github.com/zhuling904/react_demo/tree/rollup_comp)切换到`rollup_comp`分支即是完整的项目，当前实现已经足够个人使用，后续我们会新增webpack5优化、按需加载组件、实现一些常见的组件封装：包括但不限于拖拽排序、瀑布流、穿梭框、弹窗等  
*   [【前端工程化】项目搭建篇-项目初始化&prettier、eslint、stylelint、lint-staged、husky](https://juejin.cn/post/7353504333999505408)
*   [【前端工程化】项目搭建篇-配置changelog、webpack5打包](https://juejin.cn/post/7353561676091097103)
*   [【前端工程化】项目搭建篇-引入react、ts、babel解析es6+、配置css module](https://juejin.cn/post/7353963878541246504)
*   [【前端工程化】组件库搭建篇-引入storybook、rollup打包组件、本地测试组件库](https://juejin.cn/post/7355026320088989733)
*   [【前端工程化】包管理器篇-三大包管理器、npm工程管理、npm发布流程](https://juejin.cn/post/7356175306937466916)
*   [【前端工程化】自动化篇-Github Action基本使用、自动部署组件库文档、github3D指标统计](https://juejin.cn/post/7356815857078157331)
*   [【前端工程化】自动化篇-手写脚本一键自动tag、发包、引导登录npm](https://juejin.cn/post/7366601730426159144)
## 常见组件实现
*   [【组件实现篇】"从零使用react打造瀑布流的四种方式：完美展示动态图片流"](https://juejin.cn/post/7370513151052021787)
## 面试手写系列
*   [前端面试手写必备【实现常见八大数据结构一】](https://juejin.cn/post/7353504333999505408)
*   [手写哈希表【银四末尾，你上岸了吗？】哈希表，快速计算、均匀分布、扩容实现](https://juejin.cn/post/7359877430340157503)
*   [【前端面试手写必备】树🌲&实现树结构](https://juejin.cn/post/7370513151052038171)
## react实现原理系列
*   [【react原理实践】使用babel手搓探索下jsx的原理](https://juejin.cn/spost/7360512664316117026)
*   [【喂饭式调试react源码】上手调试源码探究jsx原理](https://juejin.cn/spost/7361284455535345699)
*   [【上手调试源码系列】图解react几个核心包之间的关联](https://juejin.cn/spost/7363220284503097354#heading-0)
*   [【上手调试源码系列】react启动流程，其实就是创建三大全局对象](https://juejin.cn/post/7363193808521199655#heading-1)
## 其他
*   [工作流【效率小技巧】让alfred帮我启动所有项目，nice](https://juejin.cn/post/7358709354424860707)
*   [GPT4前端食用指南](https://juejin.cn/post/7352045198854406183)







# 🍋 写在最后

如果您看到这里了，并且觉得这篇文章对您有所帮助，希望您能够点赞👍和收藏⭐支持一下作者🙇🙇🙇，感谢🍺🍺！如果文中有任何不准确之处，也欢迎您指正，共同进步。感谢您的阅读，期待您的点赞👍和收藏⭐！

感兴趣的同学可以关注下我的公众号ObjectX前端实验室


🌟 少走弯路 | ObjectX前端实验室 🛠️「精选资源｜实战经验｜技术洞见」
