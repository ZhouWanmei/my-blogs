参考：

https://www.w3cplus.com/vue/vue-mixins.html

https://blog.csdn.net/qq_35285627/article/details/80804709

# #什么是mixins

​	通俗地讲，mixins就是封装一块在其他组建中都可以使用的函数，提高代码的复用率。如果被正确使用，它不会改变函数以外的东西，所以被多次调用，得到的都是一样的值。

> 类似于原生Js中的function.js/common.js文件的作用

Vue的官方文档是这样描述`mixins`的：

> `mixins`是一种分发Vue组件中可复用功能的一种灵活方式。

​	`mixins`是一个JavaScript对象，可以包含组件中的任意选项，比如Vue实例中生命周期的各个钩子函数，也可以是`data`、`components`、`methods`或`directives`等。在Vue中，`mixins`为我们提供了在Vue组件中共用功能的方法。使用方式很简单，将共用的功能以对象的方式传入`mixins`选项中。当组件使用`mixins`对象时，所有`mixins`对象的选项都将被混入该组件本身的选项。

# #怎样使用mixins

## （1）直接在组建中使用

```js
<template>
  <div id="app">
    <router-view/>
  </div>
</template>
<script>
const mixins = {
  created() {
    console.log("来自mixins的消息");
  }
}
export default {
  name: 'App',
  mixins: [mixins]
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

 此时可在控制台看到：

```
来自mixins的消息
```

## （2）全局使用

在根目录下创建一个名为mixins的文件夹，在文件夹内新建index.js文件

###  新建mixins文件

src/mixins/index.js

```js
export default {
    methods:{
      handleClick() {
        console.log("Clicked me");
      }
    }
  };
```

### 全局注册mixins

main.js

```js
import Mixin from './mixins';
Vue.mixin(Mixin);
```

### 使用mixins里的方法

test.vue

```js
<template>
    <div class="test">
        <el-button type="success" @click="handleClick">查询</el-button>
    </div>
</template>
<script>
export default {
   data() {
       return {}
   }
}
</script>

```

