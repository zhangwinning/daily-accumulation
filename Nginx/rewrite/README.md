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

  标记rewrite的类型

| 类型 | 解释 |
| :---: | :---: |
| last | 停止rewrite检测 |
| break | 停止rewrite检测 |
| redirect | 返回302临时重定向，地址栏会显示跳转后的地址 |
| pemanent | 返回301永久重定向，地址栏会显跳转后的地 |

* 比较flag标记位的last、break

  ```
  server {
          listen  8000 ;
          server_name localhost;
          root /root/opt/app/code;
          location ~^/break {
                  rewrite ^/break /test/  break;
          }
          location ~^/last {
                  rewrite ^/last /test/ last;
          }
          location /test/ {
                  default_type application/json;
                  return 200 '{"status":"success", "remote_addr": $remote_addr}';
          }
  }
  ```

  访问 \`/break\` 会匹配第一个location，标志位是 break ，这时nginx会找root目录下的/test/目录的index.html文件，如果没有，返回404，找到显示。



