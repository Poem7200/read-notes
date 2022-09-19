# 你不知道的JavaScript阅读笔记

## Part1---作用域
### 编译查询
引擎查找变量分为LHS和RHS，这里的L和R相对于**赋值符号**而言
- LHS：查找变量，对其进行赋值操作
- RHS：获取变量的值（可以理解成“非左侧”）

### 异常
- ReferenceError：RHS从内向外一直找不到需要查找的变量，抛出的异常，和**作用域**相关
- TypeError：RHS可以找到，但是进行了错误的操作（非函数类型，执行函数） 

### 遮蔽效应
- 一般查找变量，都是从当前的局部作用域逐步向上查找，在这条链上，找到了就不再继续查找，即遮蔽
```js
var a = 1;
function test() {
  var a = 2;
  console.log(a); // 2
}
```
- 对于全局作用域的变量，可以用window属性来访问，以避开遮蔽效应的影响
- 另一种避开遮蔽效应的方法，就是使用eval和with进行作用域的**欺骗**

#### 欺骗词法
- eval：可以接受字符串作为参数，实现声明语句的传递（严格模式无效）
```js
function foo(str, a) {
  eval(str);
  console.log(a, b)
}
var b = 12;

foo('var b = 1', 2) // 2, 1
```

- with：
with基本的用法其实是给对象绑定属性（严格模式同样无效）
```js
var obj = {}
with(obj) {
  a = 1;
  b = 2;
  c = 3;
}
```
但是with的绑定，如果这个对象原先**没有这个属性**，则该属性也会被绑定到该对象**所处的作用域**上面