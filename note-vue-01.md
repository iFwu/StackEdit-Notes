
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
#### 声明式渲染
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
#### **Conditionals and Loops *条件和循环* **
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