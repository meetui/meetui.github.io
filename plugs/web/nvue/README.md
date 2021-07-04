# Nvue
> *更新时间 2020-07-01*

nvue 特有使用方式
# 配置

`manifest.json`

```
"app-plus": {
	"modules": {
		"Canvas" : "nvue canvas"
	},
}
```

# 安装

> [!TIP]
> 关于`uni-canvas-nvue`来自与官方示例`https://github.com/dcloudio/NvueCanvasDemo`这里为了方便使用制作了npm包

HBuilderX 2.2.5（alpha）开始 nvue 页面支持 Canvas，支持 W3C WebGL API WebGL 1.0

在App端，从性能来讲，由于通讯阻塞的问题，nvue的canvas性能不可能达到使用renderjs的vue页面的canvas。在App端，推荐使用vue的canvas。


```js
npm i @uni-plugs/uni-canvas-nvue
npm i @uni-plugs/uni-code
```

> [!ATTENTION]
> 相关参数均与vue使用方式相同。唯一不同的是ID 详情请参考[完整示例](/plugs/web/nvue/#完整示例)

# Html

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

# Css

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

# Js

```javascript
<script>
    import {enable, WeexBridge } from '@uni-plugs/uni-canvas-nvue';
    import CODE from '@uni-plugs/uni-code';

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
                    // img: '/static/logo.png',//图片
                    iconSize: 40, //二维码图标的大小
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

# 完整示例

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
    // npm i @uni-plugs/uni-canvas-nvue
    import {enable, WeexBridge } from '@uni-plugs/uni-canvas-nvue';
    // npm i @uni-plugs/uni-code
    import CODE from '@uni-plugs/uni-code';

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
                    // img: '/static/logo.png',//图片
                    iconSize: 40, //二维码图标的大小
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

# 完整参数
