---
group:
  title: 01常见数据结构实现篇
  order: 1
title: 1.数组
order: 1
---
# 🥝 一、数组
## 1.数组理论知识

1.  **定义**：数组是一种由相同类型的元素组成的数据集合，这些元素按照一定的顺序排列，并且可以通过索引（下标）来访问。

1.  **下标访问**：数组中的元素可以通过下标来访问，下标通常从0开始递增。这是因为数组在内存中是一段连续的存储空间，每个元素占据固定大小的内存单元。通过计算偏移量（索引 * 单个元素大小），可以快速定位数组中的任意元素。

1.  **内存存储**：数组在内存中是连续存储的，即数组的各个元素依次存储在相邻的内存单元中。这种存储方式使得通过下标访问元素的时间复杂度为O(1)，即具有很高的访问效率。

1.  数组的特点包括：
    * 元素类型相同。
    * 连续存储，可以通过下标快速访问。
    * 大小固定，无法动态扩展。

1.  动态数组：
    -   问题：动态数组是什么？它与静态数组有何区别？
    -   解答：动态数组是一种可以动态增长和缩小的数组，与静态数组不同的是，它的大小可以根据需要动态调整，通常通过重新分配内存来实现。
    -   数组在大多数编程语言中的大小固定，无法动态扩展的原因主要是因为数组在内存中是一段连续的存储空间，这段空间在创建数组时就已经确定了大小。当我们创建一个数组时，计算机会为它分配一段连续的内存空间来存储元素。这段内存空间的大小是在数组创建时确定的，通常是根据数组的类型和长度计算得出的。因此，一旦数组被创建，它的大小就固定了，无法直接在原来的内存空间上进行扩展。
    -   要想扩展数组，通常需要进行以下操作：分配一块新的内存空间，大小比原数组大。将原数组中的元素复制到新的内存空间中。释放原数组所占用的内存空间。

## 2.数组的优缺点

**数组的优缺点**：
-   问题：数组有哪些优点和缺点？
-   解答：数组的优点包括：
    -   快速访问：通过下标可以快速访问任意位置的元素。
    -   简单高效：数组的存储和访问操作都非常简单高效。
-   缺点包括：
    -   大小固定：无法动态扩展，可能导致内存浪费或需要重新分配更大的空间。
    -   插入和删除元素效率低：需要移动其他元素，效率较低。

-   在大多数编程语言中，数组的内存空间是一段连续的存储空间，每个元素占据固定大小的内存。当我们在数组中删除或插入元素时，如果要保持数组的顺序不变，就需要移动元素。

    *  **删除元素**：

        -   如果要删除数组中的某个元素，那么这个元素之后的所有元素都需要向前移动一个位置，以填补被删除元素的空缺。这是因为数组的内存空间是连续的，删除一个元素会造成后续元素的位置变化，为了保持数组的连续性和顺序不变，需要移动元素。

    *  **插入元素**：

        -   如果要在数组中插入一个元素，那么插入位置之后的所有元素都需要向后移动一个位置，为新元素腾出空间。同样地，为了保持数组的连续性和顺序不变，需要移动元素。

## 3.JS中的数组

数组的标准定义是：一个存储元素的线性集合 (collection)，元素可以通过索引来任意存取，索引通常是数字，用来计算元素之间存储位置的偏移量。几乎所有的编程语言都有类似的数据结构。然而 Javascript 的数组却略有不同。

JavaScript 中的数组是一种特殊的对象，用来表示偏移量的索引是该对象的属性，索引可能是整数。然而，这些数字索引在内部被转换为字符串类型，这是因为 JavaScript 对象中的属性名必须是字符串。数组在Javascript 中只是一种特殊的对象，所以效率上不如其他语言中的数组高。

Javaseript 中的数组，严格来说应该称作对象，是特殊的 Javascript 对象，在内部被归类为数组。由于 Array 在Javascript 中被当作对象，因此它有许多属性和方法可以在编程时使用。

### 创建数组

在 JavaScript 中，有几种常见的方式来创建数组：

