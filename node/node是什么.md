
看[技术文档](https://github.com/i5ting/How-to-learn-node-correctly)，不太清楚`Node.js 是 js 运行时环境`
```
Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.
```

然后在[知乎](https://www.zhihu.com/question/39499036)，找到了答案，按照自己的理解解释一下

运行时环境包括两部分
+ 提供代码所需要的依赖库(如node的http,path...)。
+ 掌管程序执行的某些重要的方面，以保证程序执行的安全性。---> 这个东西也可以被称为`managed runtime(管理运行时)`
被掌管方面，例如
	+ 内存管理
	+ 代码执行