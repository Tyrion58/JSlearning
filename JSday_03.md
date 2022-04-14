# JS_day_03

### 模板字符串

要把多个字符串连接起来，用+号；**对，直接相加就可以连接字符串，不用像C里面那样去做复杂操作**

```js
var name = '小明';
var age = 20;
var message = '你好, ' + name + ', 你今年' + age + '岁了!';
alert(message);
```

ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：

```js
var name = '小明';
var age = 20;
var message = `你好, ${name}, 你今年${age}岁了!`;
alert(message);
```

就不用反复去写+了

### 操作字符串

`s.length;`直接获取字符串s的长度

`s[i]`获取字符串s第i位置的元素

#### 一些常用的字符串方法：

* `toUpperCase()`把一个字符串全变为大写

  `s.toUpperCase(); //返回大写的数组`

* 同理，`toLowerCase()`把字符串全变为小写

* `indexOf()`搜索指定子串出现的位置，返回下标；没有找到时返回-1

* `substring()`返回指定区间的子串，注意是直接取出子串

  ```js
  var s = 'hello, world'
  s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
  s.substring(7); // 从索引7开始到结束，返回'world'
  ```

## 数组`array`

JS中的`array`可以包含任意数据类型，并通过索引访问每个元素

**要获得`array`的长度，直接访问`length`属性**

```js
var arr = [1, 2, 3.14, 'Hello', null, true];
arr.length; // 6
```

若直接给array的`length`赋一个新的值，会导致其大小发生变化，空位置会变为`undefinde`

若新的长度小于原先长度，会把多出来的那一部分直接丢失

```js
var arr = [1, 2, 3];
arr.length; // 3
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
```

`Array`可以通过索引把对应的元素修改为新的值，因此，对`Array`的索引进行赋值会直接修改这个`Array`：

```js
var arr = ['A', 'B', 'C'];
arr[1] = 99;
arr; // arr现在变为['A', 99, 'C']
```

*请注意*，如果通过索引赋值时，索引超过了范围，同样会引起`Array`大小的变化：

比如说我的arr数组只有3个元素，你却对arr[5]赋值，那么arr就会自动扩充长度变为6：

```js
var arr = [1, 2, 3];
arr[5] = 'x';
arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
```

**确实有点怪，因为大部分编程语言都不会允许你访问数组越界的**

然而，JavaScript的`Array`却不会有任何错误。在编写代码时，不建议直接修改`Array`的大小，访问索引时要确保索引不会越界。

### 一些数组的基础操作

* `Array`也可以通过`indexOf()`来搜索一个指定的元素的位置：

  ```js
  var arr = [10, 20, '30', 'xyz'];
  arr.indexOf(10); // 元素10的索引为0
  arr.indexOf(20); // 元素20的索引为1
  arr.indexOf(30); // 元素30没有找到，返回-1
  arr.indexOf('30'); // 元素'30'的索引为2
  ```

  注意了，数字`30`和字符串`'30'`是不同的元素。

* `slice()`对应字符串中的 `substring()`,截取数组中的一部分元素，返回一个新的数组

```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```

注意到`slice()`的起止参数包括开始索引，不包括结束索引。

如果不给`slice()`传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个`Array`：

```js
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```

* push()向数组末尾添加若干元素，pop()把数组最后一个元素删除掉,其返回值是被取出来的那个元素；**空数组继续pop不会报错，而是返回undefined**

```js
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```

* 与上面对应，unshift()方法在数组的头部添加若干元素，shift()方法则把数组的第一个元素删掉，返回值是被删掉的那个元素

* sort()对当前数组排序，**直接调用时会按照默认顺序排序**

  当然我们也有办法指定顺序

* reverse()将整个数组反转

* `splice()`方法是修改`Array`的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：**重点看看**

  ```js
  var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
  // 从索引2开始删除3个元素,然后再添加两个元素:
  arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
  arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
  // 只删除,不添加:
  arr.splice(2, 2); // ['Google', 'Facebook']
  arr; // ['Microsoft', 'Apple', 'Oracle']
  // 只添加,不删除:
  arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
  arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
  ```

* concat ( )把当前的数组和另一个数组连接起来，**得到一个新的数组**，注意：原先的数组没有变

* ```js
  var arr = ['A', 'B', 'C'];
  var added = arr.concat([1, 2, 3]);
  added; // ['A', 'B', 'C', 1, 2, 3]
  arr; // ['A', 'B', 'C']
  ```

实际上，`concat()`方法可以接收任意个元素和`Array`，并且自动把`Array`拆开，然后全部添加到新的`Array`里：

```js
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```

* join()方法把当前数组的每个元素都用**指定字符串**连接起来，返回连接后的字符串

  ```js
  var arr = ['A', 'B', 'C', 1, 2, 3]js;
  arr.join('-'); // 'A-B-C-1-2-3'
  ```

  如果`Array`的元素不是字符串，将自动转换为字符串后再连接。

* 多维数组：数组的某个元素又是一个数组

