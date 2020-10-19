### 什么是对象字面量
什么是字面量？ 用于表达源代码中一个固定值的表示法。
所以对象字面量可以理解为我们通常理解的对象。
我们通常认为对象是这样的

```js
var WYB = {
    name:'王一博',
    nike: '王甜甜',
    sex: '男',
    age: 18
}
```

下面我们看另一种有趣的写法，我们也是常见的。

```js
var WYB = {
    name: '王一博',
    config: {
        islikeDog: true
    },
    // 基本方法输出信息
    getLikePeople: function() {
        console.log('like XMT');
    },
    // 根据当前配置输出信息
    getIslikeDog: function(){
        console.log(`${this.config.islikeDog? 'yes' : 'no'}`)
    },
    // 重写当前的配置
    resetConfig: function(newConfig) {
        if(typeof newConfig === "object"){
            this.config = newConfig
            console.log(this.config);
        }else{
            console.log('is not object');
        }
    }
}
WYB.getIslikeDog() // yes
WYB.resetConfig({islikeDog: false})
WYB.getIslikeDog()  //no

```
好玩吧～～～让我在实现一个简单的购物车～～ 是不是爱上了设计模式～

因为模块是引用了对象字面量的概念～所以先讲了一个对象字面量，下面我们引出模块，后面我们在简单的实现一个购物车～

