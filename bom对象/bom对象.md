## bom对象的知识总结
+ bom的基础知识
  - Bom - 浏览器对象模型
  - bom给我们提供了一些方法让我们可以使用浏览器的一些功能
  - bom的顶级对象是window，window的属性和方法都可以不加window进行使用
  - window的一些常用方法有：alert(),window(),confirm(),prompt()(上面的提示词，默认文本)
+ 全局变量
  - 设置了全局变量，这个变量就相当于window的一个属性
  ```
  var num=100;//此处的num是一个全局变量。
  //设置了一个全局变量，这个全局变量就相当于是window的一个属性
  window.num;
  ```
+ open()和close()额方法
    + window.open(url,target,param)参数均为字符串格式
      - url:要打开的地址
      - target:新窗口的位置_blank  _self
      - param:新窗口的一些设置 "width=300,height=200"
      - 返回值：新窗口的window对象
      - window.close()关闭窗口，使用哪个window对象进行调用，就关闭谁
  ```
  window.open("http://www.baidu.com","_blank");
  //第三个参数不传就是和当前窗口大小一样
  ```
+ localtion属性
```
location.href  跳转
location.assign(url) 跳转到新页面
location.replace(url) 跳转到新页面，无法回退
location.href和location.assign的作用是一样的。
location.reload(); 刷新页面
console.log(window.location.href);//地址栏的地址
console.log(window.location.hash);//#+锚点（不包括？号后面的）
console.log(window.location.host);//ip+端口
console.log(window.location.hostname);//ip或者是域名
console.log(window.location.pathname);//端口后面的地址
console.log(window.location.port);端口
console.log(window.location.protocol);//协议
console.log(window.location.search);//?+后面的参数
```
+ navigator属性
```
window.navigator.userAgent 获取一些浏览器的信息 
window.navigator.platform 运行平台 
platform 属性是一个只读的字符串，声明了运行浏览器的操作系统和（或）硬件平台。 
虽然该属性没有标准的值集合，但它有些常用值，比如 “Win32”(windos操作系统)、”MacPPC（mac）” 以及 “Linuxi586”，等等。 
```

+ history属性
```
history.go(1) 表示前进一个页面 
history.go(-1) 表示后退一个页面 
history.forward() 表示前进 
history.back() 表示后退 
```
+ 定时器
  - setTimeout(要执行的代码，设定的时间)超时，在时间到达时触发设置的代码
```
var timer= setTimeout(function(){},1000); 
```
  - 清除定时器Timeout:clearTimeout(定时器的标识)我们一般将定时器保存在变量中，以便清除使用
```
clearTimeout(timer);
```
+ setInterval(执行的代码，间隔时间)每隔一段时间执行代码
```
var timer=setInterval(function(){},1000);
```
+ 清除定时器
```
clearInterval(timer);
```
