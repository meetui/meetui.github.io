# 介绍

> 更新时间 2020-07-01

* 修复 MacOSX 3.1.17引出的 自带中文输入法输入英文会造成部分类型的文件着色失效的Bug
* 修复 MacOSX 3.1.17引出的 10.13.6操作系统，某些情况下，HBuilderX无法启动的Bug
* 修复 Windows 3.1.17引出的 vue-cli项目，当电脑本身没有安装node环境时，运行项目到内置终端，相关npm命令执行失败的Bug
* 优化 酷黑、雅蓝主题 代码助手 选中文本颜色
* 修复 代码助手 数字模式 sass文件，某些css属性值无法正确输入数字的Bug
  
<figure>
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07d4381cff624fc79ab28cdd1bf3cc6a~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71d7c20e8c91495c81d245ccfc83d7e7~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bfe9eb88cea44007b2627bb640343dcc~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b625254802404a9b84bd699e67b03db4~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f84328d92b104edbad4c34a8665b4c72~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c1548ccd6c944bbe90ef288817077b8c~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
</figure>

# 使用方式

> [!TIP]
> 二维码 条形码都有两种使用方式：组件形式与非组件形式 这里推荐使用组件方式进行使用

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
	"^u-(.*)": "uview-ui/components/u-$1/u-$1.vue",//uView的配置
	"^w-(.*)": "@uni-ui/code-ui/components/w-$1/index.vue"//二维码条形码的配置
},
"pages": [
  //...
]
```

### Js方式

使用Js方式无需单独配置，只需要引用更具文档传参数即可使用

```js
npm i @uni-ui/code-plugs
```