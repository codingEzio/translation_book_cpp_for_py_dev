
### 6.7. 将流作为参数传入函数 <small>(Passing Streams as Parameters)</small>
> 在以上程序中，不管是输入还是输出流，我们都是以传引用的方式传给文件的。眨眼一看看起来可能很奇怪，但是转眼一想，我们只要想进行读写操作，传入的 *流* 就必须改变。简单说，当数据在通过这个 *流* 流动时，它会不可避免地发生变化。正因如此，但凡是涉及 *流* 的操作（比如文件流）都会是以传引用的方式来传递的。
