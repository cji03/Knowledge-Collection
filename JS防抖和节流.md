### 防抖

> 触发事件n秒后执行方法一次，如果在n秒内再次触发事件，重新n秒倒计时。防止方法被多次执行。

```html
<input id="username">
```

```Javascript
function debounce(fn) {
  let timeout = null

  return () => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      fn.apply(this, arguments)
    }, 500)
  }
}

function doThings() {
  console.log('防抖成功')
}

var input = document.getElementById('username')
input.addEventListener('input', debounce(doThings))
```

### 节流

> 触发事件n秒内方法只会执行一次，如果在n秒内再次触发事件，不执行方法。

```javascript
function throttle(fn) {
  let lock = false

  return () => {
    if (lock) return

    lock = true
    fn.apply(this, arguments)
    setTimeout(() => {
      lock = false
    }, 1000)
  }
}
```
