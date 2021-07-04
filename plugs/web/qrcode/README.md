# 二维码

> 更新时间 2020-07-01

此组件为二维码，默认没有边框以及二维码的颜色是黑色，如果需要边框或者颜色需要传对应的参数详情可参考下面的示例

> [!ATTENTION]
> Nvue不支持此组件，使用方式请参考[Nvue](/plugs/web/nvue/#Nvue)

### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;App&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;H5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|微信小程序|支付宝小程序|百度小程序|头条小程序|QQ小程序|
|:----:|:----:|:----: |:----:|:----: |:----: |:----:|
|√ |√  |√ |√ | √| √| √|

只要是使用`uni-app`进行开发，凡是支持`canvas`画布的都支持此组件

### 二维码Props

options为一个对象

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;类型&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|
|:----:|:----:|:----:|:----:|
|options |是  |Object |创建二维码时传的参数 |

### options

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|<span style="color:red;font-weight: 600;">id</span> |是  |String |canvas 的canvas-id 如果以组件方式使用 此属性不需要传 |
|<span style="color:red;font-weight: 600;">ctx</span> |否  |Object | 自定义组件实例 this 如果以组件方式使用此属性不需要|
|code |是  |String | 扫描二维码的结果    |
|border |否  |Object | 生成二维码的边框配置    |
|bgColor |否  |String | 生成二维码的背景色 默认 '#FFFFFF'    |
|color     |否  |string/Array | 生成二维码的颜色默认黑色 支持渐变色['#e66465','#9198e5']    |
|size |是  |String/Number |二维码的大小 一律当rpx处理  |
|level |否  |Number | 生成二维码的等级    |
|img     |否  |path | 生成二维码中间的图标    |
|iconSize     |否  |Number | 生成二维码中间的图标大小 |

> [!ATTENTION]
> 如果以组件的形式使用，参数`id`与`ctx`不需要传。其他参数更具自己需求添加使用

### Events

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;事件名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|回调参数|
|:----:   |:----:|:-----:|
|generate |二维码创建成功的时候触发  |返回一个对象 |

### 最简单的示例

```html
<template>
	<w-qrcode :options="options"></w-qrcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',// 生成二维码的值
					size: 460,// 460代表生成的二维码的宽高均为460rpx
				},
			}
		},
	}
</script>

```
