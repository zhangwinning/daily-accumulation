## 重写express\(二\)

继续实现express。

### 目标：实现一个路由

app.get\('/test', \(req, res\) =&gt; res.send\('Hello World!'\) \)

### 预备知识

1、Array.prototype.slice.call\(argumens\);

把类数组对象转化为数组，并且返回转化后的数组。

```
function foo () {
      console.log(arguments)
      console.log(Array.prototype.slice.call(arguments))
      console.log(Array.prototype.slice.call(arguments, 1))
      console.log(arguments);
}
foo ('hello', 'world')

{ '0': 'hello', '1': 'world' }
[ 'hello', 'world' ]
[ 'world' ]
{ '0': 'hello', '1': 'world' }
```

2、require模块时，Node对模块进行缓存，第二次require时，是不会重复开销的。

### 流程

```
let express = require('./express');
let app = express();

app.get('/test', (req, res) => res.send('Hello World!'));
app.listen(3001, function () {
    console.log('the server is listening:', 3001);
});
```

路由get的添加分为三板斧

```
1、express()   //为应用添加各种请求方法
2、app.get('/test', (req, res) => {})  // 构建前端请求和后端处理程序的关联
3、createServer(app)  // 请求方法的执行，请求到来后，调用函数app()
```

具体实现

1、执行express后，会在app对象中添加各种请求方法。

2、

app\[method\] 函数会在调用路由中间件（例如 app.get\(\)）时执行。

    methods.forEach(function (method) {
        app[method] = function (path) {
            this.lazyrouter();  //新建一个`router`对象
            let route = this._router.route(path); //新建一个route并添加到刚刚建立的router的stack中，这里实际上是调用的`router`函数
            route[method].apply(route, slice.call(arguments, 1)); //为route添加stack
            return this;
        }
    });

```
this.lazyrouter() 
这个方法会创建router对象，而这个对象会一直绑定到应用的_router属性上，创建的router对象在每个应用中只有一个。
```











