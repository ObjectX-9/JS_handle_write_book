---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 6.集合
order: 6
---
# 🥝 六、集合
## 1.集合的理论知识
集合（Set）是一种数据结构，用于存储一组唯一的值，这些值按照插入的顺序排列，没有重复的元素。在集合中，元素的顺序是不重要的，而且集合通常没有索引。

### 基本操作：

1.  **添加元素`add(value)`**：向集合中添加一个新元素。
1.  **删除元素`remove(value)`**：从集合中删除一个元素。
1.  **检查元素是否存在`has(value)`**：检查集合中是否存在某个元素。
1.  **清空集合`clear()`**：清空集合中的所有元素。
1.  **获取集合大小`size()`**：获取集合中包含的元素数量。
2.  **获取集合中的所有值`values()`**：返回一个包含集合中所有值的数组。
### 集合的应用场景：

-   **去重**：集合可以用来去除数组中的重复元素。
-   **数学集合操作**：如并集、交集、差集等。
-   **缓存数据**：可以用集合来存储缓存的数据，以确保数据的唯一性。

### 注意事项：

-   集合不允许重复元素，如果添加重复元素，集合会自动去除重复值。
-   在使用自定义对象时，要注意对象的引用是否相同，因为集合中的元素是通过引用来比较是否相等的。
## 2.集合的优缺点
### 优点：

1.  **唯一性**：集合中的元素是唯一的，可以避免重复元素的存在。
1.  **无序性**：集合中的元素没有固定的顺序，这在某些场景下是一个优势。
1.  **快速查找**：使用 `has()` 方法可以快速查找集合中是否包含某个元素。
1.  **动态性**：集合的大小和内容可以动态调整，无需预先分配空间。

### 缺点：

1.  **无法直接访问**：集合中的元素没有索引，无法直接通过索引访问元素，只能通过遍历或 `has()` 方法来查找元素。
1.  **不支持键值对**：集合中只包含值，不支持键值对的形式，因此在需要存储键值对的情况下，需要使用 Map 数据结构。
1.  **性能问题**：在一些操作上，集合的性能可能不如数组，比如遍历集合中的元素需要一定的时间复杂度。
## 3.js中的集合
在 JavaScript 中，集合（Set）是一种数据结构，类似于数组，但是集合中的元素是唯一且无序的。这意味着集合中不允许有重复的值，并且集合中的元素没有固定的顺序。JavaScript 中的集合是通过 Set 对象来实现的。

### 创建集合：

可以使用 Set 构造函数来创建一个空集合，也可以将一个数组或类数组对象传递给 Set 构造函数来创建包含初始值的集合。

```js
let set = new Set(); // 创建空集合
let set2 = new Set([1, 2, 3, 4, 5]); // 创建包含初始值的集合
```

### 基本操作：

-   **添加元素**：使用 `add()` 方法向集合中添加元素，如果元素已经存在于集合中，则不会重复添加。

```js
set.add(1);
set.add(2);
set.add(3);
```

-   **删除元素**：使用 `delete()` 方法从集合中删除指定元素。

```js
set.delete(2);
```

-   **判断元素是否存在**：使用 `has()` 方法判断集合中是否存在指定元素。

```js
set.has(1); // true
set.has(2); // false
```

-   **清空集合**：使用 `clear()` 方法清空集合中的所有元素。

```js
set.clear();
```

-   **获取集合大小**：使用 `size` 属性获取集合中元素的数量。

```js
set.size; // 2
```

-   **遍历集合**：可以使用 `forEach()` 方法或 `for...of` 循环来遍历集合中的元素。

```js
set.forEach((value) => {
  console.log(value);
});

for (let value of set) {
  console.log(value);
}
```
## 4.实现集合结构
用对象来模拟，这里主要需要注意键值的存储形式`obj[value] = value`
```js
class MySet {
  items = {};
  has(value) {
    return Object.prototype.hasOwnProperty.call(this.items, value);
  }

  add(value) {
    if (this.has(value)) return false;
    this.items[value] = value;
    return true;
  }

  remove(value) {
    if (!this.has(value)) return false;
    delete this.items[value];
    return true;
  }

  clear() {
    this.items = {};
  }

  size() {
    return Object.keys(this.items).length;
  }

  values() {
    // 这里是因为item[value] = value;
    return Object.keys(this.items);
  }
}

// 测试和使用集合类
const set = new MySet();

// 添加元素
set.add(1);
console.log(set.values());
set.add(1);
console.log(set.values());

set.add(100);
set.add(200);
console.log(set.values());

// 判断是否包含元素
console.log(set.has(100)); // true

// 删除元素
set.remove(100);
console.log(set.values()); // 1, 200

// 获取集合的大小
console.log(set.size()); // 2
set.clear();
console.log(set.size()); // 0
```
