---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 7.字典
order: 7
---
# 🍉 七、字典
## 1.理论知识
字典（Dictionary），也称为映射（Map），是一种键值对（key-value）的数据结构，用于存储一组唯一的键和与之相关联的值。在字典中，键是唯一的，每个键都对应一个值。

### 基本操作：

1.  **`set(key,value)`添加键值对**：向字典中添加一个新的键值对。
1.  **`remove(key)`删除键值对**：从字典中删除指定键的键值对。
1.  **`get(key)`获取值**：根据键获取对应的值。
1.  **`has(key)`检查键是否存在**：检查字典中是否存在指定的键。
1.  **`size()`获取键值对数量**：获取字典中键值对的数量。
1.  **`keys()`获取所有键**：获取字典中所有的键或所有的值。
1.  **`values()`获取所有值**：获取字典中所有的值。

### 字典的应用场景：

-   **存储键值对**：字典可以用来存储一组键值对，如对象的属性。
-   **快速查找**：通过键可以快速查找对应的值，比起数组来说，查找速度更快。
-   **缓存数据**：可以用字典来缓存一些计算结果，避免重复计算。

### 注意事项：

-   字典中的键是唯一的，如果添加相同的键，后面的值会覆盖前面的值。
-   在使用自定义对象作为键时，要确保对象的引用相同，否则会导致无法正确获取值的问题。

## 2.字典的优缺点
### 优点：

1.  **快速查找**：字典可以根据键快速查找对应的值，查找效率高。
1.  **灵活性**：字典中的键可以是任意类型的，包括原始类型和对象引用，值也可以是任意类型的。
1.  **动态性**：字典的大小和内容可以动态调整，无需预先分配空间。
1.  **数据组织**：适用于需要以键值对形式存储数据的场景，如对象属性、配置信息等。

### 缺点：

1.  **内存消耗**：相比于数组，字典需要额外的内存空间来存储键值对的关系，可能会占用较多的内存。
1.  **性能问题**：在一些操作上，字典的性能可能不如数组，比如遍历字典中的所有键值对可能需要较长的时间。
1.  **无序性**：字典中的键值对是**无序**的，无法保证插入顺序和遍历顺序一致。

## 3.js中的字典
在 JavaScript 中，可以使用 `Map` 对象来实现字典功能，但是实现的本质不是一样的，下面的章节我们会介绍如何实现的。

## 4.实现字典结构
```js
class Dictionary {
  items = {};

  set(key, value) {
    this.items[key] = value;
  }

  has(key) {
    return Object.prototype.hasOwnProperty.call(this.items, key);
  }

  remove(key) {
    if (!this.has(key)) return false;
    delete this.items[key];
    return true;
  }

  get(key) {
    return this.has(key) ? this.items[key] : undefined;
  }

  keys() {
    return Object.keys(this.items);
  }

  values() {
    return Object.values(this.items);
  }

  size() {
    return this.keys().length;
  }

  clear() {
    this.items = {};
  }
}

// 创建字典对象
const dict = new Dictionary();

// 在字典中添加元素
dict.set("age", 18);
dict.set("name", "Coderwhy");
dict.set("height", 1.88);
dict.set("address", "广州市");

// 获取字典的信息
console.log(dict.keys()); // age,name,height,address
console.log(dict.values()); // 18,Coderwhy,1.88,广州市
console.log(dict.size()); // 4
console.log(dict.get("name")); // Coderwhy

// 字典的删除方法
dict.remove("height");
console.log(dict.keys()); // age,name,address

// 清空字典
dict.clear();

```
