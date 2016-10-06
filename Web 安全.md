  
## Web 安全  
  
  
> Cross Site Scripting - 跨站脚本攻击 - XSS  
  
* XSS满足条件  
    * 在URL中输入的值在页面有有输出  
    * 输出最好是在 script 标签内  
  
* 通过 document.cookie 获取当前用户的 cookie 信息，该 cookie 必须是非 httponly 状态才能用 javascript 代码获取  
* HTML URL 编码  
    * " => %22  
    * ; => %3B  
    * 可以使用 escape('x') 函数获取字符的 URL 编码  
* HTML 实体编码  
    * < => <  
    * > => >  
    * " => "  
* 扩展攻击之蠕虫攻击  
    * 通过攻击页面，然后在页面中再次嵌入该攻击 URL 进行扇形扩展式攻击  
  
> Cross Site Request Forgery - 跨站请求伪造 - CSRF  
  
* 通过点击隐藏连接执行用户本意不想执行的 URL，该 URL 一般含某些动作  
  
> SQL 注入  
  
* 关键字  
    * 注释：username=xxx --  
    * 条件：username=xxx OR 1=1  
    * 条件：username=xxx || 1=1  
    * 截断：username=xxx'; DROP TABLE `users`;  
    * 合并：username=xxx UNION SELECT * FROM `users`;  
  
> 上传文件漏洞 - 适用于 php web 服务器  
  
* 需要满足文件上传前和上传后的文件名称一致的条件  
* 预先准备一个 hello.phpabc.jpg  
* 表面是 jpg 图片文件，其内容为 php 代码  
* 在上传的时候可使用抓包工具 fiddler 软件修改 header 信息，将文件名修改为 * hello.php;abc.jpg，甚至可以修改文件的 mime 类型  
* 该文件可以通过 php 服务器的正常验证，当在 move_upload_files 时该文件会自动保存为 hello.php  
* 然后就可以通过 url 访问该 php 文件执行其中的 php 代码了  
