# 01 vue的介绍和安装

## Vue介绍（最新稳定版本：2.6.1）

1.Vue.js（读音 /vjuː/, 类似 view） 是一套构建用户界面的渐进式框架（一套完整的解决方案，对项目侵入性大，中途需要跟换框架则需要重构整个项目）。

2.Vue 只关注视图层，易上手，有配套的第三方类库， 采用自底向上增量开发（功能迭代）的设计

3.提高开发效率，帮助减少不必要的dom操作；双向数据绑定，通过框架提供的指令，前端只需要关注业务逻辑，不再关心dom如何渲染（**MVVM**）

**MVVM**
 1、把每个页面分成了M（Model）、V（View）、VM（VM ViewModel）。VM是其中核心，M和V间的调度者。
 2、M，保存的是每个页面中单独的数据（比如要渲染页面表格，ajax请求到后台的你个数组，此数据即为M）。
 3、V，每个页面的html结构。
 4、VM，一个调度者，分割了M和V，M和V不直接关联，通过中间的VM。V想要保存数据到M，都要有VM做中间处理；V想要渲染页面，需要调用VM，VM从M中取数据。
 5、前端中使用MVVM思想，主要让开发更方便，MVVM提供了数据的双向绑定（由VM提供）

**兼容性**

Vue **不支持** IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有[兼容 ECMAScript 5 的浏览器](https://caniuse.com/#feat=es5)



## vue安装

1.在 Vue.js 的官网上直接下载 vue.min.js 并用 ` <script> ` 标签引入(建议)

[下载开发版本](https://cn.vuejs.org/js/vue.js)  包含完整的警告和调试模式

[下载生产版本](https://cn.vuejs.org/js/vue.min.js)  删除了警告，33.30KB min+gzip

2.CDN引入

最新的版本，用于日常学习

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

链接到一个明确的版本号和构建文件，避免新版本造成的不可预期的破坏

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>

3.npm安装（推荐淘宝镜像cnpm）

![npm版本查看](https://github.com/zhangwen0424/web/blob/master/images/npm和cnpm版本查看.png 'npm版本查看')

若未安装，可到[npm官方](https://www.npmjs.cn/)下载安装npm，安装好后可用之行`npm i cnpm`安装cnpm

快速搭建大型单页应用可使用vue-cli（后续介绍）

