# 1、什么是Set

数据结构Set类似于数组，但成员值是唯一的，没有重复的值。Set本身是一个构造函数，用于生成Set数据结构。

```js
const s = new Set();
```

# 2、add()方法

Set通过add()方法添加成员

```js
const s = new Set();
[1,4,2,3,4,6,7,2].forEach(x => s.add(x) );
for(let item of s){
    console.log(item);
}
```

# 3、数组去重

```js
const s1 = new Set([1,5,7,8,2,2,1]);

console.log([...s1]);

```

# 4、NaN

- 向Set加入值时，不会发生类型转换，所以5和"5"是两个不同的值。

```js
const s2 = new Set();
let a=5;
let b="5";
s2.add(a);
s2.add(b);
console.log(s2);// Set(2) {5, "5"}
```

- Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于精确相等运算符（===），主要的区别是NaN等于自身，而精确相等运算符认为NaN不等于自身。
- 在 Set 内部，两个NaN是相等。另外，两个对象总是不相等的。

```js
const s3 = new Set();
s3.add(c);
s3.add(d);
console.log(s3);//Set(1) {NaN}

let set = new Set();
set.add({});
console.log(set.size); // 1
set.add({});
console.log(set.size); // 2

```



# 5、Set实例的属性和方法

## 属性

### （1）Set.prototype.constructor

构造函数，默认就是Set函数

### （2）Set.prototype.size

返回Set实例的成员总数

## 方法

### （1）操作方法

- add(value)，添加某个值，返回Set结构本身
- has(value)，返回一个布尔值，表示该值是否为Set成员
- delete(value)，删除某个值，返回一个布尔值，表示删除成功
- clear()，清除所有成员，没有返回值

注：Array.from()方法，可将Set结构转为数组。

```js
const s4 = new Set([1,4,2,3,5,6,2,4,1,7]);
let Arr = Array.from(s4); 
console.log(s4);//Set(7) {1, 4, 2, 3, 5, …}
```



### （2）遍历方法

- keys()：返回键名的遍历器

- values()：返回键值的遍历器

注：由于 Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致。

- entries()：返回键值对的遍历器

```js
const s5 = new Set(["red","green","blue"]);
for(let item of s5.entries()){
    console.log(item);
}
//["red", "red"]
//["green", "green"]
//["blue", "blue"]
```

- forEach()：使用回调函数遍历每个成员

```js
set = new Set([1, 4, 9]);

set.forEach((value, key) => console.log(key + ' : ' + value))

// 1 : 1

// 4 : 4

// 9 : 9

```

# 6、应用

## （1）数组去重

## （2）间接运用数组的map()和filter()方法

```js
let s6 = new Set([1,2,3]);
s6 = new Set([...s6].map(x => x*2 ));
console.log(s6);//Set(3) {2, 4, 6}

let s7 = new Set([1,2,3,4,5,6,7,8]);
s7 = new Set([...s7].filter(x => (x%2)===0 ));
console.log(s7);//Set(4) {2, 4, 6, 8}
```

## （3）并集（Union）、交集（Intersect）和差集（Difference

```js
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
console.log(union);// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
console.log(intersect);// set {2, 3}

// 差集
let difference = new Set([...a].filter(x => !b.has(x)));
console.log(difference);// Set {1}
```

