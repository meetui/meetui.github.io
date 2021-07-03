# 配置
> *更新时间 2020-07-01*

!> **uni-app的`easycom`在打包的时候是按需引入的，您可以放心引入的组件库，发布打包时会自动剔除您没有使用的组件**

在`pages.json`里面配置如下
```json
"easycom": {
	//"^u-(.*)": "uview-ui/components/u-$1/u-$1.vue",//uView的配置
	"^w-(.*)": "@uni-ui/code-ui/components/w-$1/index.vue"
},
"pages": [
  //...
]
```
