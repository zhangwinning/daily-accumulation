Nginx 的rewrite 规则

* 作用

     实现URL的重写以及匹配的URL重定向。

* 配置语法

```
Syntax: rewrite regex replacement [flag];
Default: --
Context: server, location, if
```

* 正则表达式

小括号（） 用于匹配括号之间的内容，通过 $1、$2 调用

```
if ($http_user_agent ~ MSIE) {
     rewrite ^(.*)$  /msie/$1 break;
}
//访问的路径放到$1上
```



