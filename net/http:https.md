
## HTTP 状态吗  
200 OK  <br/>
301/302/303都表示 重定向 <br/>
301 永久重定向 <br/>
302 临时重定向 <br/>
303 请求资源路径发生变化 <br/>

301 和 302 有共同点的，就是用户都可以看到url替换为了一个新的，然后发出请求<br/>
301比较常用的场景是使用域名跳转。<br>
比如，我们访问 http://www.baidu.com 会跳转到 https://www.baidu.com 发送请求之后，就会返回301状态码，然后返回一个location，提示新的地址，浏览器就会拿着这个新的地址去访问。 


405 method not allowed <br/>  
请求的方式（get、post、delete）方法与后台规定的方式不符合。<br/>  

415 
后台程序不支持提交的content-type，