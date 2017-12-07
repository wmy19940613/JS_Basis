
# JS基础(二)
## 函数
+ 一匿名函数
- 匿名函数就是没有名字的函数
```
function(){}//报错，需要和表达式使用`
 var foo = function(){}
```
- 一般在函数表达式内使用，不能单独存在

+ 二自调用函数
- 这个自调用函数会在书写的位置上执行一次
   `(function(){})()`

+ 函数的类型
- 检测方式是type of  函数的类型是undefined
- 函数注释的使用：在函数前输入/**点击回车，可以输入一些跟函数参数返回值相关的标注

+ 递归
- 函数在函数内调用自己，被称为递归
```
  function fun(){
    cosole.log("今天中午吃什么");
    fun();//在函数内调用自己，循环输出今天中午吃什么
    }
   fun();//在函数外调用时，输出今天中午吃什么，但使用递归的时候注意不要造成死循环（系统会崩掉）
```

## 对象
+ 生活中抽象和具体的关系，对象是一个具体的东西，每个对象都有自身的特征（属性）和行为（方法）
+ 创建对象方式：`var obj= {} 或  var obj=new Object()（单个对象的创建）`
+ 添加属性和方法通过 对象名.属性名 对象名.方法名
```
   obj.faceValue = “超高”; 
    方法跟属性的区别在于，方法中保存的是函数。 
    obj.sayHi = function(){ 
    alert(“你好”); 
    }; 
```
+ 创建多个对象的方法：
  - 方法一：构造函数（有new，有this）
     + 在调用构造函数的时候，调用前加new,构造 函数的作用是创建对象，在构造函数内需要做的一件事情就是添加属相和方法，
        使用this,this就是代表创建出来的对象
     + 构造函数的名字，首字母要大写
 ```
     function Person(name,age){
    this.name=name;
    this.age=age;
    this.sayhi=function(){
        alert("大家号我是"+this.name)
    }
  }
  var sisi=new Person("小明",18);
 ```
  - 方法二：对象的字面量形式
    + var obj={};对象的字面量，可以直接在{}内添加属性和方法，多个属性之间使用逗号分隔

  ```
      var obj={ 
      name:"小明", 
      age:"18", 
      sayhi:function(){} 
      }
  ```
+ 对象属性的访问方式：obj.name   或 obj["name"] 效果一样
+ 获取对象中所有的值：对象是一种无序的数据存储方式，想要获取对象中的所有值使用for in 
   - 方法：for... in 
  ```
   for(var key in obj){ 
      key 在forin中表示某一个属性名，是字符串格式 
      obj[key] 表示obj中key属性的属性值 
      }
  ```
  ```
  var obj={
    name:"小明",
    age:"18",
    sayhi:function(){}
    }
    for(var k in obj){
        console.log(obj[k]);
    }
  ```
+ json数据存储格式
 ```
  var obj = { 
  “name”:”张三” 
  };
 ```
+ 日期对象Date
 - var date= new Date()
 - 日期转换成毫秒
```
var date=+new Date();
var date1=Date.parse("2017-02-10");
```
 - Date常用方法
 ```
date的方法，不用记 
getTime() 返回毫秒数和valueOf()结果一样 
getMilliseconds() 
getSeconds() 返回0-59 
getMinutes() 返回0-59 
getHours() 返回0-23 
getDay() 返回星期几 0周日 6周6 
getDate() 返回当前月的第几天 
getMonth() 返回月份，从0开始 
getFullYear() 返回4位的年份 如 2016
 ```

## 数组
+ 数组的常用方法：
  `var arr=[1,2,3,4]`
  - arr.join()用于把数组中的所有元素放入一个字符串
  ```
  var arr = new Array(3)
  arr[0] = "George"
  arr[1] = "John"
  arr[2] = "Thomas"

  document.write(arr.join())//George,John,Thomas
  ```
  - arr.toString()把数组转换成字符串，不更改原数组
  ```
  var arr=[1,2,3,4];
  console.log(arr.tostring())//"1,2,3,4";
  console.log(arr.join("-"))//"1-2-3-4"
  ```
  - arr.push()可以项数组最后添加一个或多个新项，返回添加后的数组的元素个数。
  - arr.pop()从数组最后删除一个元素，并且返回删除的元素。
  - arr.unshift()从数组前面插入一个或多个元素，注意插入多个的顺序。 返回添加后的数组的元素个数
  - arr.shift()从数组前面删除一个 ，返回删除的元素
```
  var arr=[1,2,34];
console.log(arr.push(1,2));//5,返回插入后数组的个数
console.log(arr.pop());//2返回删除的元素
console.log(arr.unshift("1", 2));//6返回数组的个数
console.log(arr.shift());//"1"返回删除的元素
```
  - arr.reverse()翻转，可以将数组的所有元素翻转，改变原数组
  - arr.sort()排序，改变原数组对字符串排序是按照首字母排序。对数值排序也是按照第一位排序，想要正序或倒叙可以传入函数参数
```
var arr=[1,2,34];
arr.sort()//正序排序
arr.sort(function(a,b){
    return b-a;
})//倒序排序
arr.sort(function(a,b){
    return a-b;
})//正序排序
```
  - arr.slice(start,end)拷贝，接受两个参数 两个参数都是索引值，可以从arr中拷贝一部分元素，含start不含end。 返回拷贝的部分，不改变原数组
  - arr.splice(start,len,...)截取，start表示截取的起始位置，len表示要截取多少个元素，后面的所有参数是可选的，表示将后面的参数添加到删除掉的位置。返回删除的元素，改变原数组
  - arr.contact()复制，可以传入多个参数，连接在arr后，返回新数组，不改变原有数组。 
  复制数组：arr.concat(); 如果不传参数，也会返回一个和原数组相同的新数组
```
var arr1=[1,3,4,6];
var arr2=[10,3,4,6];
console.log(arr1.concat(arr2));//arr1和arr2连接
arr1.concat(1,2);//
arr1.concat()//相当于arr1的复制。
```
  - indexOf(参数1，参数2（可选）)
    + 参数1为要寻找的值，参数2可选，为寻找的起始位置。 返回找到的索引值（只能找到一个）。 
      如果没找到，返回-1.ie6-ie8的不兼容
  - astIndexOf(参数1，参数2（可选）)
    + 使用方式与indexOf相同，不同点为从数组最后开始查找。ie6-ie8不兼容
+ 清空数组的三种方式
```
arr.length = 0; 
arr.splice(0,arr.length); 
arr = []; 
```

