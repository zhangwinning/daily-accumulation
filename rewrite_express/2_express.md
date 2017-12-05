## 重写express\(二\)

继续实现express。

### 目标：实现一个路由

app.get\('/', \(req, res\) =&gt; res.send\('Hello World!'\) \);

### 预备知识

router 是express中一个非常重要的数据结构，它是作为一个大容器存在，一个应用只有一个实例，里面存放各个layer，代码是在

/lib/router/index.js中。











### 流程

看一段代码

```
app.get('/', (req, res) => res.send('Hello World!') );
```



