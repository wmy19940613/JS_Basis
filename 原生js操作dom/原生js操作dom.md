## 原生JS操作dom（用js来控制页面中的标签）
+ javascript分为三个部分

 1. ECMAScript基础语法（核心）：提供核心语言功能
 2. DOM(document object model)（文档对象模型）：提供访问和操作网页内容的接口和方法。
 3. BOM（浏览器对象模型）：提供和浏览器交互的方法和接口。
 
+ Dom:Dom给我们提供了一些方法，让我们可以使用js来控制页面中的标签
+ 常用的dom方法：
 - document.getElementById('box');//通过id获取标签
 - document.getElementsByTagName("div");//通过标签名获取页面元素
 - document.getElementsByclassName("box1")//根据类名class获取页面元素
 - window.onload()中的代码会在页面完全加载后执行。
 > 注意：
    由于获取结果可能是多个，element后面要加s根据标签获取的结果是伪数组形式，伪数组是不具备数组的方法。要操作伪数组中的所有元素需要遍历伪数组。根据标签名获取元素时，有可能获取到的标签只有一个，但是形式还是伪数组。根据标签名获取时，document可以更换为任意标签.在box中获取li标签。
 > 注意： 根据id获取的时候，前面只能写document
 ```
   //想要获取box中的li,首先获取box
   var box = document.getElementByID("box");
   var lisBox = box.getElementsByTagName("li");
   console.log(lisBox);
   for(var i=0;i<lisbox.length;i++) {
      lisbox[i].innerHtml="我是box中的li";
   }
 ```
+ 设置标签的样式方法：
   - 对标签的样式设置使用.style
   - 设置标签的内容： .innerHtml
```
var box=document.getElementById("box");
box.style.width="100px";
box.style.backgroundColor="#ff00000"//带有短横线的属性要是用驼峰命名的方式。
```
`box.innerHtml="haha"`
+ 事件类型
  - 点击事件 onclick
  - 鼠标移入 onmouseover
  - 鼠标移除 onmouseout
+ 类名属性： 访问标签的类名属性通过 标签.className
+ 标签默认事件：某些标签具有默认的效果，有时候我们不想要这种效果，可以在事件最后加上return false
```
 link.onclick = function() {
   alert('今天天气好');
   return false;//通过returnfalse 取消标签的默认效果
 }
```
+ 循环添加事件：当我们进行循环添加事件的时候，在事件内部不能使用i，因为i的值已经是循环的结束条件那个值了（根据循环设置的具体情况而定）。
```
<script>
var box=document.getElementsByClassName("box");
for(var i=0;i<box.length;i++){
    box[i].onclick=function () {
        alert(this.innerHTML);
    }
}
</script>
```
+ 焦点事件：
```
onfocus 文本框获取焦点时触发事件 
onblur 失去焦点时触发事件 
表单的常用属性： 
input获取内部文本 使用value ipt.value
```
+ 表单的属性：（不太常用）禁用表单 ipt.disabled 可以给表单禁用。设置值为true表示禁用，false表示启用复选框选中 cb.checked 值为true表示选中 值为false表示没选中 下拉菜单选中 doudou.selected 值为true表示选中，为false表示没选中

