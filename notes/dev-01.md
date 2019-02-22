# 开发小记（一）

### UI 部分

主要通过使用定位来完成。

**弹框注意点：** 可以将所需要展示的内容放在 mask 里，这样就可以通过 mask 来显示弹框。

### 逻辑部分

##### API 接口

- 用户视频观看次数和分享次数

**注意点：** 由于后端没有清除掉用户前一天的观看分享的次数，所有前端要通过 cookie 来进行处理。设置两个新老观看次数，次数通过相减来得到。

```javascript
if (wactchTimesOld) {
    Cookie.set('watchTimesNew', api.times, {
        expires: xxx
    })
} else {
    Cookie.set('watchTimesOld', api.times, {
        espires: xxx
    })
}
if (wactchTimesOld && watchTimesNew) {
    watchTimes = Number(watchTimesNew) - Number(watchTimesOld)
} else {
    watchTimes = 0
}
```

- 完成任务的用户次数

  在五个方框内显示，如果次数不满五个则以 0 填充。解决办法：将数字转换为字符串，使用 [padStart](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padStart) 方法 。

  **注意点：** 因为之后需要将完成任务的用户次数相加，所以要进行相同的操作。

- 获取设备的 `duid`

##### 功能点

- 首次打开页面时弹框，之后不显示

通过 cookie 或者 localStorage 实现，第一次显示时存入值，之后判断该值是否存在。

```javascript
let firstLogin = window.localStorage.getItem('firstLogin')
if (!firstLogin) {
    // 显示弹框
    window.localStorage.setItem('firstLogin', true)
}
```

### Learning

- 使用图片替换时，直接更改 imgSrc 为相对路径的值时不生效的，需要 import 导入，在 data 中声明在使用。

```vue
<img :src="imgSrc" >
// 使用
<script>
	import imgBg from '../assets/...'
    export default {
        data() {
            return {
                imgBg: imgBg
            }
        }
    }
</script>
```

