# hello-world

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

如何在项目中使用`mockjs` 和 `axios` (http 请求库)

```js
npm install mockjs axios --save-dev
```

`mockjs`

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

`main.js` 中

```js

```