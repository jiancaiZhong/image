[switchTab](#wx.switchtab(object-object)) 跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面

- [reLaunch](#wx.reLaunch(object-object)) 关闭所有页面，打开到应用内的某个页面
- [redirectTo](#wx.redirectto(object-object)) 关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面。
- [navigateTo](#wx.navigateto(object-object)) 保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面。使用 [navigateBack](#wx.navigateback(object-object)) 可以返回到原页面。小程序中页面栈最多十层。
- [navigateBack](#wx.navigateback(object-object)) 关闭当前页面，返回上一页面或多级页面。可通过 [getCurrentPages](https://developers.weixin.qq.com/miniprogram/dev/reference/api/getCurrentPages.html) 获取当前的页面栈，决定需要返回几层。

### wx.switchTab(Object object)

#### 功能描述

跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面

#### 参数

##### Object object

| 属性     | 类型     | 默认值 | 必填 | 说明                                                         |
| :------- | :------- | :----- | :--- | :----------------------------------------------------------- |
| url      | string   |        | 是   | 需要跳转的 tabBar 页面的路径 (代码包路径)（需在 app.json 的 [tabBar](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html#tabbar) 字段定义的页面），路径后不能带参数。 |
| success  | function |        | 否   | 接口调用成功的回调函数                                       |
| fail     | function |        | 否   | 接口调用失败的回调函数                                       |
| complete | function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

#### 示例代码

```js
// app.json
{
  "tabBar": {
    "list": [{
      "pagePath": "index",
      "text": "首页"
    },{
      "pagePath": "other",
      "text": "其他"
    }]
  }
}
```

```js
wx.switchTab({
  url: '/index'
})
```

### wx.reLaunch(Object object)

#### 功能描述

关闭所有页面，打开到应用内的某个页面

#### 参数

##### Object object

| 属性     | 类型     | 默认值 | 必填 | 说明                                                         |
| :------- | :------- | :----- | :--- | :----------------------------------------------------------- |
| url      | string   |        | 是   | 需要跳转的应用内页面路径 (代码包路径)，路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2' |
| success  | function |        | 否   | 接口调用成功的回调函数                                       |
| fail     | function |        | 否   | 接口调用失败的回调函数                                       |
| complete | function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

#### 示例代码

```js
wx.reLaunch({
  url: 'test?id=1'
})
```

```js
// test
Page({
  onLoad (option) {
    console.log(option.query)
  }
})
```

### wx.redirectTo(Object object)

#### 功能描述

关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面。

#### 参数

##### Object object

| 属性     | 类型     | 默认值 | 必填 | 说明                                                         |
| :------- | :------- | :----- | :--- | :----------------------------------------------------------- |
| url      | string   |        | 是   | 需要跳转的应用内非 tabBar 的页面的路径 (代码包路径), 路径后可以带参数。参数与路径之间使用 `?` 分隔，参数键与参数值用 `=` 相连，不同参数用 `&` 分隔；如 'path?key=value&key2=value2' |
| success  | function |        | 否   | 接口调用成功的回调函数                                       |
| fail     | function |        | 否   | 接口调用失败的回调函数                                       |
| complete | function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

#### 示例代码

```js
wx.redirectTo({
  url: 'test?id=1'
})
```

### wx.navigateTo(Object object)

#### 功能描述

保留当前页面，跳转到应用内的某个页面。但是不能跳到 tabbar 页面。使用 [wx.navigateBack](https://developers.weixin.qq.com/miniprogram/dev/api/route/wx.navigateBack.html) 可以返回到原页面。小程序中页面栈最多十层。

#### 参数

##### Object object

| 属性     | 类型     | 默认值 | 必填 | 说明                                                         |
| :------- | :------- | :----- | :--- | :----------------------------------------------------------- |
| url      | string   |        | 是   | 需要跳转的应用内非 tabBar 的页面的路径 (代码包路径), 路径后可以带参数。参数与路径之间使用 `?` 分隔，参数键与参数值用 `=` 相连，不同参数用 `&` 分隔；如 'path?key=value&key2=value2' |
| events   | Object   |        | 否   | 页面间通信接口，用于监听被打开页面发送到当前页面的数据。基础库 2.7.3 开始支持。 |
| success  | function |        | 否   | 接口调用成功的回调函数                                       |
| fail     | function |        | 否   | 接口调用失败的回调函数                                       |
| complete | function |        | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

###### object.success 回调函数

###### 参数

###### Object res

| 属性         | 类型                                                         | 说明                 |
| :----------- | :----------------------------------------------------------- | :------------------- |
| eventChannel | [EventChannel](https://developers.weixin.qq.com/miniprogram/dev/api/route/EventChannel.html) | 和被打开页面进行通信 |
