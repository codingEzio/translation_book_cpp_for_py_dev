
### 6.2. 成员方法与精度控制
> 一个与特定类型的对象相关的函数一般被称为对象的成员方法。以下是一些关于成员方法的示例：
```cpp
// 此处的 setf 即为 cout 的成员方法; setf 代表 set flags
// 将默认使用科学计数法的行为改变为定长的小数点精度
cout.setf(ios::fixed)

// 不管有没有必要必须显示小数点精度
cout.setf(ios.::showpoint)

// 将精度限制在小数点后两位
cout.precision(2);
```
