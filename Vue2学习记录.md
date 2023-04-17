### Vue2学习记录

1. 直接引入Vue：
  ```html
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <!-- 生产环境版本，优化了尺寸和速度 -->
  <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
  ```
2. 使用Vue Cli，请注意我们不推荐新手直接使用 vue-cli，尤其是在你还不熟悉基于 Node.js 的构建工具时。
3. 介绍：
    * 文本插值，`<div id="app">{{ message }}</div>`；
    * v-bind 绑定元素attribute，`<spanv-bind:title="message"></span>`；
    * v-if 把数据绑定到 DOM 结构，`<p v-if="seen"></p>`；
    * v-for 可以绑定数组的数据来渲染一个项目列表，`<li v-for="todo in todos">{{ todo.text }}</li>`；
    * v-on 添加一个事件监听器，通过它调用在 Vue 实例中定义的方法，`<button v-on:click="reverseMessage"></button>`；
    * v-model 实现表单输入和应用状态之间的双向绑定，`<input v-model="message">`；
4. 组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用。在 Vue 里，一个组件本质上是一个拥有预定义选项的一个 Vue 实例。
    ```js
    Vue.component('todo-item', {
      // todo-item 组件现在接受一个
      // "prop"，类似于一个自定义 attribute。
      // 这个 prop 名为 todo。
      props: ['todo'],
      template: '<li>{{ todo.text }}</li>'
    })
    ```
5. 一个 Vue 应用由一个通过 new Vue 创建的根 Vue 实例，以及可选的嵌套的、可复用的组件树组成。
6. 当一个 Vue 实例被创建时，它将 data 对象中的所有的 property 加入到 Vue 的响应式系统中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。
7. 除了数据 property，Vue 实例还暴露了一些有用的实例 property 与方法。它们都有前缀 $，以便与用户定义的 property 区分开来。
    ```js
    vm.$data === data // => true
    vm.$el === document.getElementById('example') // => true
    // $watch 是一个实例方法
    vm.$watch('a', function (newValue, oldValue) {
      // 这个回调将在 `vm.a` 改变后调用
    })
    ```
8. 每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会。
9. created 钩子可以用来在一个实例被创建之后执行代码；也有一些其它的钩子，在实例生命周期的不同阶段被调用，如 mounted、updated 和 destroyed。生命周期钩子的 this 上下文指向调用它的 Vue 实例。
10. 插值：文本、原始HTML（v-html）、Attribute、JS表达式；
11. 指令 (Directives) 是带有 v- 前缀的特殊 attribute。一些指令能够接收一个“参数”，在指令名称之后以冒号表示。可以用方括号括起来的 JavaScript 表达式作为一个指令的参数。修饰符 (modifier) 是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。缩写：`v-bind=>:, v-on=>@`；
12. 计算属性：模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。对于任何复杂逻辑，你都应当使用计算属性。可以像绑定普通 property 一样在模板中绑定计算属性。可以将同一函数定义为一个方法而不是一个计算属性。不同的是计算属性是基于它们的响应式依赖进行缓存的。只在相关响应式依赖发生改变时它们才会重新求值。Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：侦听属性。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 watch——特别是如果你之前使用过 AngularJS。然而，通常更好的做法是使用计算属性而不是命令式的 watch 回调。
13. 侦听器：Vue 通过 watch 选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。使用 watch 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。
14. class对象语法，可以在这里v-bind:class绑定一个返回对象的计算属性。这是一个常用且强大的模式；v-bind:style内联样式也可以绑定一个样式对象：
    ```html
    <div v-bind:class="classObject" v-bind:style="styleObject"></div>
    ```
    ```js
    data: {
      isActive: true,
      error: null
    },
    computed: {
      classObject: function () {
        return {
          active: this.isActive && !this.error,
          'text-danger': this.error && this.error.type === 'fatal'
        }
      },
      styleObject: function () {
        return {
          activeColor: 'red',
          fontSize: 30
        }
      }
    }
    ```
15. class数组语法，可以把一个数组传给 v-bind:class，以应用一个 class 列表；v-bind:style数组语法可以将多个样式对象应用到同一个元素上：
    ```html
    <div v-bind:class="[activeClass, errorClass]" v-bind:style="[baseStyles, overridingStyles]"></div>
    ```
    ```js
    data: {
      activeClass: 'active',
      errorClass: 'text-danger'
    },
    ```
16. 当在一个自定义组件上使用 class property 时，这些 class 将被添加到该组件的根元素上面。这个元素上已经存在的 class 不会被覆盖。
17. v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
18.

