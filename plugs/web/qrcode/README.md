# 二维码

> 更新时间 2020-07-01

此组件为二维码，默认没有边框以及二维码的颜色是黑色，支持纯汉字以及字母数字的混合code。如果需要边框或者颜色需要传对应的参数详情可参考下面的示例

> [!ATTENTION|style:flat|label:注意|]
> Nvue不支持此组件，使用方式请参考[Nvue](/plugs/web/nvue/#Nvue) 二维码code不要过长

### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;App&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;H5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|微信小程序|支付宝小程序|百度小程序|头条小程序|QQ小程序|
|:----:|:----:|:----: |:----:|:----: |:----: |:----:|
|√ |√  |√ |√ | √| √| √|

只要是使用`uni-app`进行开发，凡是支持`canvas`画布的都支持此组件


## 如果使用脚手架方式

新版不在需要此配置

```js
//vue.config.js里面添加如下配置
module.exports = {
    transpileDependencies: [
        /[/\\]node_modules[/\\](.+?)?@uni-ui(.*)[/\\]code-plugs/
    ]
}
```

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
	<w-qrcode :options="options" @generate="hello"></w-qrcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',// 生成二维码的值
                    border:{
						color: ['#F27121','#8A2387','#1b82d2'], //边框颜色支持渐变色 最多10种颜色 如果默认黑色此属性不需要传
						opacity: 0.6, //边框透明度 默认为1不透明 0~1
						lineWidth: 6, //边框宽度
						degree: 15 //边框圆角度数 默认5
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
	<w-qrcode :options="options"  @generate="hello"></w-qrcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',// 生成二维码的值
                    color: ['#11998e','#38ef7d','#F27121','#8A2387','#1b82d2'],// 二维码颜色支持渐变色 目前只支持最多10种颜色的渐变
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
	<w-qrcode :options="options"  @generate="hello"></w-qrcode>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0',// 生成二维码的值
					size: 460,// 460代表生成的二维码的宽高均为460rpx
                    img: {// 二维码log配置 非必传
						src: '/static/logo.png', // 图片地址
						size: 40,// 图片大小
						degree: 15,// 圆角大小 如果type为round生效
						type: 'round',//图片展示类型 默认none 可选值  round圆角  circle圆 如果为round 可以传入degree设置圆角大小 默认 5
						color: '#ffffff', //图片周围的白色边框
						width: 8 //图片周围白色边框的宽度 默认5
					},
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
	<w-qrcode ref="qrcode" :options="options"  @generate="hello"></w-qrcode>
	<view @click="SaveCode">保存图片</view>
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
				const res = await this.$refs.qrcode.GetCodeImg()
				console.log(res)
			},
			hello (res) {//二维创建成功失败 都会触发 如果创建成功 里面包含图片
				console.log(res)
			}
	}
</script>

```

### 完整示例

```html
<template>
	<w-qrcode ref="qrcode" :options="options" @generate="aleard" @longtap="longtap"></w-qrcode>
	<view @click="SaveCode">保存图片</view>
