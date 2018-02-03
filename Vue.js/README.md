## 綁定屬性
v-bind
```html
<div v-bind:id="dynamicId"></div>
```

## 缩写

### v-bind 缩写

```html
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>
```

### v-on 缩写

```html
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>
```

### ticker
```
new Vue({
  el: '#app',
  data: {
    now: 0,
  },
  mounted: function () {
    this.$nextTick(function () {
      window.setInterval(() => {
        this.now = Math.trunc((new Date()).getTime() / 1000);
      },1000);
    })
  }
})
```

我们可以传给 v-bind:class 一个对象，以动态地切换 class：
<div v-bind:class="{ active: isActive }"></div>
上面的语法表示 active 这个 class 存在与否将取决于数据属性 isActive 的 truthiness。

<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>

<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
这样写将始终添加 errorClass，但是只有在 isActive 是 truthy[1] 时才添加 activeClass。 

<div v-bind:class="[{ active: isActive }, errorClass]"></div>



## 事件修饰符

在事件处理程序中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。
为了解决这个问题，Vue.js 为 v-on 提供了事件修饰符。之前提过，修饰符是由点开头的指令后缀来表示的。

.stop
.prevent
.capture
.self
.once

```html
<input v-on:keyup.13="submit">

<!-- 同上 -->
<input v-on:keyup.enter="submit">

<!-- 缩写语法 -->
<input @keyup.enter="submit">
```


## 双向数据绑定
v-model




## camelCase vs. kebab-case

HTML 特性是不区分大小写的。所以，当使用的不是字符串模板时，camelCase (驼峰式命名) 的 prop 需要转换为相对应的 kebab-case (短横线分隔式命名)：
```
Vue.component('child', {
  // 在 JavaScript 中使用 camelCase
  props: ['myMessage'],
  template: '<span>{{ myMessage }}</span>'
})
<!-- 在 HTML 中使用 kebab-case -->
<child my-message="hello!"></child>
```
