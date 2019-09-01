
#### DOM事件相关问题
**DOM 事件级别 ：**

DOM 0  : ele.onclick = function(){}

DOM 2  : ele.addEventListener('click',function(){})

DOM 3  : ele.addEventListener('keyup',function(){})  // 支持了更多的事件

**DOM 事件模型** ：捕获与冒泡

**DOM 事件流**  ： 捕获阶段 ---> 处于目标阶段  ----> 冒泡阶段

**描述DOM事件捕获的具体流程 **：

window ---> document ---> html ---> body ---> ....(目标父级元素) --->目标元素

**Event对象常见应用**：

```js
event.preventDefault() // 阻止默认事件
// 阻止后续节点的事件冒泡，不阻止当前元素的后续事件冒泡
// 阻止冒泡，比如父元素和子元素都绑定了点击事件，如果不想点击子元素时触发父级元素的点击事件，需要阻止冒泡
event.stopPropagation() 
// 执行完当前事件操作之后，阻止当前元素及后续节点的事件冒泡
// 如果给一个元素使用 addEventListener 同时注册了两个点击事件 A 和 B，在触发了A之后，不想出发B，那么在A中就应该使用此方法
event.stopImmediatePropagation(); // 立即阻止冒泡
// 使用父级元素代理事件的时候，currentTarget 指向父级元素，即事件绑定元素
event.currentTarget
// 使用父级元素代理事件的时候，currentTarget 指向触发事件的元素
event.target
```

**自定义事件：**

new Event() 和 new CustomEvent(),区别在于 CustomEvent 可以携带一个自定义数据

```js
// 自定义事件
const selfEvent = new Event("self");
const customEvent = new CustomEvent('custom',{age:18});

document.getElementById("selfButton").addEventListener("click", () => {
  document.dispatchEvent(selfEvent);
});
document.addEventListener("self", (e) => {
  console.log("slef事件触发了");
});
```

