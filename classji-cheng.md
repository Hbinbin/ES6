### 定义

ES6引入类的概念，作为对象的模板。通过`class`关键字，可以定义类。

基本用法

```js
// class声明，定义一个‘类’
class Info {
  // 构造方法：相当于ES5的构造函数
   constructor(name, age, work) {
     this.name = name;
     this.age = age;
     this.work = work;
   }
  // 私有属性：只在类内部使用的私有属性
   _workInfo = {
     company: 'ctrip',
     team: 'cruise'
  }
  // 私有方法：只在类内部调用的私有方法
   _getInfo() {
     return `我是${this.name}，今年${this.age}，工作是${this.work}`;
   }   
   // 实例方法：每个实例都可调用的方法
   getAllInfo() {
     return `${this._getInfo()};${this.workInfo}` // this.workInfo相当于一个实例属性
   }
   // getter：获得类的某一个属性
   get workInfo (){
     return `公司是${this._workInfo.company}，项目组${this._workInfo.team}，工号${this._workInfo.employeeNumber || '未知'}`;
   }
   // setter：设置类的某一个属性
   set workInfo (employeeNumber){
     this._workInfo.employeeNumber = employeeNumber;
   }
   // 静态方法：适合做工具函数，可被子类继承，子类可通过super调用
   static address() {
     return '凌空SOHO'
   }
 }

 let mineInfo = new Info('haobin',18,'web前端');
 mineInfo.workInfo = 'S72768'; 
 console.log(fooInfo.workInfo); // 公司是ctrip，项目组cruise，工号S72768
 console.log(mineInfo.getAllInfo()); // 我是haobin，今年18，工作是web前端;公司是ctrip，项目组cruise，工号S72768
 console.log(Info.address()); // 不可用于new关键字的实例，直接通过类调用
```

### 继承

ES5 的继承，实质是先创造子类的实例对象`this`，然后再将父类的方法添加到`this`上（`Parent.apply(this)`）。ES6 的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到`this`上面（所以必须先调用`super`方法），然后再用子类的构造函数修改`this`。

super作为函数使用时，只能用在子类的构造方法中。

```js
class Foo extends Bar {
   constructor(...args) {
     super(...args);
     // some code
   }
   // some code
 }
```

super作为对象使用时，在静态方法之中指向父类，在普通方法之中指向父类的原型对象。

理解：class里的static静态方法，不会被实例继承，是直接通过类来调用；

```js
class Parent {
  static foo(msg) {
    console.log('static', msg);
  }
  bar(msg) {
    console.log('instance', msg);
  }
}

class Child extends Parent {
  static foo(msg) {
    super.foo(msg);
  }
  bar(msg) {
    super.bar(msg);
  }
}

Child.foo(1); // static 1
var child = new Child();
child.bar(2); // instance 2
```



