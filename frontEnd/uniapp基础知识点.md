## uniApp

[TOC]

### uniapp页面跳转的常用几种方式：

```
// 保留当前页，跳转到非tabbar页面，使用uni.navigateBack可以返回到原页面。
uni.navigateTo
// 关闭当前页，返回上一页面或多级页面。
uni.navigateBack
// 关闭当前页面，跳转到应用内的某个页面。
uni.redirectTo
// 跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面。
uni.switchTab
// 关闭所有页面，打开到应用内的某个页面。
uni.reLaunch
```

- `navigateTo`, `redirectTo` 只能打开非 tabBar 页面。

- `switchTab` 只能打开 `tabBar` 页面。

- `reLaunch` 可以打开任意页面。

- 页面底部的 `tabBar` 由页面决定，即只要是定义为 `tabBar` 的页面，底部都有 `tabBar`。

- 不能在 `App.vue` 里面进行页面跳转。

- H5端页面刷新之后页面栈会消失，此时`navigateBack`不能返回，如果一定要返回可以使用`history.back()`导航到浏览器的其他历史记录。

  

### uniapp传参的三种方式：

```
1. 通过URL进行传参，把要传递的信息拼接在url后面
优点：取值方便可以跨域，缺点：取值长度有限制，长度过大时会被截取掉
2. 将数据存储在本地缓存中，可以在一个页面中使用另一个页面的存储数据
3. 通过eventChannel向被打开页面传送数据
页面跳转时回调函数参数值包含一个eventChannel的对象
EventChannel.emit(string eventName, any args)
EventChannel.off(string eventName, function fn)
EventChannel.on(string eventName, function fn)
EventChannel.once(string eventName, function fn)
或者监听对象数据evetns:{}
```

### uniapp缓存：

```
// 将数据存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个异步接口。
uni.setStorage
// 从本地缓存中异步获取指定 key 对应的内容。
uni.getStorage
// 从本地缓存中异步移除指定 key。
uni.removeStorage
// 将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个同步接口。
uni.setStorageSync
// 从本地缓存中同步获取指定 key 对应的内容。
uni.getStorageSync
// 从本地缓存中同步移除指定 key。
uni.removeStorageSync
// 异步获取当前 storage 的相关信息。
uni.getStorageInfo
// 同步获取当前 storage 的相关信息。
uni.getStorageInfoSync
// 清理本地数据缓存。
uni.clearSorage
// 同步清理本地数据缓存。
uni.clearStorageSync
```

### uniapp请求

```
// 发起网络请求。
uni.request
// https 请求配置自签名证书
uni.configMTLS
// 将本地资源上传到开发者服务器，客户端发起一个 POST 请求，其中 content-type 为 multipart/form-data
uni.uploadFile
// 下载文件资源到本地，客户端直接发起一个 HTTP GET 请求，返回文件的本地临时路径。
uni.downloadFile
// 创建一个 WebSocket (opens new window)连接。
uni.connectSocket
uni.onSocketOpen
uni.onSocketError
uni.onSocketMessage
uni.sendSocketMessage
uni.closeSocket
uni.onSocketClose
```

```
// 发起网络请求。
uni.request({
	url: "",
	data: {},
	header: {},
	scuccess: (res) => {
		
	}
})
// 返回值
// 如果希望返回一个 requestTask 对象，需要至少传入 success / fail / complete 参数中的一个
var requestTask = uni.request({
	url: "",
	complete: () => {}
})
requestTask.abort()

// https 请求配置自签名证书
uni.configMTLS({
	certificates: [{
        'host': 'www.test.com',
        'client': '/static/client.p12',
        'clientPassword': '123456789',
        'server': ['/static/server.cer'],
    }],
    success ({code}) {}
})
```

### 获取dom元素方式：

