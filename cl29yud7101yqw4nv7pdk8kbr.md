## type 和 interface 的区别是什么？

1. 组合方式: interface 使用extends来实现继承，type 使用&来实现联合类型。
2. 扩展方式: interface 可以重复声明用来扩展，type 一个类型只能声明一次
3. 范围不同: type 适用于基本类型，interface 一般不行。
4. 命名方式: interface 会创建新的类型名，type 只是创建类型别名，并没有新创建类型。