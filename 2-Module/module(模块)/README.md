### 什么是模块
module模式最初被定义为一种在传统软件工程中为类提供私有和公有封装的方法。
通过这种方式，可以使一个单独的对象拥有公有/私有方法和变量，从而屏蔽来自全局作用域的特殊部分。
module模式使用闭包封装“私有”状态，屏蔽处理底层事件逻辑的整洁解决方案，同时只暴露一个接口提供给其他人使用。

因为在js中没有真正意义上的公有私有概念，没有像后端那种修饰符。从技术上来说，我们不能称变量为公有私有，我们只是使用函数作用域来模拟这个概念，在module内，由于闭包的存在，声明的变量和方法只可以在该模式内部可用，但在返回对象上定义的变量和方法，则对外部使用者可用。

让我实现一个简单的计数器～～～～

```js
var firstModule = (function() {
    var count = 0;
    return {
        incrementCount: function (){
            return ++count;
        },
        resetCount: function (){
            console.log("now count" + count);
            count = 0;
        }
    }
})();
firstModule.incrementCount(); //1
firstModule.incrementCount(); //2
firstModule.incrementCount(); //3
firstModule.resetCount(); //now count 3
```
在上面代码中，count变量实际上螫与其他全局作用域隔离的，因此它表现的就像一个私有变量～，因为唯一能访问到count的就是incrementCount和resetCount这两个函数。

下面我们再来实现一个简单的购物车～

```js
var shopCart = (function(){
    var itemLIst = [];
    function doSomeThingPrivate(){
        // 干啥都行我就是一个栗子
        console.log('栗子一个')
    }
    return {
        addItem: function (values) {
            itemLIst.push(values)
        },
        getItemCount: function() {
            return itemLIst.length
        },
        doSomeThingPublic: doSomeThingPrivate,
        getTotal: function() {
            var itemCount = this.getItemCount(), total = 0;
            while (itemCount--) {
                total += itemLIst[itemCount].price;
            }
            return total
        }
    }
})();
shopCart.addItem({price: 10, item: 'apple'})
shopCart.addItem({price: 8, item: 'bread'})
console.log(shopCart.getTotal()) //18 
shopCart.getItemCount() //2

```