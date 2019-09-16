### BFC

BFC ：block formatting context 块级格式化上下文

BFC 作用 ：

​	隔绝容器内部元素和容器外部元素的相互作用。

创建 BFC 的方法

1. 浮动
2. 绝对定位，position 为 absolute 或者 fixed
3. 行内块 inline-block
4. 表格单元格 display: table-cell;
5. overflow 不为 visible
6. 弹性盒 display: flex;

实际用法：

1. 清除浮动
2. 防止与浮动元素重叠
3. 利用 BFC 包含一个元素，避免边距重叠，margin collapse

### 垂直居中方案

1. ```css
   .middle {
     position: absolute;
     top: 0;
     bottom: 0;
     margin: auto;
   }
   ```

   

2. flex 布局

   ```css
   .middle {
     display: flex;
     justify-content: center;
     align-items: center;
   }
   ```

3. ```css
   .middle {
     display: table-cell;
     vertical-align: middle;
   }
   ```

   