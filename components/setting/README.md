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

#### 主题

<div class="demo-theme-preview">
  <a data-theme="vue">正常</a>
  <a data-theme="dark">暗黑</a>
</div>

<style>
  .demo-theme-preview a {
    padding-right: 10px;
  }

  .demo-theme-preview a:hover {
    cursor: pointer;
    text-decoration: underline;
  }
</style>

<script>
  var preview = Docsify.dom.find('.demo-theme-preview');
  var themes = Docsify.dom.findAll('[rel="stylesheet"]');

  preview.onclick = function (e) {
    var title = e.target.getAttribute('data-theme');
    themes.forEach(function (theme) {
      theme.disabled = theme.title !== title;
    });
  };
</script>