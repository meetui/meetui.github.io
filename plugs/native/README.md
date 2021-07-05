# 开机自启

> 更新时间 2020-07-05

Android开机自启动，支持Android广告屏，机顶盒等

#### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Android&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|:----:|:----:|
|√ |× |

如果是云打包 直接在[插件市场](https://ext.dcloud.net.cn/plugin?id=3957)点击 右上角 for云打包 填好相关信息即可 无需执行任何接口

#### 插件测试使用流程

* 在项目根目录下新建nativeplugins目录 将下载的插件解压放入该目录

* 在manifest.json->App原生插件配置->本地插件选择该插件

* 运行->运行到手机或模拟器->制定自定义基座调试

* 打包完成后 运行基座选择自定义基座

* 开机自启动插件 由于Android高版本限制应用第一次安装后必须手动启动一次应用方可生效

* 本插件适用于Android广告屏，机顶盒等等


# 应用禁止截屏
> 更新时间 2020-07-05

禁止安卓App截屏,IOS 不可能禁止截屏，只能添加截屏事件插件市场有


#### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Android&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|:----:|:----:|
|√ |× |

如果是云打包 直接在[插件市场](https://ext.dcloud.net.cn/plugin?id=4083)点击 右上角 for云打包 填好相关信息

`app.vue`
```js
<script>
    export default {
        onLaunch: function() {
            const scree = uni.requireNativePlugin('wmf-UnScreen')
            scree.Prohibit();
        },
        : function() {
            console.log('App Show')
        },
        onHide: function() {
            console.log('App Hide')
        }
    }
 </script>
```
#### 如果不使用插件

`app.vue`

```js
 <script>
    export default {
        onLaunch: function() {
            if(uni.getSystemInfoSync().platform == 'android'){
                const main = plus.android.runtimeMainActivity();
                let mwindow  = main.getWindow();  
                    plus.android.importClass(mwindow);  
                    mwindow.setFlags(0x00002000);//WindowManager.LayoutParams.FLAG_SECURE
            }
        },
        : function() {
            console.log('App Show')
        },
        onHide: function() {
            console.log('App Hide')
        }
    }
 </script>
```

# 检测系统是否被root
> 更新时间 2020-07-05

#### 平台差异说明

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Android&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IOS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|:----:|:----:|
|√ |× |

如果是云打包 直接在[插件市场](https://ext.dcloud.net.cn/plugin?id=4047)点击 右上角 for云打包 填好相关信息

```js
 <script>
    export default {
        methods: {
            okForm() {
                const isRoot = uni.requireNativePlugin('wmf-CheckRoot');
                isRoot.isCheckRoot(res=>{
                    //如果返回的是false 则系统没有被Root 如果返回的是 true 则系统被root
                    console.log(res);//true false
                })
            }
        }
    }
 </script>
```
> [!ATTENTION]
> IOS请使用官方[API](https://www.html5plus.org/doc/zh_cn/navigator.html#plus.navigator.isRoot)`https://www.html5plus.org/doc/zh_cn/navigator.html#plus.navigator.isRoot`


# SSL双向校验

整理中


# 身份证离线识别

整理中

* 【重要】升级 HBuilderX 内置node版本升级为12.22，内置npm版本升级为6.4
* 【重要】调整 alt+鼠标滚动的行为从横向滚动调整为竖向滚动一屏。横向滚动为shift+鼠标滚轮
* 强化 各种鼠标滚轮功能，横向竖向滚动、滚3行滚一屏 [详情](https://hx.dcloud.net.cn/Tutorial/keybindings?id=鼠标滚轮)
* 新增 区域内搜索 选中一段文字，在顶部搜索栏选中区域搜索【Ctrl+Shift+f】，可以在特殊背景区内搜索、替换、全选相同词 [详情](https://hx.dcloud.net.cn/Tutorial/UserGuide/find?id=区域内搜索)
* 新增 自定义右键菜单。编辑器和内置资源管理器 `Alt + 鼠标右键`弹出自定义右键菜单
* 新增 设置 增加启用自动匹配字符功能 （【设置 - 编辑器配置】，启用自动匹配字符功能）