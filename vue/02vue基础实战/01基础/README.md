## 02 vue基础实战

[查看项目源代码代码](https://github.com/zhangwen0424/web/tree/master/vue/02vue基础实战/01基础)

### 第一个vue实例
- 1.使用script标签引入vue.js库文件，必须引入才能正常使用vue语法,引入js文件会暴露一个window.vue构造函数
- 2.body中规定vue挂载点，不能挂载到html标签以及body标签上，一个vue实例必须有且只有一个根节点  
- 3.vue声明变量用花括号输出
- 4.vue帮我们实现数据变动视图更新，适用数据量大，数据变化比较快的项目
   如：电商、论坛、直播、股票、金融、物流......
   一般企业网站，数据量变化较小，建议适用原生js写代码
```
<script src="vue.js"></script>

<div id="app">
  <div>{{message}}</div>
</div>

<script>
  var vue = new Vue({
    el: "#app", //vue启动的文档位置，也称为挂载点
    data: {
      message: "hello vue!", //设置传给html变量参数，body中花括号进行取值输出使用
    },
  });
</script>
```

### js代码输入到html页面中
js代码输入到html需要手动更改dom，对于数据变化大的业务场景，频繁修改dom会导致代码混乱，资源浪费
```
<div id="app"></div>

<script>
  // 选中id为app的元素
  var div = document.querySelector("#app");
  // 将要显示的数据
  var message = "hello js!";
  // 改变div元素内容，将message输出到div里面
  div.innerHTML = message;
  // 修改要显示的数据，页面不会自动发生改变
  message = "hello js changeed!";
  // 适用innerHTML改变页面数据显示
  div.innerHTML = message;
</script>
```

### vue数据绑定v-bind
v-bind是vue的内部指令，作用是将=后面的变量绑定到对应的html标签属性上
```
<div id="app">
  <span>显示当前时间:</span>
  <!-- 这里是把message这个变量绑定到input标签的value属性上 -->
  <input type="text" v-bind:value="message" style="width:400px"/>
</div>

<script>
  var vue = new Vue({
    el:"#app",
    data:{
      message: new Date(),
    }
  })
</script>
```

### vue条件判断语句v-if
- 可见的页面需满足：1在html中，2标签元素可见
- v-if指令用来控制标签是否编译成html(不再html中肯定不显示)，true时编译为html，false为不编译
- v-show指令标签都会编译为html中，true时显示元素，false隐藏元素
```
<div id="app">
  <ul>
    <li v-if="a">我在html中，你可以看到我</li>
    <li v-if="b">你看不到我,我也不在html里面</li>
    <li v-show="a">我在html中，可以看见我</li>
    <li v-show="b">我在html中，但是你不可以看见我</li>
  </ul>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {
      a: true,
      b: false,
    },
  });
</script>
```

### vue循环数组v-for
v-for 指令用来循环数组或对象
```
<div id="app">
  <ul>
    <!-- v-for 指令用来循环数组或对象 -->
    <li v-for="todo in todos">
      {{todo.text}}
    </li>
  </ul>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {
      todos: [
        {
          text: "我",
        },
        {
          text: "爱",
        },
        {
          text: "学",
        },
        {
          text: "习",
        },
      ],
    },
  });
</script>
```

### vue事件处理v-on
v-on指令用于在标签上挂载事件
```
<div id="app">
  <p>{{message}}</p>
  <button v-on:click="reverseMessage">点击反转字符</button>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {
      message: "hello vue!",
    },
    // methods定义vue程序的方法
    methods: {
      reverseMessage: function () {
        this.message = this.message.split('').reverse().join('')
      },
    },
  });
</script>
```

### vue双向绑定v-model
v-model作用为将视图中数据绑定到数据中
```
<div id="app">
  <!-- 将数据绑定到视图 -->
  <p>输入内容为：{{message}}</p>
  <!-- 将视图绑定到数据 -->
  <input type="text" v-model="message" />
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {
      message: "hello!",
    },
  });
</script>    
```

### vue创建组件
- 组件其实就是html标签，不过是我们可以自定义的标签，他怎么显示有我们自己定义
- 组件也可以理解为一段html模版代码，可以根据数据进行渲染，并且可以重复使用
- 每个组件都有自己独立的作用域范围，外面的数据进不来，组件内的数据出不去
- 组件需要先定义后使用，传入props数组定义组件接收的数据，template定义组件的模版
- 组件标签中通过v-bind传入组件的数据，传入props中
```
<div id="app">
  <ul>
    <!-- 组件即标签，且为我们自定义的标签 -->
    <todo-list v-for="item in list" v-bind:todo="item" v-bind:key="item.id"></todo-list>
  </ul>
</div>

<script>
  Vue.component("todo-list", {
    props: ['todo'],
    template: "<li>{{todo.text}}</li>"
  });
  // 初始化vue实例
  var vue = new Vue({
    el: '#app',
    data: {
      list: [
        {id: 0, text: "草莓"},
        {id: 1, text: "香蕉"},
        {id: 2, text: "苹果"}
      ]
    }
  })
</script>
```
