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
//代理是MSIN的，如果是/test.html ,会跳转到/msin/test.html 页面中
```

* flag 标记位

标记rewrite