</template>
<script>
	export default {
		data() {
			return {
				options:{
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0', //必传
					level: 4, //纠错等级 0~4 默认4 非必传
					type: 'none',// 码点 目前只支持 none 其它暂不支持 非必传
					src: '/static/35.png',//画布背景 非必传
					padding: 10, //二维码margin Number 单位rpx 默认0 非必传
					border:{//二维码边框配置 非必传
						color: ['#F27121','#8A2387','#1b82d2'], //边框颜色支持渐变色 最多10种颜色 如果默认黑色此属性不需要传
						opacity: 0.6, //边框透明度 默认为1不透明 0~1
						lineWidth: 6, //边框宽度
						degree: 15 //边框圆角度数 默认5
					},
					text:{//二维码绘制文字 非必传
						opacity: 1, //文字透明度 默认不透明1  0~1 非必传
						font: 'bold 20px system-ui',//文字是否加粗 默认normal 20px system-ui 非必传
						color: ["#000000"], // 文字颜色 多个颜色支持渐变色 默认黑色 非必传
						content: "这是一个测试" //文字内容
					},
					img: {// 二维码log配置 非必传
						src: '/static/logo.png', // 图片地址
						size: 40,// 图片大小
						degree: 15,// 圆角大小 如果type为round生效
						type: 'round',//图片展示类型 默认none 可选值  round圆角  circle圆 如果为round 可以传入degree设置圆角大小 默认 5
						color: '#ffffff', //图片周围的白色边框
						width: 8 //图片周围白色边框的宽度 默认5
					},
					color: ['#11998e','#38ef7d','#F27121','#8A2387','#1b82d2'], //二维码颜色支持渐变 最多10种颜色 默认黑色 非必传
					bgColor: "#FFFFFF",//二维码背景色 默认白色 非必传
					size: 460, // 二维码大小 Number 单位rpx 必传
				},
			}
		},
        methods: {
            async SaveCode (){//保存二维码图片
                const res = await this.$refs.qrcode.saveImg()
                console.log(res)
            },
            aleard (res) {// 二维码创建成功或者失败的回调 修改参数同样触发 新增返回二维码图片
                console.log(res)
            },
			longtap (e){//手指长按事件
				console.log(e);
			}
        }
</script>

```

### 二维码Props

options为一个对象

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;类型&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|
|:----:|:----:|:----:|:----:|
|options |是  |Object |创建二维码时传的参数 |

### Options

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|<span style="color:red;font-weight: 600;">id</span> |是  |String |canvas 的canvas-id 如果以组件方式使用 此属性不需要传 |
|<span style="color:red;font-weight: 600;">ctx</span> |否  |Object | 自定义组件实例 this 如果以组件方式使用此属性不需要|
|code |是  |String | 扫描二维码的结果    |
| padding| 否 | Number| 二维码间距|
|border |否  |Object | 生成二维码的边框配置    |
|bgColor |否  |String | 生成二维码的背景色 默认 '#FFFFFF'    |
|color     |否  |Array | 生成二维码的颜色默认黑色 支持渐变色['#e66465','#9198e5']    |
|size |是  |String/Number |二维码的大小 一律当rpx处理  |
|level |否  |Number | 生成二维码的纠错等级默认4 取值范围0~4    |
|img     |否  |Object | 生成二维码中间的图标配置    |
|text     |否  |Object | 生成二维码中间的文字配置 |

### Border
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|opacity |否  |Number | 边框透明度默认不透明 范围0~1    |
| degree| 否 | Number| 边框圆角度数 默认 5|
|color |否  | Array | 边框颜色最多支持10种颜色渐变 默认黑色不渐变    |
|lineWidth |否  |Number | 边框宽度   |

### Img
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|src |是  |String | 二维码中间图片地址 如果是网络图片需要先下载    |
| size| 否 | Number| 图片大小 默认 30|
|type |否  | String | 图片展示类型 默认none 可选值  round圆角  circle圆 如果为round 可以传入degree设置圆角大小 默认 5    |
|degree |否  |Number | type 为round生效 圆角度数 默认5   |
|color|否| String| 默认#FFFFFF 图片周围的白色边框|
|width|否|Number| 默认5 白色边框宽度|

### Text
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|opacity |否  |Number | 文字透明度 默认不透明 取值范围0~1    |
| font| 否 | String| 文字是否加粗文字大小 默认normal 20px system-ui|
|color |否  | Array | 文字颜色支持渐变色 最多10种   |
|content |是  |String | 文字内容   |

> [!ATTENTION]
> 如果以组件的形式使用，参数`id`与`ctx`不需要传。其他参数更具自己需求添加使用

### Methods

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方法名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|参数|
|:----:   |:----:|:-----:|
|GetCodeImg |手动获取二维码图片  |返回一个对象|

### Events

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;事件名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|参数|
|:----:   |:----:|:-----:|
|generate |二维码创建成功的时候触发  |返回一个对象 包括二维码图片|
|press |二维码长按事件  |手指长按 500ms 之后触发，触发了长按事件后进行移动不会触发屏幕的滚动|

### generate返回对象字段说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;key&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|说明|
|:----:   |:----:|
| code | 生成码的编码code |
| id | 当前canvas的唯一ID|
|createTime |条形码创建时间   |
|takeUpTime |本次绘制图案所耗时 单位ms  |
| img | 如果二维码创建成功 则返回二维码图片相关信息 object|
|size |二维码大小（转换后的大小单位px）|
| model|  设备型号|
| system | 操作系统名称及版本，如Android 10|
| platform|客户端平台，值域为：ios、android、mac（3.1.10+）、windows（3.1.10+）、linux（3.1.10+）|