1.  **使用数组字面量**：

    ```js
    let arr = [1, 2, 3, 4]; // 创建一个包含4个元素的数组
    ```

    这种方式是最简单和常见的创建数组的方式，直接使用方括号**`[]`**来包裹数组元素，每个元素之间用逗号分隔。

1.  **通过构造函数创建**：

    ```js
    let arr = new Array(1, 2, 3, 4); // 使用构造函数创建数组
    ```

    可以使用**`new Array()`**语法来创建数组，传入的参数是数组的元素。需要注意的是，如果传入的参数是一个数字，则表示创建一个具有该长度的稀疏数组，而不是包含该数字作为唯一元素的数组。

1.  **使用 Array.of() 方法**：

    ```js
    let arr = Array.of(1, 2, 3, 4); // 使用 Array.of() 方法创建数组
    ```

    **`Array.of()`**方法是 ES6 新增的方法，用于创建具有指定元素的数组。

1.  **使用 Array.from() 方法**：

    ```js
    let arr = Array.from([1, 2, 3, 4]); // 使用 Array.from() 方法将类数组对象或可迭代对象转换为数组
    ```

    **`Array.from()`** 方法是 ES6 新增的方法，可以将类数组对象或可迭代对象转换为数组。

这些是在 JavaScript 中创建数组的常见方式，每种方式都有其特点和适用场景，开发者可以根据实际需求选择合适的方式来创建数组。

### 增

JavaScript 中常用的数组添加方法包括以下几种：

1.  **使用 push() 方法添加到末尾**：

    -   **`push()`** 方法用于向数组的末尾添加一个或多个元素，并返回新数组的长度。该方法会改变原数组。

    示例：

    ```js
    let arr = [1, 2, 3];
    arr.push(4); // arr 变为 [1, 2, 3, 4]
    ```

1.  **使用 unshift() 方法添加到开头**：

    -   **`unshift()`** 方法用于向数组的开头添加一个或多个元素，并返回新数组的长度。该方法会改变原数组。

    示例：

    ```js
    let arr = [2, 3, 4];
    arr.unshift(1); // arr 变为 [1, 2, 3, 4]
    ```

1.  **使用 splice() 方法插入元素**：

    -   **`splice(start, deleteCount, item1, item2, ...)`** 方法除了可以删除元素外，还可以在指定位置插入新的元素。其中 **`start`** 是插入位置的索引，**`deleteCount`** 是删除的元素个数，**`item1, item2, ...`** 是要插入的元素。该方法会改变原数组。

    示例：

    ```js
    let arr = [1, 2, 4];
    arr.splice(2, 0, 3); // arr 变为 [1, 2, 3, 4]
    ```

1.  **使用 concat() 方法连接数组**：

    -   **`concat()`** 方法用于连接两个或多个数组，并返回一个新数组，不改变原数组。

    示例：

    ```js
    let arr1 = [1, 2];
    let arr2 = [3, 4];
    let newArr = arr1.concat(arr2); // newArr 为 [1, 2, 3, 4]，arr1 和 arr2 不变
    ```

这些方法提供了不同的添加元素到数组的方式，可以根据实际需求选择合适的方法进行操作。

### 删

JavaScript 中常用的数组删除方法包括以下几种：

1.  **使用 pop() 方法删除末尾元素**：

    -   **`pop()`** 方法用于删除数组的最后一个元素，并返回被删除的元素。该方法会改变原数组的长度。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let removedElement = arr.pop(); // 返回 4，arr 变为 [1, 2, 3]
    ```

1.  **使用 shift() 方法删除第一个元素**：

    -   **`shift()`** 方法用于删除数组的第一个元素，并返回被删除的元素。该方法会改变原数组的长度和索引。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let removedElement = arr.shift(); // 返回 1，arr 变为 [2, 3, 4]
    ```

1.  **使用 splice() 方法删除指定位置的元素**：

    -   **`splice(start, deleteCount, item1, item2, ...)`** 方法可以删除数组中从 **`start`** 位置开始的 **`deleteCount`** 个元素，并可以在删除的位置插入新的元素。该方法会改变原数组。

    示例：

    ```js
    // 从下标为1的位置删除两个元素
    let arr = [1, 2, 3, 4];
    let removedElements = arr.splice(1, 2); // 返回 [2, 3]，arr 变为 [1, 4]
    ```

