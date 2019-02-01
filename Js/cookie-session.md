# cookie机制

Cookie技术是客户端的解决方案，Cookie就是由服务器发给客户端的特殊信息，而这些信息以文本文件的方式存放在客户端.请求时Cookie信息则存放在HTTP请求头（Request Header）了.
Cookie就是这样的一种机制。它可以弥补HTTP协议无状态的不足.
# cookie是什么
cookie是一段字符串,每个cookie 都含有name/value,
cookie是一个个键值对（“键=值”的形式）加上分号空格隔开组合而成， 形如： "name1=value1; name2=value2; name3=value3"
# 设置cookie
```
document.cookie="name="+username;  
```
# JS读取cookie
```
var username=document.cookie.split(";")[0].split("=")[1]
```
# 写cookie
```
function setCookie(name,value) 
{ 
    var Days = 30; 
    var exp = new Date(); 
    exp.setTime(exp.getTime() + Days*24*60*60*1000); 
    document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString(); 
} 
```