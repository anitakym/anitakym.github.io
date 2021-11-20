---
title: vue-daily-notes
date: 2021-04-04 16:14:11
tags:
---

## 文档概览

### 安装
https://cn.vuejs.org/v2/guide/installation.html
- 注意不同版本最合适用的场景（开发，生产）

### 模版语法
- 数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值（https://mustache.github.io/）

### 指令
- 可以简单不严谨的理解为有点像标志位，Vue底层根据标记做对应处理
- https://cn.vuejs.org/v2/guide/syntax.html#%E6%8C%87%E4%BB%A4
- v-if/v-else/v-for（因为模版语法只能表达式，无法语句，所以提供这些指令）

### 组件
- https://cn.vuejs.org/v2/guide/components.html#%E7%BB%84%E4%BB%B6%E7%9A%84%E7%BB%84%E7%BB%87
- 解决的问题：复用
- 页面抽象成组件树
- Vue.component()，如果通过这个注册组件，name要唯一的
- 注意组件中的data(function返回的对象)，vm中的data(对象) —— 因为组件要复用，一个组件的 data 选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立的拷贝
- template —— 模版字符串
- Prop 是你可以在组件上注册的一些自定义 attribute。当一个值传递给一个 prop attribute 的时候，它就变成了那个组件实例的一个 property。
- 如果没有props声明的一些属性，会默认挂在template的最外层（根）结点上
- why
  - 当method里面逻辑过多，相似逻辑 => 拆分成独立的方法
  - 当html类似，重复 => 拆分html
  - 同上，样式
  

### 事件
- https://cn.vuejs.org/v2/guide/events.html
- ```v-on:click="statement"```
- 事件修饰符：在事件处理程序中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。为了解决这个问题，Vue.js 为 v-on 提供了事件修饰符。（https://cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E4%BF%AE%E9%A5%B0%E7%AC%A6）
- 按键修饰符，按键码
- 自定义事件：https://cn.vuejs.org/v2/guide/components-custom-events.html
- 鼠标事件，移动端的事件

### 插槽
- https://cn.vuejs.org/v2/guide/components-slots.html
- Vue 实现了一套内容分发的 API，这套 API 的设计灵感源自 Web Components 规范草案，将 <slot> 元素作为承载分发内容的出口。
- 注意2.6语法：v-slot
- 可以当成较为复杂的属性来看，复杂的属性没法直接写在传递信息里面，所以利用插槽的方式传递复杂内容
- 具名插槽
- 作用域插槽：本质上是传递的是返回组件的函数

### 单文件组件(在guide的工具类别下)
- https://cn.vuejs.org/v2/guide/single-file-components.html
- @vue/cli 
  - vue --version
  - vue create test
  - Vue 3 => @vue/cli v4.5 => vue updrage --next
  - 可以自己设置选项
- components => 注册，作用域只在这个文件
- scoped，会在样式上面带上hash [data-xxxx]
- v-model 语法糖，简写 :value="message" @input="handleChange",本质上还是单向数据流(https://cn.vuejs.org/v2/guide/components-custom-events.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E7%9A%84-v-model)
- .sync(可关注Vue3的差异)

### 虚拟DOM
- jquery(事件，DOM => 随着逻辑的复杂，会比较乱)
- vue(事件，state，DOM) => Virtual DOM(state+template=>DOM树) => Virtual DOM Diff(时间复杂度) 
- 算法 => 时间复杂度，通用性
- 同层级节点比较 => 移动节点 ｜ 删除新建 | 更新删除新建(无key) | 移动(有key) | 插入(有key) => 有key就有唯一标识符了，就可以把一些更新删除新建的问题改成了移动和插入的问题 => index的问题：如果是自定义的组件，简单的展示问题不大，但是list如果有删除添加排序，就会有问题

### 组件更新的触发
- 数据驱动
- 没有特殊情况不要操作DOM！！！=> review代码的时候经常发现这个问题
- 数据来源(单向的)
  - 来自父元素的```属性```-外部数据(https://cn.vuejs.org/v2/guide/components-props.html#%E5%8D%95%E5%90%91%E6%95%B0%E6%8D%AE%E6%B5%81)
  - 来自组件自身的```状态```data-内部数据(https://cn.vuejs.org/v2/api/#data)
  - 来自状态管理器-vuex|Vue.observable(https://cn.vuejs.org/v2/api/#Vue-observable)

TIPS：
- 调试
<pre>
开发中，我们可以用console里面
var vm = new Vue({...})
修改 vm.testdata.testattr 
对实例进行修改调试
</pre>


### 