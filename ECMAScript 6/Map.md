# 1、含义和基本用法

传统上，JS的对象（object）只能用字符串当做键。

```js
const el = document.getElementById('myDiv');
console.log(el);//<div class="" id="myDiv"></div>
const data = {};
data[el] = "element";
console.log(data);//{[object HTMLDivElement]: "element"}
```

将一个 DOM 节点作为对象data的键，但是由于对象只接受字符串作为键名，所以element被自动转为字符串[object HTMLDivElement]。

Map数据结构类似于对象，是键值对的集合。但是“键”不限于字符串，可以是各种数据类型（包括对象）。

```js
const m = new Map();
const obj = {name:"Admin"};
m.set(obj,"content");
console.log(m);//Map(1) {{…} => "content"}
console.log(m.get(obj));//content
console.log(m.has(obj));//true
console.log(m.delete(obj));//true
console.log(m.has(obj));//false
```

上面代码将一个对象obj作为Map的“键”。通过set()方法设置“键”，通过get()方法取"键"值。



作为一个构造函数，Map也接受一个成员是一个个表示键值对的数组 作为参数。

```js
const map = new Map([["name","张三"],["age","18"]]);
console.log(map.size);//2
console.log(map);//Map(2) {"name" => "张三", "age" => "18"}
console.log(map.get("name"));//张三
console.log(map.get("age"));//18
```

`Map`构造函数接受数组作为参数，实际上执行的是下面的算法。 

```js
const items = [
  ['name', '张三'],
  ['title', 'Author']
];

const map = new Map();

items.forEach(
  ([key, value]) => map.set(key, value)
);
```

> 注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。这一点要非常小心。 

```js
const m = new Map();
m.set(["a"],1);
console.log(m.get(["a"]));//undefined
```

​	上面代码的`set`和`get`方法，表面是针对同一个键，但实际上这是两个值，内存地址是不一样的，因此`get`方法无法读取该键，返回`undefined`。

​	Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，就不用担心自己的属性与原作者的属性同名。 

> 注：在Map中
>
> + 0和-0是同一个键；
> + 布尔true和字符串true是两个不同的键；
> + undefined和null是两个不同键；
> + NaN等于自身。

# 2、实例的属性和操作方法

## （1）size属性

size属性返回Map结构的成员总数

## （2）set(key, value)

`set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键。 

```js
let map = new Map();
map.set(1,"张三");//Map(1) {1 => "张三"}
map.set(2,"李四");//Map(2) {1 => "张三", 2 => "李四"}
```

`set`方法返回的是当前的`Map`对象，因此可以采用链式写法。 

```js
let m = new Map().set(1,"张三").set(2,"李四");
m//Map(2) {1 => "张三", 2 => "李四"}
```

## **（3）get(key)** 

`get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。 

## （4）has(key)

`has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。 

## （5）**delete(key)** 

`delete`方法删除某个键，返回`true`。如果删除失败，返回`false`。 

## **（6）clear()** 

`clear`方法清除所有成员，没有返回值。 

# 3、遍历方法 

Map 结构原生提供三个遍历器生成函数和一个遍历方法。

- `keys()`：返回键名的遍历器。
- `values()`：返回键值的遍历器。
- `entries()`：返回所有成员的遍历器。
- `forEach()`：遍历 Map 的所有成员。

需要特别注意的是，Map 的遍历顺序就是插入顺序。

```js
for(let key of m.keys()){console.log(key);}
//1
//2

for(let value of m.values()){console.log(value);}
//张三
//李四

for(let [key,value] of m.entries()){console.log(key,value);}
//1 "张三"
//2 "李四"

for(let [key,value] of m){console.log(key,value);}
//1 "张三"
//2 "李四"

for(let item of m.entries()){console.log(item[0],item[1]);}
//1 "张三"
//2 "李四"
```

Map 结构的默认遍历器接口（`Symbol.iterator`属性），就是`entries`方法。 

```js
m[Symbol.iterator] === m.entries//true
```

Map 结构转为数组结构，比较快速的方法是使用扩展运算符（`...`）。 

```js
[...m.keys()]
//(2) [1, 2]

[...m.values()]
//(2) ["张三", "李四"]

[...m.entries()]
//(2) [[1, "张三"], [2, "李四"]]

[...m]
//(2) [[1, "张三"], [2, "李四"]]
```

结合数组的`map`方法、`filter`方法，可以实现 Map 的遍历和过滤（Map 本身没有`map`和`filter`方法）。 

此外，Map 还有一个`forEach`方法，与数组的`forEach`方法类似，也可以实现遍历。 `forEach`方法还可以接受第二个参数，用来绑定`this`。 

```js

```

# 4、与其他数据结构的互相转换

## **（1）Map 转为数组** 

使用扩展运算符（`...`） 

## （2）**数组 转为 Map** 

将数组传入 Map 构造函数，就可以转为 Map。 

```js
let m = new Map([[1,"张三"],[{name:"李四"},[2,"王五"]]]);
m//Map(2) {1 => "张三", {…} => Array(2)}
```

## **（3）Map 转为对象** 

如果所有 Map 的键都是字符串，它可以无损地转为对象。 如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。 

## **（4）对象转为 Map** 

```js
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({yes: true, no: false})
// Map {"yes" => true, "no" => false}
```

## （5）Map 转为 JSON 

Map 转为 JSON 要区分两种情况。 

一种情况是，Map 的键名都是字符串，这时可以选择转为对象 JSON。 

+ 先将Map结构转为对象

+ 再使用JSON.stringify()

  

另一种情况是，Map 的键名有非字符串，这时可以选择转为数组 JSON。 

+ 先将Map结构转为数组
+ 再使用JSON.stringify()

## （6）**JSON 转为 Map** 

JSON 转为 Map，正常情况下，所有键名都是字符串。 

```js
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({yes: true, no: false})
// Map {"yes" => true, "no" => false}

function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes": true, "no": false}')
// Map {'yes' => true, 'no' => false}
```

但是，有一种特殊情况，整个 JSON 就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为 Map。这往往是 Map 转为数组 JSON 的逆操作。 

```js
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

