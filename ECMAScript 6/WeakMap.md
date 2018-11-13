# 1、含义

WeakMap结构和Map结构类似，也是用于生成键值对的集合。

WeakMap与Map区别：

+ WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。 
+ WeakMap的键名所指向的对象，不计入垃圾回收机制。 

```js
const e1 = document.getElementById('foo');
const e2 = document.getElementById('bar');
const arr = [
  [e1, 'foo 元素'],
  [e2, 'bar 元素'],
];
// 不需要 e1 和 e2 的时候
// 必须手动删除引用
arr [0] = null;
arr [1] = null;
```

​       WeakMap一个典型应用场景是，在网页的 DOM 元素上添加数据，就可以使用`WeakMap`结构。当该 DOM 元素被清除，其所对应的`WeakMap`记录就会自动被移除。

```js
let e1 = document.getElementById('myDiv');
let e2 = document.getElementById('yourDiv');
let wm = new WeakMap();
wm.set(e1,"myDiv");
console.log(wm);//WeakMap {div#myDiv => "myDiv"}
wm.set(e2,"yourDiv");
console.log(wm);//WeakMap {div#yourDiv => "yourDiv", div#myDiv => "myDiv"}

wm.set(e1,"myDiv").set(e2,"yourDiv");
console.log(wm);//WeakMap {div#yourDiv => "yourDiv", div#myDiv => "myDiv"}
```

WeakMap的键名所引用的对象都是弱引用，即垃圾回收机制不将该引用考虑在内。 

>注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用。 

```js
const wm = new WeakMap();
let key = {};
let obj = {foo: 1};

wm.set(key, obj);
obj = null;
wm.get(key)
// Object {foo: 1}
```

上面代码中，键值`obj`是正常引用。所以，即使在 WeakMap 外部消除了`obj`的引用，WeakMap 内部的引用依然存在。 

# 2、WeakMap 的语法 

WeakMap 与 Map 在 API 上的区别主要是两个 ：

+ 一是没有遍历操作 ，即没有`keys()`、`values()`和`entries()`方法 ，也没有`size`属性 
+ 二是无法清空，即不支持`clear`方法。 

因此，`WeakMap`只有四个方法可用：`get()`、`set()`、`has()`、`delete()`。 

# 3、WeakMap 的示例 

# 4、WeakMap 的用途

WeakMap 应用的典型场合就是 DOM 节点作为键名。 

```js
let myElement = document.getElementById('logo');
let myWeakmap = new WeakMap();

myWeakmap.set(myElement, {timesClicked: 0});

myElement.addEventListener('click', function() {
  let logoData = myWeakmap.get(myElement);
  logoData.timesClicked++;
}, false);
```

上面代码中，`myElement`是一个 DOM 节点，每当发生`click`事件，就更新一下状态。我们将这个状态作为键值放在 WeakMap 里，对应的键名就是`myElement`。一旦这个 DOM 节点删除，该状态就会自动消失，不存在内存泄漏风险。

WeakMap 的另一个用处是部署私有属性。

```js
const _counter = new WeakMap();
const _action = new WeakMap();

class Countdown {
  constructor(counter, action) {
    _counter.set(this, counter);
    _action.set(this, action);
  }
  dec() {
    let counter = _counter.get(this);
    if (counter < 1) return;
    counter--;
    _counter.set(this, counter);
    if (counter === 0) {
      _action.get(this)();
    }
  }
}

const c = new Countdown(2, () => console.log('DONE'));

c.dec()
c.dec()
// DONE
```

上面代码中，`Countdown`类的两个内部属性`_counter`和`_action`，是实例的弱引用，所以如果删除实例，它们也就随之消失，不会造成内存泄漏。 