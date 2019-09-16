参考网站：https://segmentfault.com/a/1190000012186439#articleHeader6

1、找到一个vue项目，安装一些依赖包

```
npm install element-ui --save  （回车）
npm install vuex --save  （回车）
npm install axios --save  （回车）
npm install mysql --save  （回车）
npm install express --save  （回车）
npm install body-parser --save  （回车）
npm install node-sass --save-dev  （回车）
npm install sass-loader --save-dev  （回车）

//可以一起安装：
npm install element-ui vuex axios mysql express body-parser --save  （回车）
npm install node-sass sass-loader --save-dev  （回车）
```

2、新建文件夹与src平级

```
在 /server 下创建文件

db.js 数据库连接配置
api.js 连接数据库，各种方法实现
sqlMap.js sql语句
router.js 后端 express 路由配置
index.js 后端入口文件，启动后端服务
```

3、/server/index 入口文件（node index.js启动服务，默认3000）
```
const path = require('path');
const express = require('express');
const app = express();

app.get('/api/getArticle', (req, res, next) => {
  res.json({
    data: {
      'name':'李梦月',
      'sex':'女'
    }
  })
})

// 监听端口
app.listen(3000);
console.log('success listen at port:3000......');

```
4、解决跨域问题（前台80，后台30会产生跨域）/config/index.js
```
'/api': {
        target: 'http://localhost:3000/api',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
    },
```
