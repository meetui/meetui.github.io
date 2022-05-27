# 介绍

> 更新时间 2020-11-23

二维码 条形码生成，二维码支持渐变色以及边框。二维码可以添加中间log图片可以将生成的条形码或者二维码保存为图片。支持`nvue`

> 使用TS重构 增加部分新功能


<img src="https://img.lovewmf.com/20211122.png" width="200"/>

# 演示效果

<figure>
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07d4381cff624fc79ab28cdd1bf3cc6a~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;border-radius: 10px;" />
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71d7c20e8c91495c81d245ccfc83d7e7~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;border-radius: 10px;" />
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bfe9eb88cea44007b2627bb640343dcc~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;border-radius: 10px;" />
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b625254802404a9b84bd699e67b03db4~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;border-radius: 10px;" />
<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f84328d92b104edbad4c34a8665b4c72~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;border-radius: 10px;" />
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c1548ccd6c944bbe90ef288817077b8c~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;border-radius: 10px;" />
</figure>

# 使用方式

> [!TIP]
> 二维码 条形码都有两种使用方式：组件形式与非组件形式 这里推荐使用组件方式进行使用


# uni_modules使用方式

> [!TIP]
> `使用 HBuilderX 导入插件`直接导入插件 无需使用npm方式 请直接配置以下

在`pages.json`里面配置如下
```js
"easycom": {
	"^w-(.*)": "@/uni_modules/wmf-code/components/w-$1/w-$1.vue"//二维码条形码的配置 如果是npm方式使用 @uni-ui/code-ui/components/w-$1/index.vue
},
"pages": [
  //...
]
```

### 组件方式

组件方式依赖于`@uni-ui/code-plugs`，在`npm i @uni-ui/code-ui -save`的时候会自动安装相关依赖。无需单独安装

```js
npm i @uni-ui/code-ui -save
```
### 配置

组件方式独有配置

!> **uni-app的`easycom`在打包的时候是按需引入的，您可以放心引入的组件库，发布打包时会自动剔除您没有使用的组件**

在`pages.json`里面配置如下
```js
"easycom": {
	"^w-(.*)": "@uni-ui/code-ui/components/w-$1/index.vue"//二维码条形码的配置
},
"pages": [
  //...
]
```

### Js方式

使用Js方式无需单独配置，只需要引用根据文档传参数即可使用

> [!TIP]
> 请直接使用组件方式，不推荐使用此方式

```js
npm i @uni-ui/code-plugs
```

```js
<template>
	<view class="qrcode-view">
		<canvas canvas-id="qrcode" id="qrcode" style="width:460rpx;height: 460rpx" />
	</view>
</template>
<script>
	import {QRCode} from '@uni-ui/code-plugs';
	export default {
		data() {
			return {
				qar: {//所有属性配置示例
					code: 'https://qm.qq.com/cgi-bin/qm/qr?k=LKqML292dD2WvwQfAJXBUmvgbiB_TZWF&noverify=0', //必传
					level: 4, //纠错等级 0~4 默认4 非必传
					type: 'none',// 码点 目前只支持 none 其它暂不支持 非必传
					src: '/static/35.png',//画布背景 非必传
					padding: 10, //二维码margin Number 单位rpx 默认0 非必传
					border:{//非必传
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
				}
			}
		},
		onReady() {
			this.findCan(this.qar)
		},
		methods: {
			findCan(obj) {
				QRCode(obj,res=>{
					console.log(res)
				});
			},
		}
	}
</script>
```