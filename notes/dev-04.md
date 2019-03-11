# 开发小记（四）

#### ~~base-start-vue 项目问题~~

~~`npm run build` 进行打包时，会失败，需要收到那个删除 `dist` 目录~~ 

**问题原因**：

删除了 register-service-worker 文件。

#### 问题 & 解决

1. 将固定写死的列表数据改成从接口获取，但接口返回的数据没有相对应图片地址的字段？

**解决方法**：将相关的图片地址保存到数组中，渲染列表数据时通过下标值来显示地址，如果存在则显示对应地址，否则显示默认图片。

2. 视频播放页的返回路径添加。在微信中打开分享链接，打开后能够返回到视频列表页。

**解决方法**：使用 widow.history 的 replace 、pushState 和 onpopstate 方法来实现。

```javascript
let page = "/t/list/"
let url = window.location.href
// 修改当前激活的历史记录条目
history.replaceState({
page: "list"
}, null, page), history.pushState({
page: "detail"
}, null, url), window.onpopstate = function(page) {
page.state && "list" === page.state.page && location.reload()
}
```

3. 点赞需求：站内站外两种情况，一天之内对每个用户自由一次的点赞机会。站内的根据 auid 来判断。处理的方法是使用 localStorage。

**解决方法**：

```javascript
// 获取存储中已经点过赞的 puid
let auidVoteList = JSON.parse(window.localStorage.getItem(key)) || []
// 将点过赞的 puid 加入
auidVoteList.push(item.puid)
// 重新存储
window.localStorage.setItem(key, JSON.stringify([...new Set(auidVoteList)]))
// 获取新的点赞列表
let newAuidList = window.localStorage.getItem(key)
//  更新 voteData
this.voteData = newAuidList ? JSON.parse(newAuidList) : []
```

