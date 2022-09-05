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
>> 1.getType可以接受参数，即type，第二个参数其实**没有接收**，而是在调用过程中动态接收
>> 2.这个函数调用后返回了一个新的函数，也就是**item => Object(item) instanceof Number**，把这个函数传递给filter的回调方法
