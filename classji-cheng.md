### 基本用法

举个栗子：

```js
// class声明，定义一个‘类’
class Info {
  // 构造方法
   constructor(name, age, work) {
     this.name = name;
     this.age = age;
     this.work = work;
   }
  // 私有属性
   _workInfo = {
     company: 'ctrip',
     team: 'cruise'
  }
  // 私有方法
   _getInfo() {
     return `我是${this.name}，今年${this.age}，工作是${this.work}`;
   }   
   // 实例方法
   getAllInfo() {
     return `${this._getInfo()};${this.workInfo}` // this.workInfo相当于一个实例属性
   }
   // getter
   get workInfo (){
     return `公司是${this._workInfo.company}，项目组${this._workInfo.team}，工号${this._workInfo.employeeNumber || '未知'}`;
   }
   // setter
   set workInfo (employeeNumber){
     this._workInfo.employeeNumber = employeeNumber;
   }
 }

 let mineInfo = new Info('haobin',18,'web前端');
 mineInfo.workInfo = 'S72768'; 
 console.log(fooInfo.workInfo); // 公司是ctrip，项目组cruise，工号S72768
 console.log(mineInfo.getAllInfo()); // 我是haobin，今年18，工作是web前端;公司是ctrip，项目组cruise，工号S72768
```

### 继承

ES5 的继承，实质是先创造子类的实例对象`this`，然后再将父类的方法添加到`this`上（`Parent.apply(this)`）。ES6 的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到`this`上面（所以必须先调用`super`方法），然后再用子类的构造函数修改`this`。

如果这段话没看懂，那就使用继承时，直接下面的代码：

```

class Foo extends B.ar {
   constructor(...args.) {
     super(...args);
     // some code
   }
   // some code
 }
```