1.  **使用 filter() 方法删除符合条件的元素**：

    -   **`filter(callback)`** 方法用于根据指定的条件过滤数组中的元素，并返回一个新数组，不改变原数组。可以结合条件判断函数来实现删除符合条件的元素。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let newArr = arr.filter(item => item !== 2); // newArr 为 [1, 3, 4]，arr 不变
    ```

这些方法提供了不同的删除数组元素的方式，可以根据实际需求选择合适的方法进行操作。

### 改

JavaScript 中常用的数组修改方法包括以下几种：

1.  **直接通过索引修改元素**：

    -   可以直接通过索引来修改数组中的元素值。

    示例：

    ```js
    let arr = [1, 2, 3];
    arr[1] = 4; // arr 变为 [1, 4, 3]
    ```

1.  **使用 splice() 方法替换元素**：

    -   **`splice(start, deleteCount, item1, item2, ...)`** 方法除了可以删除和插入元素外，还可以替换指定位置的元素。其中 **`start`** 是替换位置的索引，**`deleteCount`** 是删除的元素个数，**`item1, item2, ...`** 是要替换的元素。该方法会改变原数组。

    示例：

    ```js
    let arr = [1, 2, 3];
    arr.splice(1, 1, 4); // arr 变为 [1, 4, 3]
    ```

1.  **使用 map() 方法修改元素**：

    -   **`map(callback)`** 方法会创建一个新数组，新数组的元素是原数组经过某种操作后的结果。可以结合回调函数对每个元素进行修改。

    示例：

    ```js
    let arr = [1, 2, 3];
    let newArr = arr.map(item => item * 2); // newArr 为 [2, 4, 6]，arr 不变
    ```

1.  **使用 forEach() 方法修改元素**：

    -   **`forEach(callback)`** 方法会对数组的每个元素执行一次指定的函数。可以直接在回调函数中修改元素的值。

    示例：

    ```js
    let arr = [1, 2, 3];
    arr.forEach((item, index, array) => {
      array[index] = item * 2;
    }); // arr 变为 [2, 4, 6]
    ```

这些方法提供了不同的修改数组元素的方式，可以根据实际需求选择合适的方法进行操作。

### 查

JavaScript 中查找数组元素可以使用多种方法，下面是一些常见的方法：

1.  `indexOf()`

    返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

    ```js
    const array = [2, 5, 9];
    console.log(array.indexOf(2));// 0
    console.log(array.indexOf(7));// -1
    ```

1.  `find()`

    返回数组中满足提供的测试函数的第一个元素的值。如果没有找到符合条件的元素，则返回`undefined`。

    ```js
    const array = [5, 12, 8, 130, 44];
    const found = array.find(element => element > 10);
    console.log(found);// 12
    ```

1.  `findIndex()`

    返回数组中满足提供的测试函数的第一个元素的索引。如果没有找到符合条件的元素，则返回-1。

    ```js
    const array = [5, 12, 8, 130, 44];
    const isLargeNumber = (element) => element > 13;
    console.log(array.findIndex(isLargeNumber));// 3
    ```

1.  `includes()`

    用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回true，否则返回false。

    ```js
    const array = [1, 2, 3];
    console.log(array.includes(2));// true
    console.log(array.includes(4));// false
    ```

1.  `filter()`

    创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

    ```js
    const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
    const result = words.filter(word => word.length > 6);
    console.log(result); // ["exuberant", "destruction", "present"]
    ```

1.  `some()`

    测试数组中是不是至少有1个元素通过了被提供的函数测试。它返回的是一个布尔值。

    ```js
    const array = [1, 2, 3, 4, 5];
    const even = (element) => element % 2 === 0;
    console.log(array.some(even));// true
    ```

1.  `every()`

    测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。

    ```js
    const isBelowThreshold = (currentValue) => currentValue < 40;
    const array1 = [1, 30, 39, 29, 10, 13];
    console.log(array1.every(isBelowThreshold));// true
    ```

这些方法都是 ECMAScript 5 或更高版本中引入的，因此在现代浏览器中应该都可以使用。需要注意的是，`find()` 和 `findIndex()` 是 ECMAScript 6 中新增的方法。

### 遍历

1.  **使用 for 循环遍历**：

    ```js
    let arr = [1, 2, 3];
    for (let i = 0; i < arr.length; i++) {
      console.log(arr[i]);
    }
    ```

1.  **使用 forEach() 方法遍历**：

    ```js
    let arr = [1, 2, 3];
    arr.forEach(item => {
      console.log(item);
    });
    ```

1.  **使用 map() 方法遍历**：

    ```js
    let arr = [1, 2, 3];
    let newArr = arr.map(item => {
      return item * 2;
    });
    ```

1.  **使用 for...of 循环遍历**：

    ```js
    let arr = [1, 2, 3];
    for (let item of arr) {
      console.log(item);
    }
    ```

这些方法各有特点，可以根据实际需求选择合适的方法进行数组遍历。

### 其他方法

1.  **concat() 方法**：

    -   **`concat()`** 方法用于连接两个或多个数组，并返回一个新数组。

    示例：

    ```js
    let arr1 = [1, 2];
    let arr2 = [3, 4];
    let newArr = arr1.concat(arr2); // newArr 为 [1, 2, 3, 4]
    ```

1.  **slice() 方法**：

    -   **`slice(start, end)`** 方法用于从原数组中提取出指定范围的元素，返回一个新数组。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let newArr = arr.slice(1, 3); // newArr 为 [2, 3]
    ```

