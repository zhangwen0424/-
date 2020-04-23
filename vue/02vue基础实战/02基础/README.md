## 02 vue基础实战
[查看项目源代码代码](https://github.com/zhangwen0424/web/tree/master/vue/02vue基础实战/02基础)
### vue实例
- 只有在data挂载的字段才是双向绑定（视图跟随数据变化），其他数据无法做到
- 实例化vue后可以直接访问data里面的数据 
- 不可以通过实例添加一个不存在的属性，如需添加即使没有值（null,undefined）也要在data中声明变量，否则视图中访问该变量报错
```
<div id="app">
  <p>a:{{a}}</p>
  <p>b:{{b}}</p>
</div>

<script>
  var data = {
    a: 1,
    b: null,
  };
  var vue = new Vue({
    el: "#app",
    data: data,
    methods: {
      say: function () {
        console.log("hi!", this.a);
      },
    },
  });
  console.log("vue.a:", vue.a); //1
  data.a = 3;
  console.log("data.a:", vue.a); //3
  vue.a = 3;
  console.log("vue.a:", vue.a); //3
  vue.b = "hello"; 
  vue.say(); //3
</script>
```

### vue阻止双向绑定freeze
阻止修改和添加对象的值:Object.freeze();
```
<div id="app">
  <p>ab:{{ab}}</p>
  <button v-on:click="ab='afd'">修改ab的值</button>
</div>

<script>
  var obj = { ab: 1231 };
  Object.freeze(obj);
  var vue = new Vue({
    el: "#app",
    data: obj,
  });
  // 访问vue的数据
  console.log("vue.ab:", vue.ab, vue.$data); //vue.ab: 1231 {ab: 1231}
  // 访问vue根元素
  console.log("vue.$el:", vue.$el); //vue.$el: (#app的node节点)
  //  实例化vue传入的参数数据
  console.log("vue.$options:", vue.$options);
  // freeze后无法修改vue的data数据
  vue.$watch("ab", function (newval, oldval) {
    console.log(`新值为：${newval}`);
    console.log(`旧值为：${oldval}`);
  });
</script>
```

### vue实例上的方法$on
v-on是注册一个自定义事件，用$emit调用事件
```
<div id="app">
  <p>message: {{message}}</p>
  <button v-on:click="test">点击修改数据</button>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: { message: "hello!" },
    methods: {
      test: function(){
        this.$emit('test', 'hi!')
      }
    },
  });
  // 注册一个自定义事件，事件名字为test
  vue.$on('test', function(msg){
    this.message = msg;
  });
</script>
```

### vue生命周期函数
```
<div id="app">
  <p>{{message}}</p>
  <button v-on:click="message='hello vue!'">点击我更新数据</button>
  <button v-on:click="destroy">点击我销毁vue实例</button>
</div>

<script>
  var vue = new Vue({
    el:"#app",
    // vue生命周期函数
    beforeCreate() {
      console.log('开始创建前。。。')
    },
    created() {
      console.log('创建完成了。。。')
    },
    beforeMount() {
      console.log('开始挂载了。。。')
    },
    mounted() {
      console.log('挂载完成了。。。')
    },
    beforeUpdate() {
      console.log("开始更新了。。。")
    },
    updated() {
      console.log('更新完成了。。。')
    },
    beforeDestroy() {
      console.log('开始销毁了。。。')
    },
    destroyed() {
      console.log('销毁结束。。。')
    },
    data:{message:'测试数据'},
    methods: {
      destroy: function(){
        vue.$destroy();
      }
    },
  })
</script>
```

### vue的模版语法
- v-once阻止标签上的双向绑定,只取初始值
- v-text以text的格式输出，有元素标签的会显示标签
- v-html以html的格式输出，有元素标签的会把标签生成元素显示
- 支持简单的表达式格式输出，不支持js语句输出
```
<div id="app">
  <span v-once>{{msg}}</span><br />
  <span>{{msg}}</span><br />
  <span v-bind:id="msg" v-text="msg"></span><br />
  <span v-bind:id="msg" v-html="msg"></span><br />
  <span>{{num+1}}</span><br />
  <span>{{bool?true:false}}</span><br>
  <!-- 不支持js语句 -->
  <!-- <span>{{console.log(num)}}</span> -->
  <button v-on:click="msg='hello'">修改数据</button>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {
      msg: "<li>hello vue</li>",
      num: 10,
      bool: false,
    },
  });
</script>
```

### vue指令参数、修饰和缩写
- `v-on:click`缩写为: `@click`
- `v-bind:id`缩写为: `:id`
```
<div id="app">
  <!-- 冒号后面是指定的参数，进一步说明指令的类型或其他信息 -->
  <p v-on:mouseover="console">鼠标移入。。。</p>
  <p v-on:id="'abc'"></p>
  <a v-on:click.prevent="console" href="https://github.com/zhangwen0424"
    >点击我阻止默认行为</a
  >
  <!-- v-on指令的缩写 -->
  <p @mouseover="console">鼠标移入。。。</p>
  <!-- v-bind指令的缩写 -->
  <p :id="'abc'"></p>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {},
    methods: {
      console: function () {
        console.log(new Date());
      },
    },
  });
</script>
```

### vue中getter和setter函数原理
`Object.defineProperty(obj, prop, desc)`
直接在一个对象上定义一个新属性，或者修改一个已经存在的属性
  - obj 需要定义属性的当前对象
  - prop 当前需要定义的属性名
  - desc 属性描述符
属性描述符有两种形式，且不能混合使用，分别为数据描述符，存取描述符
  - 1.数据描述符 --特有的两个属性（value,writable）
  - 2.存取描述符 --是由一对 getter、setter 函数功能来描述的属性，进行更精准的控制对象属性
```
<script>
  console.log("数据描述符......");
  var obj0 = {
    num: 1, //数量
    price: 10, //单价
  };
  Object.defineProperty(obj0, "total", {
    value: 1000,
    writable: true, //设置是否可写,默认不可写
  });
  console.log("total:", obj0.total); //total: 1000
  obj0.total = 2000;
  console.log("total:", obj0.total); //total: 2000
  console.log("obj0:", obj0); //obj0: {num: 1, price: 10, total: 2000}

  console.log("存取描述符......");
  var obj = {
    num: 1, //数量
    price: 10, //单价
  };
  Object.defineProperty(obj, "total", {
    // 访问total时调用get函数
    get: function () {
      console.log("get...");
      return this.num * this.price;
    },
    // 修改total时调用set函数
    set: function (val) {
      console.log("set...");
    },
  });
  obj.num = 5;
  console.log("total:", obj.total);
  obj.total = 100;
  console.log("total:", obj.total);
  console.log("obj:", obj);
  /*
  get...
  total: 50
  set...
  get...
  total: 50
  obj: {num: 5, price: 10}
  */
</script>
```

### vue计算属性computed
- 计算属性依赖于其他属性，是通过一系列复杂运算得出的结果
- 他会直接调用getter函数，如果参与计算的其他属性发生变化，计算属性会重新计算
- 属于数据与数据之间的绑定关系
```
<div id="app">
  <p>原来的信息：{{message}}</p>
  <p>计算后的信息：{{reverseMessage}}</p>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: { message: "hello" },
    computed: {
      reverseMessage: function() {
        return this.message.split('').reverse().join('');
      }
    },
  });
</script>
```

### js构造函数
- 用 new 关键字来调用的函数，称为构造函数,构造函数首字母一般大写
- 函数体内部的 this 指向该内存,构造函数执行过程的最后一步是默认返回 this 
- 每当创建一个实例的时候，就会创建一个新的内存空间
- 使用new调用构造函数，执行以下几步：
   - 1.创建一个this变量，该变量指向一个空对象
   - 2.该对象继承函数的原型属性和方法加入this引用的对象中
   - 3.返回this对象
    ```
    function Test(name){
      var this = {};
      this.name = name;
      this.say = function(){
        return "I am "+name;
      }
      return this;
    }
   ```
   - 如果直接调用函数，this对象指向为window，并且不回返回任何对象
    ```
    function Test(name) {
      // if (!(this instanceof Test)) {
      //   console.log('没有new这个Test类实例')
      //   return new Test(name);
      // }
      this.name = name;
      this.val = 12;
    }
    Test.prototype.say = function () {
      console.log("I am " + this.name);
    };

    var obj = new Test("mornki");
    console.log("obj.val", obj.val, obj.name); //obj.val 12 mornki
    obj.say(); //I am mornki
    var obj1 = new Test("xiaoming");
    console.log("obj1.val", obj1.val, obj1.name); //obj1.val 12 xiaoming
    obj1.say(); //I am xiaoming

    var people = Test("mornki");
    console.log(people); //undefined
    console.log(window.name); //mornki
    ```
