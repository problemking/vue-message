# vue-message

> vue+php+mysql实现留言

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

```
## 跨域的解决

#在数据接口文件中加入

header("Access-Control-Allow-Origin: *");//如果需要设置允许所有域名发起的跨域请求，可以使用通配符 * 

header('Access-Control-Allow-Headers: X-Requested-With,X_Requested_With'); 

## 格式化后台穿过来的时间戳

Vue.filter('time', function (value) {

   return new Date(parseInt(value) * 1000).toLocaleString().replace(/年|月/g, "-").replace(/日/g, " ");
   
})

在vue2,0中，过滤器只能用在插值表达式中{{}},去掉了1.0版本的内置过滤器，需要自定义过滤器。

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
