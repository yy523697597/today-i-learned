## ES6

### 模块化

语法：import export

环境：使用 babel 编译ES6语法，模块化可以用 webpack 或者 rollup

### 常用功能：

1. let 	const 

   const 定义的变量无法修改

   ```js
   let name = "yu";
   const age = 26;
   age = 24; // 报错， Uncaught TypeError: Assignment to constant variable.
   ```

2. 块级作用域

   ```js
   if (true) {
     var a = 0;
   }
   console.log(a); // 0
   
   if (true) {
     let b = 1;
     const c = 2;
   }
   console.log(b); // 报错，Uncaught ReferenceError: b is not defined
   console.log(c); // 报错，Uncaught ReferenceError: c is not defined
   ```

3. class 类

   ```js
   class Parent {
     constructor(name) {
       this.name = name;
     }
     printName() {
       console.log(this.name);
     }
   }
   ```

4. 字符串模板

   ```js
   const name ='yu';
   let user = `my name is ${name}`; // "my name is yu"
   ```

5. async   await

   ```js
   async function getSource(id) {
     const res = await ce.get(id);
     console.log(res);
   }
   ```

6. 解构赋值

   ```js
   let obj = {
     a: 1,
     b: 2
   };
   
   let { a, b } = obj;
   console.log(a); // 1
   console.log(b); //2
   ```

7. 箭头函数

   **箭头函数在定义时，this就确定了，不是运行时指定的。**

   普通函数中，this是运行时确定的，很容易出现奇怪的问题

   ```js
   function arrow() {
     let realObj = this; // {name: yu }
     let arr = [1, 2, 3];
     arr.map(function(item) {
       console.log(this); // window
     });
     arr.map(item => console.log(this)); // {name: yu }
   }
   arrow.call({ name: "yu" });
   ```

8. 函数默认参数

   ```js
   function getName(name = "yu") {
     console.log(name);
   }
   getName();	// yu
   getName("gou");	// gou
   ```

   

9. Promise

   ```js
   function loadImg(src) {
     let promise = new Promise((resolve, reject) => {
       let img = document.createElement("img");
       img.onload = function() {
         resolve(img);
       };
       img.onerror = function() {
         reject(new Error("资源加载错误"));
       };
       img.src = src;
     });
     return promise;
   }
   let src = "https://qna.smzdm.com/201907/30/5d3fbd6ce29ad5187.jpg_a200.jpg";
   loadImg(src)
     .then(img => {
       console.log("width", img.width);
       // 这儿返回了 img，后面的 then 才能接受到 img
       return img;
     })
     .then(img => console.log("height", img.height))
     .catch(err => console.log(err));
   ```

   

