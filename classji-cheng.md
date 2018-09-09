举个栗子：

```js
class Info {
  // 私有属性
   _workInfo = {
     company: 'ctrip',
     team: 'cruise'
  }
  // 私有方法
   _getInfo() {
     return `我是${this.name}，今年${this.age}，工作是${this.work}`;
   }
   // 构造方法
   constructor(name, age, work) {
     this.name = name;
     this.age = age;
     this.work = work;
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

1.从此js多了一种声明方式：class

