call、apply、bind

```
    使用一个函数需要改变this指向

    fn.call(thisObj, arg1, arg2 ...)
        传递的参数不多
    fn.apply(thisObj, [arg1, arg2 ...])
        传递的参数很多，则可以用数组将参数整理好使用
    const newFn = fn.bind(thisObj); newFn(arg1, arg2...)
        生成一个新的函数长期绑定某个函数给某个对象使用

```