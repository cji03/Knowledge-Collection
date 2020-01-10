> 基本类型：number, string, boolean, undefined, null, symbol
> 对象 Object

### typeof

```javascript
typeof '' //"string"
typeof undefined //"undefined"
typeof null //"object"
typeof 11 //"number"
typeof true //"boolean"
typeof Symbol() //"symbol"
typeof [] //"object"
typeof {} //"object"
typeof function() {} //"function"
typeof new Date() //"object"
typeof Number(11) //"number"
typeof new Number(11) //"object"
```

1. 除了null被判定为object之外的基本类型，都可以正确判断结果。
2. 对于引用类型，除了function被判断为function之外，都判断为object类型。

### instanceof

> instanceof检测的是原型, 只能用来判断两个对象是否有实例关系，不能用来作类型判断。

```javascript
'ssdfsa' instanceof String //false
new String() instanceof String //true
[] instanceof Array //true
[] instanceof Object //true
```

> Array.isArray() 可以用来判断Array类型。

### toString()

toString() 是 Object 的原型方法，调用该方法，默认返回当前对象的 [[Class]] 。这是一个内部属性，其格式为 [object Xxx] ，其中 Xxx 就是对象的类型。

对于 Object 对象，直接调用 toString()  就能返回 [object Object] 。而对于其他对象，则需要通过 call / apply 来调用才能返回正确的类型信息。

```javascript
Object.prototype.toString.call('')  // [object String]
Object.prototype.toString.call(1)  // [object Number]
Object.prototype.toString.call(true) // [object Boolean]
Object.prototype.toString.call(Symbol()) //[object Symbol]
Object.prototype.toString.call(undefined) // [object Undefined]
Object.prototype.toString.call(null) // [object Null]
Object.prototype.toString.call(new Function()) // [object Function]
Object.prototype.toString.call(new Date()) // [object Date]
Object.prototype.toString.call([]) // [object Array]
Object.prototype.toString.call({}) //[object Object]
```
