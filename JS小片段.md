#### Copy to Clipboard

使用web api，`document.execCommand`

```javascript
export function copyToClip(content) {
  const aux = document.createElement('input');

  aux.setAttribute('value', content);
  document.body.appendChild(aux);
  aux.select();
  document.execCommand('copy');
  document.body.removeChild(aux);
}
```

#### 下载二进制文件流到xlsx

设置api的`responseType=blob(或者ArrayBuffer)`

使用`a`标签下载流文件

```javascript
filename = res['Content-Type']
// 文件类型可以从response中获取

const downloadFile = (filename, text) => {
  const blob = new Blob([text], {
      type: 'application/octet-stream',
  });
  const url = window.URL.createObjectURL(blob);
  const element = document.createElement('a');
  element.setAttribute('href', url);
  element.setAttribute('download', filename);
  element.style.display = 'none';
  document.body.appendChild(element);
  element.click();
  document.body.removeChild(element);
};
```
