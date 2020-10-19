## 什么是构造器？
假设我们是react技术栈的开发者，在我们提起构造器时候往往出现在脑海里面的是constructor( )，那么这个constructor 和我们今天要学习的构造器有什么异同呢？ 我们先了解一下constructor

### 类的constructor
#### 在es6中，我们通过class来实现，举个例子

```js
class People{
    //构造方法constructor就等于上面的构造函数People
    constructor(name = 'wenbo', age = '18'){
        this.name = name;
        this.age = age;
    }

    sayName(){
        return '我的名字是：'+this.name;
    }
}
//创建新的子类p1
let p1 = new People('harrisking',23); //输出p1为 {name: "harrisking", age: 23}
let p2= new People(); //输出p1为 {name: "wenbo", age: 18}
```

其实class方法完全就是对象原型的语法糖,效果是完全一样的,构造方法constructor( )其实就是构造函数本身

我们在衍生一个非常熟悉的例子如下

```js
// 我们用一个男人继承一个people。
class man extends People{
    constructor(name,age,sex){
        super(name,age);//调用父类的constructor(name,age)
        this.sex = sex;
    }
    haha(){
        return this.sex + ' ' + super.sayName();//调用父类的sayName() 
    }
}
var s = new man('wen1', '19', '男'); // 输出s为 {name: "wen1", age: "19", sex: "男"}
s.haha()  // 输出为 "男 我的名字是：wen1"

// 上面例子是不是似曾相识？我们经常写的react语法。剖析开来，一个男人继承了一个人（people）的名字和年龄，所以不需要在写this.name=name 和 this.age=age
```
#### 那么我们用ES5实现一下

```js
//构造函数People
function People (name,age){
    this.name = name;
    this.age = age;
    this.sayName = function(){
        return '我的名字是：'+this.name;
    }
}

//创建新的子类p1
let p1 = new People('harrisking',23); // 输出 p1{name: "harrisking", age: 23, sayName: ƒ} 其中__proto__ 中只有constructor 和__proto__ 

// 上面是一个简单的构造器，但是它有一些问题，
// 1、它使继承变得困难 ，像sayName这样的函数是为每个使用people构造器创建的新对象而分别定义的，如果我们要改sayName会变得困难，这不是最理想的，这种函数应该在所有people类型实例间共享。
// 所以我们可以如下实现。
function People (name,age){
    this.name = name;
    this.age = age;
}
People.prototype.sayName = function(){
    return '我的名字是：'+this.name;
}

var p1 = new People('王一博', 18);
var p2 = new People('肖战', 18);

p1.sayName() // "我的名字是：王一博"
p2.sayName() // "我的名字是：肖战"

People.prototype.sayName = function(){
    return '我的名字是：'+this.name + '并且长得帅！！！人见又人爱';
}
p1.sayName()  // "我的名字是：王一博并且长得帅！！！人见又人爱"
p2.sayName()   // ...
```
