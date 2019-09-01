
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
