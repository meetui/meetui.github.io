# 条形码

> 更新时间 2020-07-01


此组件为条形码，默认条形码的颜色是黑色，如果需要颜色则需要传对应的参数详情可参考下面的示例

### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;App&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;H5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|微信小程序|支付宝小程序|百度小程序|头条小程序|QQ小程序|
|:----:|:----:|:----: |:----:|:----: |:----: |:----:|
|√ |√  |√ |√ | √| √| √|

只要是使用`uni-app`进行开发，凡是支持`canvas`画布的都支持此组件

## 如果使用脚手架方式

```js
//vue.config.js里面添加如下配置
module.exports = {
    transpileDependencies: [
        /[/\\]node_modules[/\\](.+?)?@uni-ui(.*)[/\\]code-plugs/
    ]
}
```

> [!ATTENTION]
> Nvue不支持此组件，使用方式请参考[Nvue](/plugs/web/nvue/#Nvue)

### 基本使用

请确定在`pages.json`里面配置了`easycom`。如果没有请前往当前文档的：使用方式->组件方式里面的配置。如已经配置请忽略

```html
<template>
	<w-barcode :options="options"></w-barcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					width: 670, // 宽度 单位rpx
					height: 100, // 高度 单位rpx
					code: 'E57890543271985',// 生成条形码的值
				},
			}
		},
	}
</script>

```

### 修改颜色

```html
<template>
	<w-barcode :options="options"></w-barcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					width: 670, // 宽度 单位rpx
					height: 100, // 高度 单位rpx
                    color: ['#45B649','#00c3ff', '#ee0979'], //默认黑色 如果传入多个则颜色渐变
					code: 'E57890543271985',// 生成条形码的值
				},
			}
		},
	}
</script>
```


### 完整示例

```html
<template>
	<w-barcode @press="longtap" ref="barcode" :options="options"  @generate="aleard"></w-barcode>
	<view @click="SaveCode"></view>
</template>
<script>
	export default {
		data() {
			return {
				options:{
                    color: ['#45B649','#00c3ff', '#ee0979'], // 条形码的颜色 默认黑色
					bgColor: '#FFFFFF', // 背景色
					width: 670, // 宽度 单位rpx
					height: 100, // 高度 单位rpx
					code: 'E57890543271985',// 生成条形码的值
				},
			}
		},
        methods: {
            async SaveCode (){//保存条形码图片
                const res = await this.$refs.barcode.GetCodeImg()
                console.log(res)
            },
            aleard (res) {// 条形码创建成功的回调 修改参数同样触发
                console.log(res)
            },
			longtap (e){//长安事件
				console.log(e);
			}
        }
	}
</script>
```

### 条形码Props

options为一个对象

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;类型&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|
|:----:|:----:|:----:|:----:|
|options |是  |Object |创建条形码时传的参数 |

### options

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|<span style="color:red;font-weight: 600;">id</span> |是  |String |canvas 的canvas-id 如果以组件方式使用 此属性不需要传 |
|<span style="color:red;font-weight: 600;">ctx</span> |否  |Object | 自定义组件实例 this 如果以组件方式使用此属性不需要|
|code |是  |String | 扫描条形码的结果    |
|bgColor |否  |String | 生成条形码的背景色 默认 '#FFFFFF'    |
|color     |否  |Array | 生成条形码的颜色默认黑色 多个渐变色['#e66465','#9198e5'] 最多10中颜色   |
|width |是  |Number | 生成条形码的宽度 一律当rpx处理    |
|height |是  | Number | 生成条形码的高度 一律当rpx处理|

> [!ATTENTION]
> 如果以组件的形式使用，参数`id`与`ctx`不需要传。其他参数更具自己需求添加使用

### Methods

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|参数|
|:----:   |:----:|:-----:|
|GetCodeImg |手动获取二维码图片  |返回一个对象|
### Events

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;事件名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|回调参数|
|:----:   |:----:|:-----:|
|generate |条形码创建成功的时候触发  |返回一个对象 |
|press |手指长按 500ms 之后触发，触发了长按事件后进行移动不会触发屏幕的滚动  |- |

### generate返回对象字段说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;key&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|
|:----:   |:----:|
| code | 生成码的编码code |
| id | 当前canvas的唯一ID|
|createTime |条形码创建时间   |
|takeUpTime |本次绘制图案所耗时 单位ms  |
| img | 如果二维码创建成功 则返回二维码图片相关信息 object|
|with |条形码的宽度（转换后的大小单位px）|
|height|条形码高 转换后的大小单位px）|
| model|  设备型号|
| system | 操作系统名称及版本，如Android 10|
| platform|客户端平台，值域为：ios、android、mac（3.1.10+）、windows（3.1.10+）、linux（3.1.10+）|