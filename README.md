
### 作用域和闭包

------

**说一下对变量提升的理解：**

使用 var 定义的变量和函数声明，都会被提升到代码的最顶端。

使用 let 和 const 声明的变量不会。

```js
console.log(a); // undefined
var a = 100;

fn(); // 12
function fn() {
  console.log(12);
}
---------------------------------
var a;
console.log(a); // undefined
a = 100;

function fn() {
  console.log(12);
}
fn(); // 12
---------------------------------
console.log(a); // Uncaught ReferenceError: a is not defined
let a = 100;

console.log(a); // Uncaught ReferenceError: a is not defined
const a = 100;

```

**说明 this 几种不同的使用场景：**

1. 构造函数中使用：this 指向 new 运算符创建的空对象

   ```js
   function Foo(name) {
     // this 指向 new 运算符创建的空对象
     this.name = name;
   }
   let user = new Foo("yu");
   
   ```

2. 普通函数中使用，this 指向 window

   ```js
   var a = 10;
   function print() {
     // this 指向 window
     console.log(this.a); // 10
   }
   print();
   ```

3. 对象中使用，this 指向该对象

   ```js
   let obj = {
     name: "yu",
     getName() {
       console.log(this.name);
     }
   };
   obj.getName();
   ```

4. 使用 call、apply、bind时，this 指向传入的对象

   ```js
   let obj = {
     name: "yu",
     age: 26,
     getNameAndAge(age) {
       console.log(this);
       console.log(this.name);
       console.log(age);
     }
   };
   obj.getNameAndAge.call({ name: "gou" }, 25); 
   // { name: "gou" }  gou   25
   // apply 传参数要用数组的形式
   obj.getNameAndAge.apply({ name: "mi" }, [23]);
   // { name: "mi" }  mi  23
   
   let print = function() {
     console.log(this.name);
   }.bind({ name: 'yui' });
   print() // yui
   ```

**总结：this 的指向是在运行时确定的，而不是定义时候**



**作用域相关：**

自由变量：当前作用域中未定义的变量

作用域链：当要获取一个变量的值的时候，先判断是否能在当前作用域获取，如果不能再往上级作用域寻找，直到window

```js
// 创建10个a标签，点击的时候弹出相应的序号：
for (var i = 0; i < 10; i++) {
  (function(i) {
    let a = document.createElement("a");
    a.innerHTML = i + "<br/>";
    a.addEventListener("click", e => {
      e.preventDefault();
      console.log(i);
    });
    document.body.appendChild(a);
  })(i);
}
```

**闭包：**闭包主要是为了防止污染变量

1. 函数作为返回值

   ```js
   function printFn() {
     var a = 100;
     return function() {
       console.log(a);
     };
   }
   
   var a = 20;
   var print = printFn();
   print(); // 100
   ```

2. 函数作为参数传递

   ```js
   function F1() {
     var a = 10;
     return function() {
       console.log(a);
     };
   }
   var a = 30;
   var f1 = F1();
   function f2(fn) {
     var a = 20;
     fn();
   }
   f2(f1); // 10
   ```

```js
// 实际开发中闭包的用法
function isFirstLoad(id) {
  let _list = [];
  return function() {
    if (_list.includes(id)) {
      return false;
    } else {
      _list.push(id);
      return true;
    }
  };
}
let firstLoad = isFirstLoad();
firstLoad(10); // true
firstLoad(10); // false
```

**总结：函数和变量的作用域是在定义的时候就确定了的，和运行环境无关。**