```
// 查询节点信息的对象
const selectorQuer = uni.createSelectorQuery()
// 将选择器的选取范围更改为自定义组件 component 内，返回一个 SelectorQuery 对象实例。（初始时，选择器仅选取页面范围的节点，不会选取任何自定义组件中的节点）。
const query = selectorQuery.in(component)
// 在当前页面下选择第一个匹配选择器 selector 的节点，返回一个 NodesRef 对象实例，可以用于获取节点信息。
const nodeRef = selectorQuery.select(selector)
// 在当前页面下选择匹配选择器 selector 的所有节点，返回一个 NodesRef 对象实例，可以用于获取节点信息。
const nodeRef = selectorQuery.selectAll(selector)
// 选择显示区域，可用于获取显示区域的尺寸、滚动位置等信息，返回一个 NodesRef 对象实例。
const nodeRef = selectorQuery.selectViewport()
// 执行所有的请求。请求结果按请求次序构成数组，在callback的第一个参数中返回。
const nodeRef = selectorQuery.exec(callback)
// 获取节点的相关信息。第一个参数是节点相关信息配置（必选）；第二参数是方法的回调函数，参数是指定的相关节点信息。
nodesRef.fields(object,callback)
// 添加节点的布局位置的查询请求。相对于显示区域，以像素为单位。其功能类似于 DOM 的getBoundingClientRect。返回 NodesRef 对应的 SelectorQuery。
nodesRef.boundingClientRect(callback)
// 添加节点的滚动位置查询请求。以像素为单位。节点必须是 scroll-view 或者 viewport。返回 NodesRef 对应的 SelectorQuery。
nodesRef.scrollOffset(callback)
// 添加节点的 Context 对象查询请求。支持 VideoContext、CanvasContext、和 MapContext 等的获取。
nodesRef.context(callback)
// 获取 Node 节点实例。目前支持 Canvas 的获取。
nodesRef.node(callback)
```

**注意**

- nvue 暂不支持 uni.createSelectorQuery，暂时使用下面的方案

  ```
  <template>
    <view class="wrapper">
      <view ref="box" class="box">
        <text class="info">Width: {{size.width}}</text>
        <text class="info">Height: {{size.height}}</text>
        <text class="info">Top: {{size.top}}</text>
        <text class="info">Bottom: {{size.bottom}}</text>
        <text class="info">Left: {{size.left}}</text>
        <text class="info">Right: {{size.right}}</text>
      </view>
    </view>
  </template>
  
  <script>
    // 注意平台差异
    // #ifdef APP-NVUE
    const dom = weex.requireModule('dom')
    // #endif
  
    export default {
      data () {
        return {
          size: {
            width: 0,
            height: 0,
            top: 0,
            bottom: 0,
            left: 0,
            right: 0
          }
        }
      },
      onReady() {
      	 setTimeout(()=> {
  	        const result = dom.getComponentRect(this.$refs.box, option => {
  		    console.log('getComponentRect:', option)
  		    this.size = option.size
  		})
  		console.log('return value:', result)
  		console.log('viewport:', dom.getComponentRect('viewport'))
  	 }, 100);
       }
    }
  </script>
  ```

  

### 上拉加载，下拉刷新：

1，在pages.json ,当前页面syle中添加enablePullDownRefresh: true；

2, 在组件中使用onPullDownRefresh，下拉刷新;

// 开始下拉刷新，调用后触发下拉刷新动画，效果与用户手动下拉刷新一致。

uni.startPullDownRefresh 

uni.stopPullDownRefresh

3，onReachButtom页面滚动到底部的事件,上拉加载



节流和防抖：

```
// 防抖——触发高频事件后 n 秒后函数只会执行一次，如果 n 秒内高频事件再
次被触发，则重新计算时间；
function debounce(fn, time) {
    let timeout = null
    // 创建一个标记用来存放定时器的返回值
    return function() {
        clearTimeout(timeout)
        // 每当用户输入的时候把前一个 setTimeout clear 掉
        timeout = setTimeout(() => {
            // 然后又创建一个新的 setTimeout, 这样就能保证输入字符后的
            // interval 间隔内如果还有字符输入的话，就不会执行 fn 函数
            fn.apply(this, arguments)
        }, time)
    }
}
function sayHi() {
	console.log('防抖成功')
}
var inp = document.getElementById('inp')
inp.addEventListener('input',debounce(sayHi)) 

// 节流——高频事件触发，但在 n 秒内只会执行一次，所以节流会稀释函数的执行频率。
function throttle(fn) {
    let canRun = true // 通过闭包保存一个标记
    return function() {
        if (!canRun) return
        // 在函数开头判断标记是否为 true，不为 true 则 return
        canRun = false // 立即设置为 false
        setTimeout(() => {
            // 将外部传入的函数的执行放在 setTimeout 中
            fn.apply(this, arguments)
            // 最后在 setTimeout 执行完毕后再把标记设置为 true(关键) 表示可以执行
            // 下一次循环了。当定时器没有执行的时候标记永远是 false，在开头被 return 掉
            canRun = true
        }, 500)
    }
}
function sayHi(e) {
	console.log(e.target.innerWidth,e.target.innerHeight)
}
window.addEventListener('resize',throttle(sayHi))

```

 

### 虚拟列表实现：

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bd3e687f46e149c5aeb9e63de55ff026~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)