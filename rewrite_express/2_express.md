## 重写express\(二\)

继续实现express。

### 目标：实现一个路由

app.get\('/', \(req, res\) =&gt; res.send\('Hello World!'\) \)

### 预备知识

1、Array.prototype.slice.call\(argumens\);

把类数组对象转化为数组，并且返回转化后的数组

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

2、require模块时，Node对模块进行缓存，第二次require时，是不会重复开销的

### 流程

看一段代码

```
app.get('/', (req, res) => res.send('Hello World!') );
```

从表面看来，get方法可以将url中的path与后台程序关联起来，是不是这样呢，看看

#### 添加请求方法

app对象中请求方法是在application.js的以下代码中添加的，而app\[method\]会在调用路由中间件时执行。

    methods.forEach(function (method) {
        app[method] = function (path) {
            this.lazyrouter();  //新建一个`router`对象
            let route = this._router.route(path); //新建一个route并添加到刚刚建立的router的stack中，这里实际上是调用的`router`函数
            route[method].apply(route, slice.call(arguments, 1)); //为route添加stack
            return this;
        }
    });