1.  **indexOf() 和 lastIndexOf() 方法**：

    -   **`indexOf(item)`** 方法用于返回数组中第一个匹配项的索引，如果没有找到匹配项则返回 -1。
    -   **`lastIndexOf(item)`** 方法用于返回数组中最后一个匹配项的索引，如果没有找到匹配项则返回 -1。

    示例：

    ```js
    let arr = [1, 2, 3, 4, 2];
    let index = arr.indexOf(2); // index 为 1
    let lastIndex = arr.lastIndexOf(2); // lastIndex 为 4
    ```

1.  **join() 方法**：

    -   **`join(separator)`** 方法用于将数组中的所有元素连接成一个字符串。可以指定一个分隔符来分隔数组元素，默认为逗号。

    示例：

    ```js
    let arr = [1, 2, 3];
    let str = arr.join('-'); // str 为 "1-2-3"
    ```

1.  **toString() 方法**：

    -   **`toString()`** 方法用于将数组转换为字符串，并返回结果。

    示例：

    ```js
    let arr = [1, 2, 3];
    let str = arr.toString(); // str 为 "1,2,3"
    ```

1.  **filter() 方法**：

    -   **`filter(callback)`** 方法用于筛选数组中符合指定条件的元素，并返回一个新数组。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let newArr = arr.filter(item => item % 2 === 0); // newArr 为 [2, 4]
    ```

1.  **find() 和 findIndex() 方法**：

    -   **`find(callback)`** 方法用于返回数组中第一个符合条件的元素，如果没有找到则返回 undefined。
    -   **`findIndex(callback)`** 方法用于返回数组中第一个符合条件的元素的索引，如果没有找到则返回 -1。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let found = arr.find(item => item > 2); // found 为 3
    let foundIndex = arr.findIndex(item => item > 2); // foundIndex 为 2
    ```

1.  **sort() 方法**：

    -   **`sort(compareFunction)`** 方法用于对数组元素进行排序，默认按照字符串 Unicode 代码点排序。可以传入一个比较函数来指定排序规则。

    示例：

    ```js
    let arr = [3, 1, 4, 2];
    arr.sort((a, b) => a - b); // arr 变为 [1, 2, 3, 4]
    ```

