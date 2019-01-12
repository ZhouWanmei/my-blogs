官网：https://leancloud.cn/

# 安装

```
# 存储服务（包括推送）
$ npm install leancloud-storage --save
# 实时消息服务
$ npm install leancloud-realtime --save
```

# 初始化配置

src/LeanCloud/index.js

```js
import AV from 'leancloud-storage'
var APP_ID = 'iSWsKBVbp4q41xrAfHzYcQtd-gzGzoHsz'
var APP_KEY = 'ERkg8SiC8uRSem4QwVmxNa5N'

AV.init({
  appId: APP_ID,
  appKey: APP_KEY
})
 
 export default AV
```

# 全局导入

src/main.js

```js
//云数据库
import lean from './LeanCloud/index.js'
Vue.prototype.$lean=lean
```

# 使用

如在登录时：

```js
this.$lean.User.logIn(this.validateForm.username, this.validateForm.password).then(function (loginedUser) {
          router.push('./main');
        }, function (error) {
          alert(JSON.stringify(error));
        });
```

> 其他使用方法参照官方 文档：https://leancloud.cn/docs/leanstorage-started-js.html#hash1905932728