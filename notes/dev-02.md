# 开发小记（二）

### 伪元素不能设置大小

在给每个视频框的左上角加一个小徽章时，我选择用伪元素 after 来做，但是在移动端适配时发现，安卓和 iOS 图片显示的大小不一致。

```less
&::after {
    content: url("../assets/star-1.png");
    width: 1.24rem;
    height: 1.106667rem;
    position: absolute;
    top: 0;
    left: 0;
}		
```

**问题：** 伪元素里的 content 是不能设置大小的，解决办法通过将图片设置为背景图片来进行设置。

```less
&::after {
    content: '';
    width: 1.24rem;
    height: 1.106667rem;
    background-image: url("../assets/star-1.png");
    background-size: 1.24rem 1.106667rem;
    position: absolute;
    top: 0;
    left: 0;
}
```

### 请求图片资源无法加载

在安卓和 iOS 上请求图片时，发现有些图片加载不出来。原因安卓不能加载 htttp 请求的图片资源，所以解决办法将 http 改成 https 可通过字符串来操作。

```javascript
let url = 'http://www.baidu.com'
url.replace('http://', 'https://')
// 最好匹配 http:// 如果匹配 http 的话，就会将 https://www.baidu.com 更改为 httpss:// www.baidu.com
```

### 事件捕获

需求：给父元素绑定一个事件，来切换两个子元素之间的显示，当点击子元素时不触发事件。

```html
<div id="div1">
    <div>btn1</div>
    <div>btn2</div>
</div>
```

```javascript
let div = document.getElementById('div1')
div.addListenListener('click', (e) => {
    if (e.target.id === 'div1') {
        // code here...
    }
})
```