1.  **reverse() 方法**：

    -   **`reverse()`** 方法用于颠倒数组中元素的顺序，原地修改数组。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    arr.reverse(); // arr 变为 [4, 3, 2, 1]
    ```

1.  **reduce() 和 reduceRight() 方法**：

    -   **`reduce(callback, initialValue)`** 方法用于累积数组的每个元素，并返回一个累加的结果。
    -   **`reduceRight(callback, initialValue)`** 方法与 **`reduce()`** 类似，但是从数组的末尾开始累加。

    示例：

    ```js
    let arr = [1, 2, 3, 4];
    let sum = arr.reduce((accumulator, currentValue) => accumulator + currentValue, 0); // sum 为 10
    ```

1.  **使用 every() 方法遍历**：

    -   **`every(callback)`** 方法用于检测数组的所有元素是否都符合指定条件。它会对数组中的每个元素执行一次回调函数，直到找到一个不符合条件的元素为止。

    示例：

    ```js
    let arr = [1, 2, 3];
    let result = arr.every(item => item > 0); // result 为 true
    ```

1.  **使用 some() 方法遍历**：

    -   **`some(callback)`** 方法用于检测数组的是否至少有一个元素符合指定条件。它会对数组中的每个元素执行一次回调函数，直到找到一个符合条件的元素为止。

    示例：

    ```js
    let arr = [1, 2, 3];
    let result = arr.some(item => item > 2); // result 为 true
    ```
    
## 4.实现数组结构
没什么可说的时间思路比较简单，看注释即可。

```js
/**
 * 基本数组结构
 */
class BasicArray {
  constructor() {
    this.length = 0;
    this.data = {};
  }

  /**
   * 末尾增加元素
   * @param {*} item
   */
  add(item) {
    this.data[this.length] = item;
    this.length++;
  }

  /**
   * 任意位置插入元素
   * @param {*} index
   * @param {*} item
   */
  insert(index, item) {
    if (index < 0) index = 0;
    if (index > this.length) index = this.length;
    // 从最后一个开始移动，让出i的位置
    if (index >= 0 && index <= this.length) {
      for (let i = this.length; i > index; i--) {
        this.data[i] = this.data[i - 1];
      }
      this.data[index] = item;
    }
    this.length++;
  }

  /**
   * 删除指定位置元素
   * @param {*} index
   * @returns
   */
  delete(index) {
    const deleted = this.data[index];
    // 用i后面的元素覆盖之前的元素
    for (let i = index; i < this.length - 1; i++) {
      this.data[i] = this.data[i + 1];
    }
    // 前面的元素被填充了，最后一个空出来了
    delete this.data[this.length - 1];
    // 记得长度-1
    this.length--;
    return deleted;
  }

  /**
   * 更新元素
   * @param {*} index
   * @param {*} item
   */
  update(index, item) {
    this.data[index] = item;
  }

  /**
   * 获取数组长度
   * @returns
   */
  getLength() {
    return this.length;
  }

  /**
   * 获取元素
   * @param {*} index
   * @returns
   */
  get(index) {
    return this.data[index];
  }

  /**
   * 获取整个数组
   * @returns
   */
  getArray() {
    return this.data;
  }

  /**
   * 打印帮助函数，用来判断是否修改了原数组
   * @param {*} operateName
   * @param {*} array
   * @param {*} callback
   */
  logHelper(operateName, array, callback) {
    const input = [...array];
    const result = callback();

    console.log({
      operation: operateName,
      arrayBefore: input,
      arrayAfter: array,
      mutates: this.mutatesArray(input, array),
      result,
    });
  }

  /**
   * 浅比较判断数组是否修改
   * @param {*} array1 原始数组
   * @param {*} array2 修改后的数组
   * @returns
   */
  mutatesArray(array1, array2) {
    // 长度不同肯定不相等
    if (array1.length !== array2.length) return true;
    for (let i = 0; i < array2.length; i++) {
      if (array1[i] !== array2[i]) {
        return true;
      }
    }
    return false;
  }
}

// // 基本数组使用示例
// const myArray = new BasicArray();
// myArray.insert(0, 'a');
// myArray.insert(1, 'b');
// myArray.insert(2, 'c');
// myArray.print(); // ['a', 'b', 'c']

// myArray.update(1, 'x');
// myArray.print(); // ['a', 'x', 'c']

// myArray.delete(0);
// myArray.print(); // ['x', 'c']

// console.log(myArray.getLength()); // 2

module.exports = BasicArray;

```
