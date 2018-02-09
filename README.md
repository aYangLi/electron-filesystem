## 基于vue-electron的文件管理器

### git 介绍：

> 这个项目是从 github 摘过来的一个 electron-vue 项目；项目名称为 electron-filesystem ，本人复制此项目，单拉一个 git 的原因是上手此项目时，遇到了一些坑总结记录，也希望爱学习人士用此项目时少走弯路（本人花了半天才把项目跑完，压缩完成，流程走完，特此记录采坑记录），非常感谢原作者的项目，绝无冒犯之意，近在此引用记录；

原项目 gitbub 地址为：https://github.com/k-water/electron-filesystem  

### 接下来进入重点：

**采坑一：**  
- 在根目录下 package.json 缺少项目依赖；导致 npm install 之后，npm run dev 经常报错；在我上传的这个项目中我已经**补充完成**（大家可以直接用我这个项目在本地运行，借用别人项目，再次像原作者致敬！！！）；

**采坑二：**  
- 在此时运行 npm run dev ;你会发现还是会报错，提示缺少 reset-css ；这是因为原作者在 app.vue 中 @import  '../../node_modules/reset-css/reset.css' 所以各位再进入到 app 目录下，再次 npm install, 

**采坑三：**
- 经过上面两个坑，然后回到根目录，执行 npm run dev; 如果不报错，则跳过此坑，如果报错为 ‘Error: spawn electron ENOENT’；则将根目录下的 node_modle 删除掉，重新 npm intall 即可；

**采坑四：**  
- 接下来便可以进行打包安装包了；首先在根目录下执行 npm run build; 然后进入 build 目录下执行 grunt; 完成看打包完成的安装包能否使用；如果不可以；则删除掉打包的东西，退回到根目录，执行 npm run pack; 再次 npm run build => grunt; 再看安装包；重复此流程；

**注意五：**
- 在打包为安装包过程时，在 build 目录下需要再次 npm install ,并且全局安装 grunt => npm intatll grunt -g;


我的采坑完成，接下进入原作者的流程：

### 项目由来

项目的实现是一个`WIndows平台的文件管理器`，实现了基本的文件操作功能，新建，删除，复制，粘贴，剪切，重命名。

项目地址：[https://github.com/k-water/electron-filesystem](https://github.com/k-water/electron-filesystem)

### 什么是Electron
Electron 可以让你使用纯 JavaScript 调用丰富的原生 APIs 来创造桌面应用。你可以把它看作是专注于桌面应用而不是 web 服务器的，io.js 的一个变体。

这不意味着 Electron 是绑定了 GUI 库的 JavaScript。相反，Electron 使用 web 页面作为它的 GUI，所以你能把它看作成一个被 JavaScript 控制的，精简版的 Chromium 浏览器。


以下资料供参考学习：

[Electron(维基百科)](https://zh.wikipedia.org/wiki/Electron_(%E8%BD%AF%E4%BB%B6%E6%A1%86%E6%9E%B6))

[中文文档](https://www.w3cschool.cn/electronmanual/)

[(译)Electron的本质](https://segmentfault.com/a/1190000007503495)


[入门视频教程](http://ourcodeworld.com/articles/read/106/how-to-choose-read-save-delete-or-create-a-file-with-electron-framework)

### 技术栈
* [x] Vue
* [x] VueRouter
* [x] Vuex
* [x] Vue-Electron
* [x] iView
* [x] Eslint
* [x] Babel
* [x] Webpack
* [x] Less

项目采用了vue-cli脚手架搭建开发环境，在开始编码之前，在gayhub上搜了一下，发现有大神写了一个基于vue和electron的脚手架，看了文档后，发现正好适合我的需要，瞬间发现了新大陆。

项目名称：`electron-vue`

项目地址：[https://github.com/SimulatedGREG/electron-vue](https://github.com/SimulatedGREG/electron-vue)

项目文档(英文的)：[https://simulatedgreg.gitbooks.io/electron-vue/content/en/](https://simulatedgreg.gitbooks.io/electron-vue/content/en/)

> PS：在开始编码之前要仔细阅读文档。

### 工程目录
``` bash
│
├── README.md                           <=  项目介绍
├── app                                 <=  开发目录
│   ├── dist                            <= 编译打包
│   ├── icons                           <= 相关图标
│   ├── src                             <= 项目源代码
│   │   ├── main                        <= electron主进程
│   │   │   ├── application.js
│   │   │   ├── index.dev.js
│   │   │   ├── index.js
│   │   ├── renderer                    <= electron渲染进程
│   │   │   ├── App.vue                 <=  Vue 根组件
│   │   │   ├── main.js                 <=  Vue 入口
│   │   │   ├── assets                  <=  静态资源
│   │   │   ├── common                  <=  公共配置
│   │   │   ├── config                  <=  项目配置
│   │   │   ├── extend                  <=  Vue 扩展相关
│   │   │   ├── router                  <=  Vue 路由相关
│   │   │   ├── store                   <=  Vuex
│   │   │   ├── views                   <=  视图层
│   ├── index.ejs                       <= 模板文件
│   ├── package.json                    <=  相关依赖
├── build                               <=  打包桌面应用相关
│   ├── Gruntfile.js                    <=  构建脚本
│   ├── package.json                    <=  相关依赖
├── tasks                               <=  electron-packeger打包
│   ├── release.js
│   ├── runner.js
├── test                                <=  测试文件夹  
│   ├── e2e
│   ├── unit
│   ├── .eslintrc
├── config.js                           <=  electron打包配置
├── webpack.main.config.js
├── webpack.renderer.config.js
├── package.js
│
│
```

### 使用说明

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:9080
npm run dev

# build electron app for production
npm run build

# lint all JS/Vue component files in `app/src`
npm run lint

# run webpack in production
npm run pack

### login
username：water
password：123456
```
---
### 制作安装程序
打包完成后进入`build`目录，执行`grunt`命令

![](https://oc1gyfe6q.qnssl.com/17-11-2/91160373.jpg)

执行完成后会有`installer`目录，双击Setup.exe安装即可

![](https://oc1gyfe6q.qnssl.com/17-11-2/61565525.jpg)

### 效果预览

![](https://oc1gyfe6q.qnssl.com/17-8-13/94171252.jpg)

![](https://oc1gyfe6q.qnssl.com/17-8-13/63034830.jpg)

![](https://oc1gyfe6q.qnssl.com/17-8-13/51761758.jpg)

![](https://oc1gyfe6q.qnssl.com/17-8-13/20713678.jpg)
