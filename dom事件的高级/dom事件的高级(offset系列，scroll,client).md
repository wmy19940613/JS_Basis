## 动漫的高级补充（offset，scroll，client）
+ offset系列
 - offsetWidth和offsetHeight: 用来得到对象的大小
 - offsetWidth和style.height的区别：
   + demo.style.height只能获取行内样式，如果样式写到了其他的地方，甚至根本就没写，便无法获取。
   + style.height是字符串，并且带单位，offsetHeight是数值
   + demo.style.height可以设置行内样式，offsetHeight是只读属性
   + 所有一般用demo.offsetHeight来获取某元素的真是宽度或高度，用demo.style.height来设置宽度或高度。
   + 
 - offsetHeight的构成：offsetHeight=height+上下padding+上下border(不包括上下外边距margin)
 - offsetwidth同理
 - offsetLeft:距离自身最近的（带有定位的）父元素的 左侧/顶部 的距离 
 - offsetTop:距离自身最近的（带有定位的）父元素的 左侧/顶部 的距离 
     > 注意：没有offsetRight和offsetBottom
     > 如果所有的飞机都没有定位则以body为准
     > offsetLeft 是自身border左侧到父级padding左侧的距离
 - offsetLeft和style.left的区别：
   + style.left只能获取行内样式
   + offsetLeft是只读，style.left可读可写
   + offsetLeft是数值，style.left是字符串并且有单位px
   + 如果没有加定位，style.left获取的数值可能是无效的
   + 最大区别在于offsetLeft以border左上角为基准，style.left以margin左上角为基准
 - offsetParent:表示某个标签外面定位的父盒子（不一定是父节点，也可能是爷爷）
 > 注意：区分offsetParent 和 parentNode
```
console.log(box2.offserParent)//可能是定位的干爹，最近的一个定位的父元素 
console.log(box2.parentNode)//一定是亲爹 
```
 > 所有的属性都是只读属性，获取的结构是数值类型
+ scroll系列
  - scrollHeight和scrollWidth:标签内部实际内容的高度或宽度
    + 不计算外框，如果内容不超出盒子，值为盒子的宽高（不带边框）
  - scrollTop和scrollLeft:被卷去部分的顶部/左侧 到可视区域顶部/左侧的距离
  - 获取页面滚动坐标
    + 页面滚动坐标非常常用：但是有很大的兼容性问题，可以合写为
    ```
    var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0; 
    ```
    + 封装自己的scroll(): 由于很常用，每次都写上面一堆很麻烦，所以模仿jQuery封装一个自己的scroll()方法，返回页面滚动坐标
  ```
  //通过下面这个函数可以得到页面卷曲的高度/宽度
  function scroll () {
           return {
              scrollTop:window.pageYOffset || document.documentElement.scrollTop||ducument.body.scrollTop||0,
              scrollLeft:window.pageXOffset || document.documentElement.scrollLeft||ducument.body.scrollLeft||0,
           }
     }
  ```
    + 固定导航案例：
      - 当页面向下滚动的时候 进行判断 如果页面向上走的距离 大于导航栏到页面顶部的距离时 将导航栏的定位改为固定定位 
      - 小问题：当导航栏改为固定定位的一瞬间，后面的元素会塌陷。解决方案：给下面的元素添加数值为导航栏高度的padding-top
  + client系列
    - clientWidth和clientHeight:
      + 总结：偏移offsetWidth: width + padding + border 
              卷曲scrollWidth: width + padding 不包含border 内部内容的大小 
              可视clientWidth: width + padding 不包含border
    - clientTop和clientLeft:
      + clientTop和clientLeft没用 ,他们就是borderTop和borderLeft（如果有滚动条会包含滚动条的宽度，但谁见过滚动条在顶部或者左侧的？！）
  + 网页可视区宽高：
    - 网页可视区宽高的兼容写法：页面可视区宽高非常有用，但是有很大的兼容性问题，可合写为：
  ```
  var clientWidth = window.innerWidth|| document.documentElement.clientWidth|| document.body.clientWidth|| 0;
  ```
    - 封装自己的client():封装自己的scroll(): 由于很常用，每次都写上面一堆很麻烦，所以模仿jQuery封装一个自己的client()方法，返回可是去宽度和高度
```
function client(){
    return clientWidth : window.innerWidth|| document.documentElement.clientWidth|| document.body.clientWidth|| 0,
    clientHeight = window.innerHeight|| document.documentElement.clientHeight|| document.body.clientHeight|| 0;
}
``` 
 + 体会响应式布局的原理：当我们的页面宽度 大于 960 像素的时候 页面为红色并显示computer 当我们的页面宽度 大于 640 小于 960 页面为绿色并显示tablet 剩下的页面为蓝色并显示mobile
 + 三大系列总结：
 ```
  offsetWidth     scrollWidth    clientWidth
  offsetHeight    scrollHeight    clientHeight
  offsetLeft      scrollLeft      clientLeft
  offsetTop       scrollTop       clientTop
  offsetParent    scroll()        client()
  //offsetWidth=padding+border+内容
  //scrollWidth=border
 ```
