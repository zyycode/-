1. fixed 失效问题

   在写弹窗样式时，使用了 fixed 定位，发现不受控制。发现原因是因为同时使用了 transform 属性。

   > **当元素祖先的 transform 属性非 none 时，定位容器由视口变为祖先。**

   比如，我的一个弹窗容器的 transfrom 属性非 none 时，同时该容器中的关闭按钮也使用 fixed 来定位，会发现按钮不是相对于视口来定位，而是改容器。

   失效原因：**Stacking Context — 堆叠上下文**

[不受控制的 position: fixed](https://www.cnblogs.com/coco1s/p/7358830.html)



2. 有三张图片，点击替换图片，同时已点击过的图片变为默认。

   我是在图片上绑定事件，先将图片地址变为默认，然后用 e.target.src 改变当前图片。但是发现已点击过的图片不能改变。

   **总结**：在使用 vue 中不用直接操作 DOM，应该把操作抽象到数据，使用数据驱动模式。

   在第二种方案中，将每个图片都绑定一个变量，通过改变变量来改变图片的路径，但是感觉有些冗余。

   因此选用循环来实现，只需要判断点击元素和当前元素的下标是否相等。

```html
<!-- 一 -->
<div class="item">
    <img @click="selectBattery(5, $event)" :src="batImgSrc" alt="gift-battery">
    <p>+10</p>
</div>
<div class="item">
    <img @click="selectBattery(10, $event)" :src="batImgSrc" alt="gift-battery">
    <p>+10</p>
</div>
<div class="item">
    <img @click="selectBattery(15, $event)" :src="batImgSrc" alt="gift-battery">
    <p>+15</p>
</div>

<!-- 三 -->
<div class="item" v-for="(item, index) in batImgList" :key="item.id">
  <img
    @click="selectBattery(item.num, index)"
    :src="index === activeIndex ? giveBatImg : giveNoBatImg"
    alt="gift-battery-1"
  >
  <p>{{item.num}}</p>
</div>
```

```javascript
// 一
selectBattery(num, e) {
  this.batImgSrc = giveNoBat
  e.target.src = giveBat
},
// 二
selectBattery(num) {
  this.batImgSrc1 = giveNoBat
  this.batImgSrc2 = giveNoBat
  this.batImgSrc3 = giveNoBat
  console.log(num)
  switch (num) {
    case 5: this.batImgSrc1 = giveBat; break;
    case 10: this.batImgSrc2 = giveBat; break;
    case 15: this.batImgSrc3 = giveBat; break;
  }
},
// 三
selectBattery(num, index) {
  this.activeIndex = index
},
```



中东视频接口：

用户（auid）和 视频的电池数量

用户参赛视频中 其它用户赠送的电池数量以及赠送者信息（头像）



用户的观看视频数量和转发视频数量



逻辑：

1. 倒计时，时间过不能领电池和赠送电池

2. 用户每天进入播放视频和转发次数 清零

3. 领电池：

   ？时间是否是每天，是否前端做限制（有问题）

   登陆获取 5 个（任务一）

   播放 5 个 视频及以上获取 5 个 （任务二）

   转发 1 个视频及以上获取 5 个 （任务三）

   别人赠送的电池的显示，没有则显示文案

4. 赠送视频

   用户自己电池数量减少，对应视频的电池数量增加

5. 参赛视频展示

   若登陆用户为参赛用户则展示用户的参赛视频





1. 从输入 URL 到页面加载发生了什么？
2. JS 基础语法，闭包，原型，this





