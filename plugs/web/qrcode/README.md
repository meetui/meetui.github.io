# 二维码

> 更新时间 2020-07-01

此组件为二维码，默认没有边框以及二维码的颜色是黑色，如果需要边框或者颜色需要传对应的参数详情可参考下面的示例

> [!ATTENTION|style:flat|label:注意|]
> Nvue不支持此组件，使用方式请参考[Nvue](/plugs/web/nvue/#Nvue)

### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;App&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;H5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|微信小程序|支付宝小程序|百度小程序|头条小程序|QQ小程序|
|:----:|:----:|:----: |:----:|:----: |:----: |:----:|
|√ |√  |√ |√ | √| √| √|

只要是使用`uni-app`进行开发，凡是支持`canvas`画布的都支持此组件

### 基本使用

请确定在`pages.json`里面配置了`easycom`。如果没有请前往当前文档的：使用方式->组件方式里面的配置。如已经配置请忽略

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

### 增加边框

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
                    border:{
						color: ['#ec008c','#fc6767'], // 边框颜色支持渐变色 目前只支持最多两种颜色的渐变
                        // color: '#fc6767', // 单色不渐变
						lineWidth: 6, // 边框的宽度 不传默认为4
					},
					size: 460,// 460代表生成的二维码的宽高均为460rpx
				},
			}
		},
	}
</script>
```

### 修改颜色

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
                    color: ['#11998e','#38ef7d'],// 颜色支持渐变色 目前只支持最多两种颜色的渐变
                    // color: '#38ef7d',// 单色不渐变
					size: 460,// 460代表生成的二维码的宽高均为460rpx
				},
			}
		},
	}
</script>

```

### 添加LOG


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
                    img: '/static/logo.png',//图片路径
                    iconSize: 40,// 不传此参数默认为30
				},
			}
		},
	}
</script>
```

> [!ATTENTION|style:flat|label:注意|]
> 图片的路径，可以是相对路径，临时文件路径，存储文件路径，网络图片路径建。如果图片路径多变建议统一采用以下方式

```js
uni.getImageInfo({
    src:'/static/logo.png',// 图片的路径，可以是相对路径，临时文件路径，存储文件路径，网络图片路径
    complete: res =>{// 接口调用结束的回调函数（调用成功、失败都会执行）
        console.log(res)// res.path 为图片路径 获取到res.path后赋值给 img参数
    }
});
```

### 保存二维码

> [!TIP|style:flat|label:说明|]
> 具体返回信息请看官方文档https://uniapp.dcloud.io/api/canvas/canvasToTempFilePath


```html
<template>
	<w-qrcode ref="qrcode" :options="options"></w-qrcode>
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
        methods: {
			async SaveCode (){//保存二维码图片
				const res = await this.$refs.qrcode.saveImg()
				console.log(res)
			}
	}
</script>

```

### 完整示例

```html
<template>
	<w-qrcode ref="qrcode" :options="options" @generate="aleard"></w-qrcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',
					size: 460,
                    border:{
						color: ['#ec008c','#fc6767'],
						lineWidth: 6,
					},
                    level: 4, //纠错等级
                    color: ['#11998e','#38ef7d'],
                    img: '/static/logo.png',
                    iconSize: 40,
				},
			}
		},
        methods: {
            async SaveCode (){//保存二维码图片
                const res = await this.$refs.qrcode.saveImg()
                console.log(res)
            },
            aleard (res) {// 二维码创建成功的回调 修改参数同样触发
                console.log(res)
            }
        }
</script>

```

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

