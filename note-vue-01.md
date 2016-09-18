
## 引入 Vue.js

### 起因
- jQuery 的DOM操作与异步回调有天生的冲突
- Vue.js 的MVVM设计模式十分易于前后端分离——只需要后端提供接口
- Vue.js min + gzip后大小只有22kb，十分易于部署

### 环境搭建

使用了cooking搭建了Vue.js的调试和生产环境
> [用 cooking 搭建一个简单又优雅的 Vue 项目开发环境 (入门篇)](http://zhuanlan.zhihu.com/p/22387692)

使用stackedit.io、browsersync和腾讯云搭建了Vue.js笔记系统

### 学习
#### 声明式渲染 *Declarative Rendering*
##### **Text Interpolation *文本插入* **
```html
<div id="app">
  {{ message }}
</div>
```
```js
//新的Vue实例
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  }
})
```
> <div id="app"> {{ message }} </div>

![](http://7xtesn.com1.z0.glb.clouddn.com/ipic/2016-09-19-00%3A57%3A51.jpg)

 DOM会自动响应数据变化，修改 `app.message` 可看到实例的更新

##### **Directive Bind *指令绑定* **
```html
<div id="app-2">
  <span v-bind:id="id">Inspect me</span>
</div>
```
```js
var app2 = new Vue({
  el: '#app-2',
  data: {
    id: 'inspect-me'
  }
})
```
> <div id="app-2"><span v-bind:id="id">Inspect me</span></div>

同文本插入一样，绑定元素的`id`可以被看做Vue实例中的`id`
#### 条件和循环 *Conditionals and Loops *
##### 切换元素显示
```html
<div id="app-3">
  <p v-if="seen">Now you see me</p>
</div>
```
```js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

> <div id="app-3">   <p v-if="seen">Now you really see me</p> </div>

##### 列表循环
```html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ul>
</div>
```
```js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Learn JS' },
      { text: 'Learn Vue' },
      { text: 'Build sth awesome' }
    ]
  }
})
```
> <div id="app-4">   <ol>
>     <li v-for="todo in todos">
>       {{ todo.text }}
>     </li>   </ul> </div>

![](http://7xtesn.com1.z0.glb.clouddn.com/ipic/2016-09-19-00%3A58%3A51.jpg)
##### 输入的处理
###### 按钮事件绑定
```html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">
  Reverse Message
  </button>
</div>
```
```js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
> <div id="app-5">   <p>{{ message }}</p>
> <button v-on:click="reverseMessage">Reverse Message</button> </div>

![](http://7xtesn.com1.z0.glb.clouddn.com/ipic/2016-09-19-00%3A59%3A17.jpg)
###### 使用 `v-model` 指令让 input 与 app 的状态双向绑定
```html 
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
```js 
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```

> <div id="app-6">   <p>{{ message }}</p>   <input v-model="message">
> </div>

![](http://7xtesn.com1.z0.glb.clouddn.com/ipic/2016-09-19-00%3A59%3A45.jpg)

#### Composing with Components *构建组件* 
![组件树🌲](https://rc.vuejs.org/images/components.png)

* 组件就是预定义选项的Vue实例
* 使用 `prop` 来让组件的数据从父组件传递到子组件
* 逻辑解耦，子组件逻辑不影响父组件
##### 例子
```js
Vue.component('todo', {
  //props指要从父组件继承的属性（组件内的名称）
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```
使用 `v-bind` 绑定组件的数据
```html
<div id="app-7">
  <ol>
    <!-- v-for、message等属性属于父组件，需要通过v-bind绑定到子组件中 -->
    <todo v-for="ok in todos" v-bind:todo="ok"></todo>
  </ol>
</div>
```

> <div id="app-7">   <ol>
>     <todo v-for="ok in todos" v-bind:todo="ok"></todo>   </ol> </div>

![](http://7xtesn.com1.z0.glb.clouddn.com/ipic/2016-09-19-01%3A10%3A33.jpg)
