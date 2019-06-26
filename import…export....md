## export 和 export default

1. export与export default均可用于导出常量、函数、文件、模块等。
2. 导出时export可以有多个，export default只有一个。
3. 通过export方式导出，导入时用{...}方式解构；export default方式，导入为整体。
4. export能直接导出变量表达式，export default不行。
 
```javascript
export const a = '...'
export const doSomething = () => { 
  ...
}
function doSomething2(){
  ...
}

export { doSomething2 }
-----------------------
import { doSomething, doSomething2, a } from '...'
```

```javascript
const b = '...'
const doSomething = () => { 
  ...
}
export default { b, doSomething }
------------------------
import something from '...'
// something = { b, doSomething }
```
