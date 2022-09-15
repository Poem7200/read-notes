# 函数式编程
------
## Arity
> 函数的“长度”是什么？
答：参数的个数
```js
const sum = (a, b) => a + b
console.log(sum.length) // 2
```

## 高阶函数 Higher-Order Function（HOF）
> 以函数为参数或/和返回值的函数
其实ES6内置的filter、map这些也是高阶函数
```js
const filter = (data, filterMethod) => data.filter(filterMethod)
const getType = type => item => Object(item) instanceof type
console.log(filter([0, '1', true], getType(Number))) // [0]
```
> 分析一下这个过程：

1. getType可以接受参数，即type，第二个参数其实**没有接收**，而是在调用过程中动态接收
2. 这个函数调用后返回了一个新的函数，也就是**item => Object(item) instanceof Number**，把这个函数传递给filter的回调方法

## 闭包
> 暂不添加

## 柯里化 Currying
> 把一个多元函数转变为一元函数，每次调用只接收一个参数并返回**带有一个参数的函数**，直到所有参数传递完成，返回结果
```js
// 正常的函数这么写
const add = (a, b) => a + b;
// 柯里化每次入参只有一个，返回新的函数，直到所有的参数都输入了，才输出结果
const curry = x => y => x + y;
console.log(curry(2)) // return anonymous function
console.log(curry(2)(3)) // 5
```

### 自动柯里化
（待补充）

## 函数组合 Function Composition
> 把两个函数放在一起，形成第三个函数，一个函数输入为另一个函数输出
```js
// 函数定义
const compose = (f1, f2) => a => f1(f2(a))
const floorAndToString = compose(val => val.toString(), Math.floor)
console.log(floorAndToString('12.12')) // '12'
```

## 后续 Continuation
> 一个程序执行的任意时候，尚未执行的代码即Continuation

常见的Continuation例如**异步请求数据的后续处理方法**

## 幂等
> 一个函数执行多次，都返回相同的结果，则是幂等的

例如数学中的**绝对值**
```js
f(f(x)) = f(x)
``` 


