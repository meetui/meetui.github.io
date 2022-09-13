# Git

> 更新时间 2020-07-05

日常使用`git`常用的操作命令 `.gitignore`

### 第一次提交

创建 git 仓库:

```js
1. git init

2. git config user.name "name" //git config --global user.name 全局

3. git config user.email "lovewmf@sina.cn"

4. git add .

5. git commit -m "init: 初始化项目"

6. git remote add origin https://gitee.com/lovewmf/test.git

7. git push -u origin master

```

已有仓库?

```js
1. git remote rm origin

2. git remote add origin https://gitee.com/lovewmf/test.git

3. git push -u origin master
```

### 删除远程仓库分支

```js
git remote rm origin

git branch -D name

git push origin --delete name

```

### 账号错误

清空本地保存的用户名和密码

```js
git config --system --unset credential.helper
```

### 代码合并

全部合并

```js
git merge dev // 合并整个dev到当前分支
```

合并某一次提交

```js
git cherry-pick 282a0bcd6a64df3ffa6c24fbd8453ff22844a131 // 合并某一次提交到当前分支
```

### 常规操作

```js
git reset --hard 282a0bcd6a64df3ffa6c24fbd8453ff22844a131 // 会退到某一次提交的版本

git merge --abort // 会退到pull之前

```

### 创建标签

```js

git tag 2021-07-08 // 创建tag

git tag -a 2021-07-08 -m "注释"// 创建带注释的tag

git push origin 2021-07-08 //将tag 推送到远程

git tag -d 2021-07-08 //删除本地tag

git push origin :refs/tags/2021-07-08 // 删除远程tag

git tag // 列出所有tag

```

### commit注释规范

规范的注释可以方便很多事,标签的作用是快速识别和判断出当前提交的内容的作用。

```js
git commit -m "init: 初始化项目"

git commit -m "add: 添加一个新的功能"

git commit -m "update: 更新某个功能或其它"

git commit -m "flare: 本次提交亮点，表明自己完成了一个很有意思，很有闪光点，亮点的功能或代码。以便引起自己或他人的重视或注视。"

git commit -m "done: 完成某一个功能"

git commit -m "fix: 完成某个功能之后如果还有更新，就不做update了，因为你已经认为自己完成了。后面的都是发现的问题，所以都是要处理的bug，所以处理完，就要称之为修复fix"

git commit -m "feature: 实现用户注册功能，修复所有问题，并通过测试.你已经完成此功能，将不会再对他进行修复或更新。除非要升级此功能，或此功能有了新的变化和需求。如果有新的需求了，则又要从add开始做"

git commit -m "ban: 禁用某个功能,决定临时或永久的禁用。有可能未来会开启。如果永久的禁用，那不如删除"

git commit -m "delete: 删除某个功能"

git commit -m "reset: 弃用用户评论功能，并进行强制回退处理"

git commit -m "style: 格式/样式（不影响代码运行的变动）"

git commit -m "refactor: 重构（即不是新增功能，也不是修改bug的代码变动）"

git commit -m "merge: 代码合并"

git commit -m "sync: 同步主线或分支的Bug"

git commit -m "revert: 回滚到上一个版本"

git commit -m "chore: 构建过程或辅助工具的变动"

git commit -m "test: 增加测试"

git commit -m "perf: 优化相关，比如提升性能、体验"

git commit -m "docs: 文档"
```
