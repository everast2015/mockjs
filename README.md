# hello-world

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

## 一、如何在项目中使用`mockjs` 和 `axios` (http 请求库)

```js
npm install mockjs axios --save-dev
```

## 二、`mockjs`

在根目录`src`下，新建一个`mockdata.js` 文件
```js
const Mock = require('mockjs') // 获取mock对象
const Random = Mock.Random // 获取random对象，随机生成各种数据，具体请翻阅文档
const domain = 'http://mockjs.com/api' // 定义默认域名，随便写
const code = 200 // 返回的状态码

// 随机生成文章数据
const postData = req => {
  
  console.log(req) // 请求体，用于获取参数

  let posts = [] // 用于存放文章数据的数组
  
  for (let i = 0; i < 1000; i++) {
    let post = {
      title: Random.csentence(10, 25), // 随机生成长度为10-25的标题
      author: Random.cname(), // 随机生成名字
      date: Random.date() + ' ' + Random.time() // 随机生成年月日 + 时间
    }

    posts.push(post)
  }
  
  // 返回状态码和文章数据posts
  return {
    code,
    posts
  }
}

// 定义请求链接，类型，还有返回数据
Mock.mock(`${domain}/posts`, 'get', postData);
```

## 三、`main.js` 中

```js
import Mock from './mockdata.js' // 刚刚手写的mock.js文件
import axios from 'axios' // axios http请求库

axios.defaults.baseURL = 'http://mockjs.com/api' // 设置默认请求的url
Vue.prototype.$http = axios // axios 放到原型链上，方便后期使用
```

在组件`mounted` 生命周期中使用
```js
  this.$http.get('/posts').then(res => {
      console.log(res.data.posts)
      this.datalist = res.data.posts
    })
```