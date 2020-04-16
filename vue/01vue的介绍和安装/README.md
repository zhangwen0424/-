## 01 vue的介绍和安装

### Vue介绍（最新稳定版本：2.6.1）
Vue.js（读音 /vjuː/, 类似 view）  

1.是一套构建用户界面的渐进式框架（一套完整的解决方案，对项目侵入性大，中途需要跟换框架则需要重构整个项目）。

2.Vue 只关注视图层，易上手，有配套的第三方类库， 采用自底向上增量开发（功能迭代）的设计

3.提高开发效率，帮助减少不必要的dom操作；双向数据绑定，通过框架提供的指令，前端只需要关注业务逻辑，不再关心dom如何渲染（**MVVM**）

**MVVM**
 1、M（Model每个页面中单独的数据）、V（View每个页面的html结构）、VM（VM ViewModel提供数据的双向绑定）。VM是其中核心，。
 2、VM，M和V不直接关联，通过中间的VM（M和V间的调度者）。V想要保存数据到M，都要有VM做中间处理；V想要渲染页面，需要调用VM，VM从M中取数据。

**兼容性**

Vue **不支持** IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有[兼容 ECMAScript 5 的浏览器](https://caniuse.com/#feat=es5)


### vue安装

1.在 Vue.js 的官网上直接下载 vue.min.js 并用 ` <script> ` 标签引入(建议)
[下载开发版本](https://cn.vuejs.org/js/vue.js)  包含完整的警告和调试模式
[下载生产版本](https://cn.vuejs.org/js/vue.min.js)  删除了警告，33.30KB min+gzip

2.CDN引入
- 最新的版本，用于日常学习
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

- 链接到一个明确的版本号和构建文件，避免新版本造成的不可预期的破坏
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>

3.npm安装（推荐淘宝镜像cnpm）
![](https://github.com/zhangwen0424/web/raw/master/vue/images/npm%E5%92%8Ccnpm%E7%89%88%E6%9C%AC%E6%9F%A5%E7%9C%8B.png)


若未安装，可到[npm官方](https://www.npmjs.cn/)下载安装npm，安装好后可用之行`npm i cnpm`安装cnpm

快速搭建大型单页应用可使用vue-cli（后续介绍）

