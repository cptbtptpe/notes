## Nginx

### set 指令

```
用于定义一个变量，并为变量赋值
作用范围为
    
    if
    location
    server

```

### if 指令

```
if( condition )
{
    ...
}

作用范围为如：
if ( $host ~ "linuxidc-taiwan-5" )
{
        set $linuxidc_name linuxidc5;
}

if 指令用于检查一个条件是否符合，如果条件符合，则执行大括号内的内容
if 指令不支持嵌套，不支持多个 && 或 ||

可以指定的条件为：

    变量名
    变量比较可以使用 = （等于）和 != （不等于）
    正则表达式匹配可以使用 ~（区分大小写匹配）和 ~* （不区分大小写匹配）
    !~ 和 !~* 则表示不匹配
    -f 和 !-f 用来判断文件是否存在
    -d 和 !-d 用来判断目录是否存在
    -e 和 !-e 用来判断文件或目录是否存在
    -x 和 !-x 用来判断文件是否可以执行
    
```

### nginx 内置变量

```
$host              请求的主机名
$request_filename  请求的文件名
```

### rewrite 指令

```
rewrite regex replacement flag;

用来重定向 URL

if ( !-e $request_filename )
{
    rewrite /(.*) /index.php last;
}

rewrite 最后一项为标记位， Nginx 支持的标记为有：

    last             表示完成 rewrite
    permanent        返回 301 永久重定向，浏览器地址栏会显示跳转后的 URL
    break            本条规则匹配完成后，终止其他规则的匹配
    redirect         返回 302 临时重定向

 
last 和 break 完成 URL 的重定向，浏览器上的地址不会变，但在服务器端上的位置发生了变化
permanent 和 redirect 用来实现 URL 跳转，浏览器地址栏会显示跳转后的 URL

使用 alias 指令时必须使用 last 指令
使用 proxy_pass 指令时必须使用 break 指令
```
