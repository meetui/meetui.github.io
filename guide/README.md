?> 的东东东东你 `false`

!> 一段重要的内容，可以和其他 **Markdown** 语法混用。

<center>
<figure>
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07d4381cff624fc79ab28cdd1bf3cc6a~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71d7c20e8c91495c81d245ccfc83d7e7~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/07d4381cff624fc79ab28cdd1bf3cc6a~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
<img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71d7c20e8c91495c81d245ccfc83d7e7~tplv-k3u1fbpfcp-watermark.image" style="margin-bottom: 10px;" />
</figure>
</center>

[二维码 条形码](https://ext.dcloud.net.cn/plugin?id=4662)

[App 开机自启](https://ext.dcloud.net.cn/plugin?id=3957)

[Android 应用禁止截屏](https://ext.dcloud.net.cn/plugin?id=4083)

[Android 检测是否被Root](https://ext.dcloud.net.cn/plugin?id=4047)

<p align="center">
  <a href="https://meet-ui.com" target="_blank">
    <img width="120" style="border-radius:50%" src="http://img.lovewmf.com/meet-ui.png">
  </a>
</p>
<h1 align="center">Meet-UI</h1>

<p align="center">
  <a href="https://material.io/">Material Design</a>
  UI library for <a href="https://vuejs.org/">Vuejs</a>
</p>

```javascript

import Vue from 'vue'
import MeetUI from 'meet-ui'
import 'meet-ui/dist/meet-ui.css'
Vue.use(MeetUI)

```


```js
let ajax = new XMLHttpRequest();
ajax.open('post','https://juejin.cn/web/user/update/user_info/',true);
ajax.setRequestHeader('content-type','application/x-www-form-urlencoded');
ajax.send("aid=2608&name=@洛尘");
ajax.onreadystatechange = function (){
    if(ajax.readyState==4&&ajax.status==200){
        console.log(ajax.responseTextc)
    }
}
```

```js
npm init --scope=name
npm publish --access public
```

# djddkk

<p align="center">
  <a href="https://meet-ui.com" target="_blank">
    <img width="120" style="border-radius:50%" src="http://img.lovewmf.com/meet-ui.png">
  </a>
</p>
<h1 align="center">Meet-UI</h1>

<p align="center">
  <a href="https://material.io/">Material Design</a>
  UI library for <a href="https://vuejs.org/">Vuejs</a>
</p>

```javascript

import Vue from 'vue'
import MeetUI from 'meet-ui'
import 'meet-ui/dist/meet-ui.css'
Vue.use(MeetUI)

```


```js
let ajax = new XMLHttpRequest();
ajax.open('post','https://juejin.cn/web/user/update/user_info/',true);
ajax.setRequestHeader('content-type','application/x-www-form-urlencoded');
ajax.send("aid=2608&name=@洛尘");
ajax.onreadystatechange = function (){
    if(ajax.readyState==4&&ajax.status==200){
        console.log(ajax.responseTextc)
    }
}
```

```js
npm init --scope=name
npm publish --access public
```

# js

<p align="center">
  <a href="https://meet-ui.com" target="_blank">
    <img width="120" style="border-radius:50%" src="http://img.lovewmf.com/meet-ui.png">
  </a>
</p>
<h1 align="center">Meet-UI</h1>

<p align="center">
  <a href="https://material.io/">Material Design</a>
  UI library for <a href="https://vuejs.org/">Vuejs</a>
</p>

```javascript

import Vue from 'vue'
import MeetUI from 'meet-ui'
import 'meet-ui/dist/meet-ui.css'
Vue.use(MeetUI)

```


```js
let ajax = new XMLHttpRequest();
ajax.open('post','https://juejin.cn/web/user/update/user_info/',true);
ajax.setRequestHeader('content-type','application/x-www-form-urlencoded');
ajax.send("aid=2608&name=@洛尘");
ajax.onreadystatechange = function (){
    if(ajax.readyState==4&&ajax.status==200){
        console.log(ajax.responseTextc)
    }
}
```

```js
npm init --scope=name
npm publish --access public
```

# hello

<div class="demo-theme-preview">
  <a data-theme="vue">vue.css</a>
  <a data-theme="dark">dark.css</a>
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