# 1、概念#

WeakSet结构与Set类似，成员都是唯一的。但是，它与Set有两个区别：

+ WeakSet的成员只能是对象。
+ WeakSet中的对象都是弱引用，即如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中 。WeakSet不可遍历。

# 2、语法#

WeakSet是一个构造函数，可以使用new关键字创建一个WeakSet数据结构。

```js
let ws = new WeakSet();
```

作为构造函数，WeakSet 可以接受一个数组或类似数组的对象作为参数。 

```js
let a = [[1,2],[3,4]];
let ws = new WeakSet(a);
console.log(ws);//WeakSet{[1,2],[3,4]}
```

a是一个数组，它的成员也是两个数组，a作为WeakSet构造函数的参数，a的成员也会成为WeakSet的成员。

> a数组的成员成为 WeakSet 的成员，而不是a数组本身。这意味着，数组的成员只能是对象。 

```js
let a = [1,2];
let ws = new WeakSet(a);
console.log(ws);//Uncaught TypeError
```

此时，a数组成员不是对象，加入WeakSet就会报错。

# 3、方法#

- **WeakSet.prototype.add(value)**：向 WeakSet 实例添加一个新成员。
- **WeakSet.prototype.delete(value)**：清除 WeakSet 实例的指定成员。
- **WeakSet.prototype.has(value)**：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。

# 4、其它#

​	WeakSet 没有size属性，没有办法遍历它的成员。 WeakSet 不能遍历，是因为成员都是弱引用，随时可能消失，遍历机制无法保证成员的存在，很可能刚刚遍历结束，成员就取不到了。WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。 