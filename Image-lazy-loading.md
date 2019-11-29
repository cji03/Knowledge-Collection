### `IntersectionObserver`

使用web提供的API，它可以帮助track监听的element是否进入到当前viewport视窗中。来帮助实现图片的懒加载，在用户滑到特定的image后加载当前image。

默认情况下用一张placeholder的图片做站位，或者用css做一个loading的动画效果做站位。在`img`元素进入视窗后，替换src为真实展示的图片地址。

```html
<img class="lazy" src="https://res.cloudinary.com/drp9iwjqz/image/upload/e_blur:2000,f_auto,q_auto:eco/v1508291830/jeremywagner.me/using-webp-images/tacos-1x.jpg" data-src="https://res.cloudinary.com/drp9iwjqz/image/upload/f_auto,q_auto/v1508210556/jeremywagner.me/using-webp-images/tacos-2x.jpg" alt="">
```

```javascript
document.addEventListener("DOMContentLoaded", function() {
  const lazyImages = [].slice.call(document.querySelectorAll("img.lazy"));
  console.log(lazyImages)

  if ("IntersectionObserver" in window && "IntersectionObserverEntry" in window && "intersectionRatio" in window.IntersectionObserverEntry.prototype) {
    const lazyImageObserver = new IntersectionObserver(function(entries, observer) {
      entries.forEach(function(entry) {
        if (entry.isIntersecting) {
          const lazyImage = entry.target;

          lazyImage.src = lazyImage.dataset.src;
          lazyImage.classList.remove("lazy");
          lazyImageObserver.unobserve(lazyImage);
        }
      });
    });

    lazyImages.forEach(function(lazyImage) {
      lazyImageObserver.observe(lazyImage);
    });
  }
});
```

https://developers.google.com/web/updates/2016/04/intersectionobserver?hl=zh-CN[google的文档介绍]
https://w3c.github.io/IntersectionObserver/#intersection-observer-api[webapi介绍]
https://codepen.io/malchata/pen/YeMyrQ?editors=1010[codepen]
https://caniuse.com/#search=intersectionobser[目前的浏览器支持度还不错]
