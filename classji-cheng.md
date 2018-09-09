举个栗子：

```js
class Info {
   _workInfo = {
     company: 'ctrip',
     team: 'cruise'
 }
   _getInfo() {
     return `我是${this.name}，今年${this.age}，工作是${this.work}`;
   }
   constructor(name, age, work) {
     this.name = name;
     this.age = age;
     this.work = work;
   }
   getAllInfo() {
     return `${this._getInfo()};${this.workInfo}`
   }
   get workInfo (){
     return `公司是${this._workInfo.company}，项目组${this._workInfo.team}，工号${this._workInfo.employeeNumber || '未知'}`;
   }
   set workInfo (employeeNumber){
     this._workInfo.employeeNumber = employeeNumber;
   }

 }

 let fooInfo = new Info('haobin',18,'web前端');
 fooInfo.workInfo = 'S72768';
 console.log(fooInfo.getAllInfo());
```



