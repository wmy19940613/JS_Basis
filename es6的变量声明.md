## es6变量的声明方式
+ 保留了var和function,新增了let,const,class,import
+ let 
```
 ------------
    let
  ------------
  1、let只在所在的代码块中有效
  for (var i = 0; i < 10; i++) {}
  console.log(i); //10

  for(let j = 0; j < 10; j++) {}
  console.log(j);// Error: j is not define

  2、以前我们需要用IIFE解决的问题
  for (var i = 0; i < 5; i++) {
    setTimeout(function () {
      console.log(i); // 输出5次5
    },0);
  }
  for (var k = 0; k < 5; k++) {
    (function (k) {
      setTimeout(function () {
        console.log(k); //输出0,1,2,3,4
      },0);
    })(k);
  }
  for (let j = 0; j < 5; j++) {
    setTimeout(function () {
      console.log(j); //输出0,1,2,3,4
    },0);
  }

  3、不存在变量声明提升
  console.log(foo); // 输出undefined
  console.log(bar); // 报错ReferenceError

  var foo = 2;
  let bar = 2;
  可能动手实践的同学会发现在webpack配置的es6环境中。
  并不会出现这种情况，那主要是babel转码是还是讲let转成了var,不要纠结这个。

  4、暂时性死区TDZ
  var temp = 123;
  if (true) {
    //TDZ start
    temp = "abc"; //ReferenceError
    console.log(temp); //ReferenceError
    //TDZ end
    let temp;
    console.log(temp); //undefined

    temp = 12;
    console.log(temp); //12
  }
  其实这个也可以解释上面那条 不存在变量声明提升。
  同时在TDZ区域中使用typeof temp 也是不安全的。
  但是你typeof 未声明的变量 倒是返回undefined, 这就是TDZ的效果。
  同样这里你也可能试验不出来，你看一下bundle.js,你就懂了。

  5、let不允许重复声明
  {
    let a = 1;
    let a = 10; //这里在转码的时候就报错了。
  }
```
+ const
```
 ----------
    const
  ----------
  1、大部分与let差不多。

  2、const （只读）（一旦声明必须赋值）  
  const MAX = 123;
  MAX = 1; //转码阶段就爆错了。

  3、对于复合类型变量 (可以给他的属性赋值)
  const a = {};
  a.name = "dai";
  a.age = 21;

  4、如何你不想添加属性
  const b = Object.freeze({});
  b.name = 'dai'; //TypeError
```
```
插曲–ES6引入了块级作用域 
其实这也解释了为什么let、const在自己所在的代码块有效了。

  {
    var b = 1;
    {
      var b = 10;
      console.log(b); //10
    }
    console.log(b); //10
  }

  {
    let a = 1;
    {
      let a = 2;
      console.log(a); //2
    }
    console.log(a); //1
  }
```
+ class
```
---------
    class
  ---------
  1、class作为es6的语法糖，实际上es5也可以实现的。
  class Point {
    constructor (x, y) {
      this.x = x;
      this.y = y;
    }
    toString () {
      return this.x + ',' + this.y;
    }
  }
  //上面是一个类
  Object.assign(Point.prototype, {
    getX () {
      return this.x;
    },
    getY () {
      return this.y;
    }
  })
  let p1 = new Point(1,2);
  console.log(p1.toString()); //1,2
  console.log(p1.getX()); //1
  console.log(p1.getY()); //2
  console.log(Object.keys(Point.prototype)); // ["getX", "getY"]  

  (1)、方法之间不需要逗号分隔
  (2)、toString () {} 等价于 toString: function () {}
  (3)、你仍然可以使用Point.prototype
  (4)、你可以用Object.assign()一次性扩展很多方法
  (5)、类内部定义方法多是不可以枚举的
  (6)、constructor(){}是一个默认方法，如果没有添加，会自动添加一个空的。
  (7)、constructor默认返回实例对象（this），完全可以指定返回其他的对象。
  (8)、必须用new调用
  (9)、不存在变量提升
  (10)、当用一个变量去接受class时，可以省略classname
  (11)、es6不提供私有方法。

  2、使用extends继承
  class ThreeDPoint extends Point {
    constructor (x, y, z) {
      console.log(new.target); //ThreeDPoint
      super(x, y);
      this.z = z;
    }

    toString () {
      return super.toString() + ',' + this.z;
    }

    static getInfo() {
      console.log('static method');
    }

    get z() {
      return 4;
    }
    set z(value) {
      console.log(value);
    }
  }
  ThreeDPoint.getInfo(); // "static method"
  let ta = new ThreeDPoint(2,3,4);
  console.log(ta.toString()); //2,3,4
  console.log(ta.z); // 4
  ta.z = 200; // 200
  console.log(Object.getPrototypeOf(ThreeDPoint)); //Point

  (1)、constructor中必须调用super,因为子类中没有this,必须从父类中继承。
  (2)、子类的__proto__属性总是指向父类
  (3)、子类的prototype属性的__proto__总是指向父类的prototype
  (4)、Object.getPrototypeOf()获取父类
  (5)、super作为方法只能在constructor中
  (6)、super作为属性指向父类的prototype.
  (7)、在constructor中使用super.x = 2，实际上this.x = 2;但是读取super.x时，又变成了父类.prototype.x。
  (8)、原生构造函数是无法继承的。
  (9)、get set 方法可以对属性的赋值和读取进行拦截
  (10)、静态方法不能被实例继承。通过static声明
  (11)、静态属性只能 ThreeDPoint.name = "123" 声明 （与static没什么关系）
```
+ import
```
 -----------
    import
  -----------
  1、ES6引入了自己的模块系统。通过export导出，import导入。
  2、与CommonJS不同的是，它是获取模块的引用，到用的时候才会真正的去取值。

  3、例如student.js中:
  let student = [
    {
      name: 'xiaoming',
      age: 21,
    },
    {
      name: 'xiaohong',
      age: 18
    }
  ]
  export default student; // 这种导出方式，你可以在import时指定它的名称。  

  4、在app.js中我们就可以这样用:
  import StudentList from './student.js'; //指定名称
  console.log(StudentList[0].name); //xiaoming
```
