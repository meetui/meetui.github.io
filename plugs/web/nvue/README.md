# Nvue
> *更新时间 2021-06-23*

nvue 特有使用方式 参数请参考vue
### 配置

`manifest.json`

```
"app-plus": {
	"modules": {
		"Canvas" : "nvue canvas"
	},
}
```

### 安装

> [!TIP]
> 关于`uni-canvas-nvue`来自与官方示例`https://github.com/dcloudio/NvueCanvasDemo`这里为了方便使用制作了npm包

HBuilderX 2.2.5（alpha）开始 nvue 页面支持 Canvas，支持 W3C WebGL API WebGL 1.0

在App端，从性能来讲，由于通讯阻塞的问题，nvue的canvas性能不可能达到使用renderjs的vue页面的canvas。在App端，推荐使用vue的canvas。


```js
npm i @uni-ui/nvue-canvas-plugs
npm i @uni-ui/code-plugs

```

> [!ATTENTION]
> 相关参数均与vue使用方式相同。唯一不同的是ID 详情请参考[完整示例](/plugs/web/nvue/#完整示例)

### Html

```html
<template>
	<view class="container">
		<view class="panel" :style="{width: widthPanle}">
			<text class="header">请扫描以下任意二维码或条形码</text>
			<view class="juster-center">
				<view class="barcode">
					<gcanvas ref="barcode" class="barcode"></gcanvas>
				</view>
				<text class="barnum">{{code}}</text>
				<view class="qrcode">
					<gcanvas ref="qrcode" class="qrcode"></gcanvas>
				</view>
			</view>
		</view>
	</view>
</template>
```

### Css

```css

<style>
	.container{
		align-items: center;
		justify-content:center;
	}
	.panel {
		margin-top: 200rpx;
		border-radius: 10rpx;
		background-color: #fff;
		padding-bottom: 80rpx;
	}
	
	.header {
		text-align: center;
		padding: 30rpx 0;
		color: #1b82d2;
		font-weight: bold;
		background-color: #f0f0f0;
		border-radius: 10rpx 10rpx 0 0;
		margin-bottom:50rpx;
	}
	.juster-center{
		align-items: center;
	}
	.barcode {
		width: 670rpx;
		height: 100rpx;
	}
	
	.barnum {
		padding: 20rpx 0;
		font-size: 38rpx;
		font-weight: bold;
		text-align: center;
	}
	.qrcode {
		width: 460rpx;
		height: 460rpx;
		background-color: #fff;		
	}
</style>
```

### Js

```javascript
<script>
    import {enable, WeexBridge } from '@uni-ui/nvue-canvas-plugs';
    import CODE from '@uni-ui/code-plugs';

    const modal = weex.requireModule("modal");
    module.exports = {
        data: {
            code: 'E01181016286106',
			widthPanle: '660rpx',
            config:{
                bar:{// 条形码配置
                    color: '#000', // 条形码的颜色
                    bgColor: '#FFFFFF', // 背景色
                    width: 670, // 宽度 单位rpx
                    height: 100 // 高度 单位rpx
                },
                qrc:{// 二维码配置
                    size: 460, // 二维码大小 单位rpx
                    level: 4, //等级 0～4
                    bgColor: '#FFFFFF', //二维码背景色 默认白色
                    border: {
                        color: "#faa755", //边框颜色支持渐变色
                        lineWidth: 4, //边框宽度
                    },
                    color: ['#e66465', '#9198e5'] // 二维码颜色 默认黑色
                }
            },
            ctxQR: null,
			ctxBR: null
        },
        onReady: function(e) {
			this.getSystemInfo()
			// 二维码
            const qr = this.$refs["qrcode"];
            const canvasQR = enable(qr, {
                bridge: WeexBridge
            });
			this.ctxQR = canvasQR.getContext('2d');
			
			// 条形码
			const br = this.$refs["barcode"];
			const canvasBR = enable(br, {
			    bridge: WeexBridge
			});
			this.ctxBR = canvasBR.getContext('2d');
            this.findCan();
        },
        methods: {
            findCan () {
                // 条形码
                CODE.BarCode({...this.config.bar,code: this.code,id: this.ctxBR});
                // 二维码
                CODE.QRCode({...this.config.qrc, id: this.ctxQR, code: "https://weixin.qq.com/g/AwYAAHO3aO4zlasEij6bLsk4hlZd5XNFkkBmqyS55mLPFxmn5c9PaI1omqLhd24f"});
            },
			getSystemInfo () {
				try {
				    const res = uni.getSystemInfoSync();
					this.widthPanle = (res.windowWidth*0.95 + 'px') || '660rpx';
				} catch (e) {}
			}
        }
    }
</script>
```

#### 完整示例

> [!NOTE]
> 完整示例可以直接复制

```js
<template>
	<view class="container">
		<view class="panel" :style="{width: widthPanle}">
			<text class="header">请扫描以下任意二维码或条形码</text>
			<view class="juster-center">
				<view class="barcode">
					<gcanvas ref="barcode" class="barcode"></gcanvas>
				</view>
				<text class="barnum">{{code}}</text>
				<view class="qrcode">
					<gcanvas ref="qrcode" class="qrcode"></gcanvas>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
    import {enable, WeexBridge } from '@uni-ui/nvue-canvas-plugs';
    import CODE from '@uni-ui/code-plugs';

    const modal = weex.requireModule("modal");
    module.exports = {
        data: {
            code: 'E01181016286106',
			widthPanle: '660rpx',
            config:{
                bar:{// 条形码配置
                    color: '#000', // 条形码的颜色
                    bgColor: '#FFFFFF', // 背景色
                    width: 670, // 宽度 单位rpx
                    height: 100 // 高度 单位rpx
                },
                qrc:{// 二维码配置
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
                }
            },
            ctxQR: null,
			ctxBR: null
        },
        onReady: function(e) {
			this.getSystemInfo()
			// 二维码
            const qr = this.$refs["qrcode"];
            const canvasQR = enable(qr, {
                bridge: WeexBridge
            });
			this.ctxQR = canvasQR.getContext('2d');
			
			// 条形码
			const br = this.$refs["barcode"];
			const canvasBR = enable(br, {
			    bridge: WeexBridge
			});
			this.ctxBR = canvasBR.getContext('2d');

			//创建二维码 条形码
            this.findCan();
        },
        methods: {
            findCan () {
                // 条形码
                CODE.BarCode({...this.config.bar,code: this.code,id: this.ctxBR});
                // 二维码
                CODE.QRCode({...this.config.qrc, id: this.ctxQR, code: "https://weixin.qq.com/g/AwYAAHO3aO4zlasEij6bLsk4hlZd5XNFkkBmqyS55mLPFxmn5c9PaI1omqLhd24f"},res=>{
					console.log(res)//二维码创建成功失败都会 回调
				});
            },
			getSystemInfo () {
				try {
				    const res = uni.getSystemInfoSync();
					this.widthPanle = (res.windowWidth*0.95 + 'px') || '660rpx';
				} catch (e) {}
			}
        }
    }
</script>
<style>
	.container{
		align-items: center;
		justify-content:center;
	}
	.panel {
		margin-top: 200rpx;
		border-radius: 10rpx;
		background-color: #fff;
		padding-bottom: 80rpx;
	}
	
	.header {
		text-align: center;
		padding: 30rpx 0;
		color: #1b82d2;
		font-weight: bold;
		background-color: #f0f0f0;
		border-radius: 10rpx 10rpx 0 0;
		margin-bottom:50rpx;
	}
	.juster-center{
		align-items: center;
	}
	.barcode {
		width: 670rpx;
		height: 100rpx;
	}
	
	.barnum {
		padding: 20rpx 0;
		font-size: 38rpx;
		font-weight: bold;
		text-align: center;
	}
	.qrcode {
		width: 460rpx;
		height: 460rpx;
		background-color: #fff;		
	}
</style>
```

### 完整参数

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;必选&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|类型|说明|
|:----:|:----:|:----:|:----:|
|id |是  |Object |请参考示例|
|code |是  |String | 扫描二维码的结果    |
| padding| 否 | Number| 二维码间距|
| type | 否 | String| 二维码码点 默认none 可选值dots 圆点 square正方形距|
| src| 否 | String| 二维码背景图片|
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