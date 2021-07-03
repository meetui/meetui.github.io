# 安装

> *更新时间 2020-07-01*

!> **必须带`-save` 因为组件依赖 `@uni-ui/code-plugs`**

nvue使用指南[详情](/)
```js
// 安装
npm i @uni-ui/code-ui -save

// 更新
npm update @uni-ui/code-ui
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