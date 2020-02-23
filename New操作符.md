```javascript
const haha = new Person();

// haha.__proto__ = Person.prototype;
```

• 创建一个空对象，将它的引用赋给 this，继承函数的原型.
• 通过 this 将属性和方法添加至这个对象.
• 最后返回 this 指向的新对象，也就是实例.

```
let newMethod = function (Parent, ...rest) {
    // 1.以构造器的prototype属性为原型，创建新对象；
    let child = Object.create(Parent.prototype);
    // 2.将this和调用参数传给构造器执行
    Parent.apply(child, rest);
    // 3.返回第一步的对象
    return child;
};
```
