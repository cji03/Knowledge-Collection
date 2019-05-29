When u need to new some empty Array:

```js
Array.from({length: 5});
// [undefined, undefined, undefined, undefined, undefined]

Array.from(new Array(5));
// [undefined, undefined, undefined, undefined, undefined]

[...new Array(5)]
// [undefined, undefined, undefined, undefined, undefined]
```

Range function:

```js
function basicRange(n) {
  return [ ... Array(n).keys() ]
}

function baseRange(start, end, step) {
  var index = -1,
    length = Math.max(Math.ceil((end - start) / (step || 1)), 0),
    result = Array(length);

  while (length--) {
    result[++index] = start;
    start += step;
  }
  return result;
}
```
