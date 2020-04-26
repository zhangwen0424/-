## 02 vue基础实战
[查看项目源代码代码](https://github.com/zhangwen0424/web/tree/master/vue/02vue基础实战/03基础)

### vue动态绑定class
```
<div id="app">
  <!-- 方式1 -->
  <div class="container" v-bind:class="{active:isActive,line:isLine}">
    动态绑定class
  </div>
  <div class="container" v-bind:class="[a,b]">动态绑定class数组</div>
  <div class="container" v-bind:style="{color: mycolor,fontSize: myfont}">
    动态绑定style
  </div>
  <!-- 方式2 -->
  <div class="container" v-bind:class="classobj">
    动态绑定class
  </div>
  <div class="container" v-bind:class="classarr">动态绑定class数组</div>
  <div class="container" v-bind:style="styleobj">动态绑定style</div>
</div>

<script>
  var vue = new Vue({
    el: "#app",
    data: {
      isActive: true,
      isLine: true,
      a: "active",
      b: "line",
      mycolor: "blue",
      myfont: 25 + "px",
      classobj: { active: true, line: true },
      classarr: ["active", "line"],
      styleobj: { color: "blue", fontSize: "25px" },
    },
  });
</script>
```
