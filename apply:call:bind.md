### javascript-apply(); call();

主要作用是用来改变函数作用于，调用函数并改变本次函数执行时“this”的指向。

对于 apply、call 二者而言，作用完全一样，只是接受参数的方式不太一样。

```javascript
function add(a, b) {
  return a + b;
}
function addCall(a, b) {
  return add.call(this, a, b);
}
function addApply(a, b) {
  return add.apply(this, [a, b])
}

addCall(1, 2) //3
addApply(1, 2) //3
```

wang这个对象没有`sayName`这个方法，可以通过`call`或者`apply`来使用`chen`的方法。

```javascript
const chen = {
  name: 'chen',
  sayName: function() {
    console.log(this.name);
  }
}
const wang = {
  name: 'wang',
  age: 30,
  gender: 'male'
}

chen.sayName() //'chen'
chen.sayName.call(wang) //'wang'
chen.sayName.apply(wang) //'wang'
```

介于`max, min`并不接受`array`作为参数，可以利用`apply`来快速筛选。（方法并不依赖context，所以this部分可以用任意替代）

```javascript
const numbers = [5, 6, 2, 3, 7];
const max = Math.max.apply(null, numbers);
```
