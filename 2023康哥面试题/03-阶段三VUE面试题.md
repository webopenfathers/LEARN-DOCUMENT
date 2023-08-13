# ■ 符号说明

💘 课题   

🌟 常见重要   

🌛 需要有印象的

🆕 v3新特性  



# ■ week1-day1 基本语法

## 💘 课题      

week1-day1  Vue基础（基本语法：简介、模板语法、列表渲染、条件渲染、事件处理）



## 🆕 先学vue3基本语法

```
<div id="root">
    <h1>{{msg}}</h1>

    <input type="text" v-model="content" />
    <button @click="addFn">添加</button>
    
    <ul>
        <li v-for="item in todos">{{item.id}} {{item.title}}</li>
    </ul>
</div>
<script src="https://unpkg.com/vue@next"></script>
<script>
// 以前：new Vue({el,data,methods....})
// 以前：new Vue({data,methods....}).$mount('#root')
// 现在：Vue.createApp({data,methods}).mount('#root')

Vue.createApp({
    data() {
        return {
            msg: "hello vue3",

            content: '',
            todos: [
                {id:1, title: '吃饭'},
                {id:2, title: '睡觉'},
                {id:3, title: '挤痘痘'},
            ]
        }   
    },
    methods: {
        addFn() {
            this.todos.push({
                id: this.todos.length,
                title: this.content
            })
        }
    }
}).mount('#root')
</script>
```



## 🌟 说出vue常用的指令

```
{{}} 两个大括号
v-text
v-html
v-bind  简写 :
v-for
v-if、v-else-if、v-else
v-show
v-on   简写 @

v-pre   跳过编译（几乎99%不会用）
v-once  仅渲染一次（几乎99%不会用）
v-cloak 插值闪烁问题  

v-model 第二天知识点
```

 

## 🌟  MVVM、MVC面试题

- 谈谈你对MVC的理解 

```
MVC是软件开发中常见的开发模式，主要应用于后端，将程序划分为M模型、V视图、C控制器从而便于团队协作开发，减少代码冗余
```

- 谈谈你对MVVM理解

```
MVVM是Model-View-ViewModel缩写，也就是将MVC中的Controller演变成ViewModel
Model层代表数据模型、
View层代表UI组件
ViewModel是Model、View层的桥梁，数据会绑定到ViewModel并自动将数据渲染到页面，视图变化会通知ViewModel层更新数据。

或者 

随着移动互联网的发展，MVVM思想借鉴MVC、MVP思想演变而来，M模型负责数据维护，V视图负责数据展示，VM则是M和V的桥梁，监控M模型数据变化自动更新V视图，从而解决传统前后端分离JQ架构弊端

开发者在代码中大量调用相同的 DOM API, 处理繁琐 ，操作冗余，使得代码难以维护。
大量的DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。
当 Model 频繁发生变化，开发者需要主动更新到View ；当用户的操作导致 Model 发生变化，开发者同样需要将变化的数据同步到Model 中，这样的工作不仅繁琐，而且很难维护复杂多变的数据状态。
```

- 谈谈MVVM和MVC区别

```
相同点：都是软件开发常见的开发模式或者开发思想
不同点：
1- MVC后端居多，MVVM前端
2- MVC单向通信 目的将M和V代码分离，MVVM则是双向通信，不需要手动操作DOM

或

最初MVC最早出现在后端   M代表模型负责数据处理、V代表视图负责数据战士、C代表控制器负责调度
后来前端也有了MVC库，最早实现的就是backbone.js 但是V和M并没有很好的解耦
因此出现了MVVM模式，
MVVM是Model-View-ViewModel缩写，也就是将MVC中的Controller演变成ViewModel
Model层代表数据模型、
View层代表UI组件
ViewModel是Model、View层的桥梁，数据会绑定到ViewModel并自动将数据渲染到页面，视图变化会通知ViewModel层更新数据。
```

> 多说一嘴：VUE不是纯MVVM框架 
>
> https://cn.vuejs.org/v2/guide/instance.html#%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA-Vue-%E5%AE%9E%E4%BE%8B 
>
> 虽然没有完全遵循 [MVVM 模型](https://zh.wikipedia.org/wiki/MVVM)，但是 Vue 的设计也受到了它的启发。因此在文档中经常会使用 `vm` (ViewModel 的缩写) 这个变量名表示 Vue 实例。



## 🌟  说一下v-show、v-if的区别

相同点：都可以用户判断控制元素隐藏显示

不同点：1-v-if语法更强、2-v-if控制DOM、v-show控制CSS

如何选：高频切换例如二维码、登录弹框、提示框、删除提示框、tab选项卡，推荐使用v-show 来减少DOM频繁删除创建所产生的额外性能开销



高逼格

```
v-if 是真正的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 “display” 属性进行切换。
所以，v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。
```





## 🆕 判断循环v-if、v-for优先级

- 手册

```
https://cn.vuejs.org/v2/guide/list.html#v-for-%E4%B8%8E-v-if-%E4%B8%80%E5%90%8C%E4%BD%BF%E7%94%A8
https://cn.vuejs.org/v2/guide/conditional.html#v-if-%E4%B8%8E-v-for-%E4%B8%80%E8%B5%B7%E4%BD%BF%E7%94%A8 
```

- 在 vue 2.x 中，在一个元素上同时使用 `v-if` 和 `v-for` 时， `v-for` 会优先作用。
- 在 vue 3.x 中， `v-if` 总是优先于 `v-for` 生效。


- vue2 

```
<div id="root">
    <h1>vue2 v-for>v-if（仅仅指同一个标签上）</h1>
    

    <!-- 判断假的，压根不会遍历 -->
    <div v-if="state">
    	<p v-for="item in todos">{{item.title}}</p>
    </div>

    <!-- 同一个标签先v-for走三次生成3个p  然后挨个判断都隐藏删掉   脱裤子放屁的感觉 -->
    <p v-for="item in todos" v-if="state">{{item.title}}</p>
    
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
const vm = new Vue({
    el: "#root",
    data: {
   	 	state: false,
    
        todos: [
            {id:1, title:'a'},
            {id:2, title:'b'},
            {id:3, title:'c'},
        ]
    }
})
</script>
```

- vue3  优化

```

<div id="root2">
    <h1>vue3 v-if > v-for</h1>
    
    
    <!-- 不循环 -->
    <p v-for="item in todos" v-if="state">{{item.title}}</p>

    <hr>
    

    <!-- 不循环 -->
    <div v-if="state">
    	<p v-for="item in todos">{{item.title}}</p>
    </div>

    <hr>

    <!-- 
        多学一招：为了避免指令写在同一个标签上可读性查，因此代码提升/指令提升 也就是将v-if写在父级标签上
        但是影响布局，
        解决用template标签  不会
    -->
    <template v-if="state">
    	<p v-for="item in todos">{{item.title}}</p>
    </template>
</div>
<script src="https://unpkg.com/vue@next"></script>
<script>
Vue.createApp({
    data() {
        return {
            state: true,

            todos: [
                {id:1, title:'a', show: true},
                {id:2, title:'b', show: false},
                {id:3, title:'c', show: true},
            ]
        }
    }
}).mount('#root2')
</script>
```







# ■ week1-day2  特殊语法

## 💘 课题      

week1-day2  Vue基础（特殊语法：表单输入绑定、购物车案例）



无，都在【week1-day6  Vue原理】课件中





# ■ week1-day3 花式思想

## 💘 课件

week1-day3  Vue基础（花式思想：Class与Style绑定、计算属性、侦听器、过滤器、自定义指令、ref属性、混入）



##  🌛 Class与Style绑定工作有用过吗

```
:class="item.icon"
:style="{ width: item.payload ? item.payload.width : '100%' }"
:style="{ width: item.width || '70px' }"

1-后台管理系统菜单   v-bidn:style="{width: 模型数据}"
2-主题色切换        
3-tab选项卡
4-其他

案例1：https://vant-contrib.gitee.io/vant/#/zh-CN/tab
源码1：https://unpkg.com/browse/vant@1.0.0/packages/tab/index.vue
案例3：https://element.eleme.io/#/zh-CN/component/tabs 
源码3：https://unpkg.com/browse/element-ui@2.15.5/packages/tabs/src/tab-bar.vue
案例3：https://element.eleme.io/#/zh-CN/component/button
源码3：https://unpkg.com/browse/element-ui@2.15.5/packages/button/src/button.vue
```





##  🌟 计算属性和侦听器区别、使用场景

计算属性：计算属性有缓存、并且是响应式依赖缓存，调用不加小括号

侦听器：侦听器无缓存，侦听模型数据变化，不能调用



计算属性：一个数据, 依赖另外一些数据 **“计算”** 而来的结果

```
利用vuex辅助函数，结合计算属性去显示数据 项目中大量使用
树型分类数据
等等复杂的逻辑，存在性能问题、或者避免重复调用存在性能问题的场景都可以使用计算属性。
```

侦听器：当需要监控模型数据变化时候

```
网站搜索
监控弹框显示二维码
模糊筛选、关键词筛选
日期筛选、下拉筛选
全选、全不选等
锋团Admin项目中监控路由变化显示对应面包屑
等等
```



> - 相同点
>
> 1. 语法角度（ a 从思想上都是普通方法升级版  b 都可以写函数或对象
> 2. 研发角度：计算属性-减少冗余、缓存提升性能、侦听器-减少DOM操作 符合VUE响应式思想
>
> - 不同点
>
> 1. 从语法角度：调用时，计算属性调用不加小括号，侦听器不能调用
> 2. 从功能角度：计算属性有缓存、响应式依赖，侦听器没有缓存常用于搜索、监控数据变化、代替事件等



##  🌟 watch监控失效场景&解决方案

针对于对象类型的数据，需要加deep属性深度监听/侦听





##  🌟 watch两大属性应用场景

- deep是什么哪里用

> a-锋团Admin项目中：监控路由变化，通过meta路由元信息重置面包屑🍞
>
> ```
> // watch: {
> //   // 针对于复杂类型的深度监听（注：深度监听场景）
> //   // params(newData) {
> //   //   console.log(newData);
> //   // },
> //   params: {
> //     deep: true,
> //     handler(newData) { // 也可以直接用日期组件的change事件
> //       console.log(newData);
> //  	   this.params.start_time = newData.date[0];
> //   		 this.params.end_time = newData.date[1];
> //     },
> //   },
> // },
> ```
>
> b-锋团Admin项目中：给角色分配权限 重置树🌲型控件
>
> ```
> editAuth.vue 
> // 获取所有权限  当前行数据变化获取最新的权限数据
> watch: {
>   row: {
>     deep: true,
>     handler() {
>       getAuthsApi().then((res) => {
>       	this.authsData = res.data;
>       });
>     },
>   },
> },
> ```
>
> C-锋团Admin项目中：基于elementui二次封装的form编辑默认显示数据要监控row变化
>
> ```
> watch: { // qf-form封装的表单组件中，编辑传递的row当前行数据变化同步更改
>    // row(newData) {
>    //   console.log("watch", newData);
>    // },
>    row: {
>      handler(newData) {
>         if (!newData) return;
>         this.formData = newData;
>     },
>     immediate: true,
>   },
> },
> ```

- immediate是什么哪里用

> a-锋团Admin项目中：meat路由元信息【首次】重置面包屑🍞
>
> ```
> watch: { // 监控路由变化同步面包屑
>   // $route(newData) {
>   //   // console.log(newData);
>   //   this.name1 = newData.meta.name1;
>   //   this.name2 = newData.meta.name2;
>   // },
>   $route: {
>     handler(newData) {
>       this.name1 = newData.meta.name1;
>       this.name2 = newData.meta.name2;
>     },
>   	immediate: true,
>   },
> },
>   
> ```
>
> b-锋团Admin项目中：基于elementui二次封装的form编辑默认显示数据要监控row变化
>
> ````
> watch: { // qf-form封装的表单组件中，编辑传递的row当前行数据变化同步更改
>    // row(newData) {
>    //   console.log("watch", newData);
>    // },
>    row: {
>      handler(newData) {
>         if (!newData) return;
>         this.formData = newData;
>     },
>     immediate: true,
>   },
> },
> ````



##  🌟 谈谈你对过滤器的理解有没有用过

作用：项目用来过滤数据，便于维护

语法：Vue.filter()

场景：订单状态、商品状态、性别、支付状态、发货状态。





##  🌟  谈谈你对混入的理解有没有用过

作用：复用组件里面的逻辑层，减少冗余便于维护

语法：Vue.mixin({data,methods....})

场景：锋团Admin项目中确认删除、接口操作后的提示重定向、jump重定向封装等等

场景：跳转封装this.$router.push 也是为了避免重复点击报错；也可以通过重置路由模块原型









##  🌛 自定义指令有没有用过

用过



全屏、复制剪切板、dialog对话框拖拽等等










# ■ week1-day4 组件编程

## 💘 课件

week1-day4  Vue基础（组件编程：组件化开发思想、组件封装、props、$emit、组件通信、插槽slot、仿写UI组件库、动态组件等）





## 🌟 为啥data要写函数里面返回对象

> 说明1
>
> ```
> 一个组件被复用多次，也就会创建多个实例，本质上都是基于同一个构造函数，如果data直接是对象，因为对象是引用类型，所以会影响到所有实例。
> 因此：为了保证组件不同的实例之间data不冲突，data必须是一个函数
> ```
>
> 或说法2
>
> ```
> 当一个组件被定义，data 必须声明为返回一个初始数据对象的函数，因为组件可能被用来创建多个实例。如果 data 仍然是一个纯粹的对象，则所有的实例将共享引用同一个数据对象！通过提供 data 函数，每次创建一个新实例后，我们能够调用 data 函数，从而返回初始数据的一个全新副本数据对象
> ```
>
> 或说法3
>
> ```
> 因为组件是用来复用的，且 JS 里对象是引用关系，
> 如果组件中 data 是一个对象，那么这样作用域没有隔离，
> 子组件中的 data 属性值会相互影响，如果组件中 data 选项是一个函数，
> 那么每个实例可以维护一份被返回对象的独立的拷贝，
> 组件实例之间的 data 属性值不会互相影响；而 new Vue 的实例，
> 是不会被复用的，因此不存在引用对象的问题。
> 
> 
> 
> function Component() {}
> Component.prototype.data = {
>   name: "jack",
>   age: 22,
> };
> var componentA = new Component();
> var componentB = new Component();
> componentA.data.age = 55;
> // componentA 和 componentB data之间指向了同一个内存地址，
> // 相互污染
> console.log(componentA, componentB);
> 
> 
> 
> function Component() {
>   this.data = this.data();
> }
> Component.prototype.data = function () {
>   return {
>     name: "jack",
>     age: 22,
>   };
> };
> var componentA = new Component();
> var componentB = new Component();
> componentA.data.age = 55; // 互补影响
> console.log(componentA, componentB);
> 
> 
> ps.
> let a = {}
> let b = {}   互补影响
> ----------
> let a = {}
> let b = a    相互影响（一个对象赋值给另一个对象  才会相互影响
> ```
>
> 





## 🌛谈谈你对单向数据流的理解

单向数据流指在组件化思想，开发的项目中，数据由根或者父组件传递给子组件，禁止🈲子组件中直接更改，而是由父更改后重新传递给子数据使用

```
// 在vue中 只能父数据传递给子 父修改后会自动同步到子
// 不允许子修改父  
// 生活中：你妈给你多少钱 就用多少，不允许你直接去拿 否则长大了完犊子
// 代码中：父给你就用，你自己直接改 容易后期搞懵逼谁串改了数据
```





## 🌟 如何实现组件通信？

常用：状态管理工具 vuex  
常用：父传子 props、子传父$emit、兄弟 eventBus
常用：slot插槽
概率：通过组件实例  ref获取、     =》   $parent获取、$root获取、$children获取
概率：v-model
了解：利用provide、inject





##  🌟 事件.native作用

概念：直接在组件上绑定原生事件

举例：使用elemenui、vantui封装的弹框、input等组件，需要使用官方原生事件





## 🌟 在组件上写原生事件失效解决方案

> 方法1：通过自定义事件重写原生事件
>
> 方法2：加.native修饰符



## 🌟 在组件上使用v-model原理

工作极少

但是笔试可能需要手写

```
<组件名 v-model="data中的键"></组件名>
<组件名 :value="data中的键" @input="data => data中的键 = data"></组件名>
```



## 🌛 修饰符.sync原理


```
<组件名 v-bind:属性名.sync="data中的键"></组件名>
<组件名 v-bind:属性名="data中的键"  @update:必须一样的属性名="data => data中的键 = data"></组件名>
```







# ■ week1-day5 剩余知识：生命周期、keep-alive等等

## 💘 课件

week1-day5  Vue基础（剩余知识：虚拟DOM、浏览器运行机制、回流重绘、生命周期、keep-alive、transition过渡



## 🌟 说出浏览器运行机制

浏览器主进程，负责创建和销毁tab进程、负责交互前进后退、负责网页文件下载等
渲染进程：每个tab对应一个渲染进程，下面有GUI渲染线程、JS引擎线程、事件线程、定时器线程、异步请求线程
GPU进程：负责3D图绘制
第三方插件进程：负责第三方插件处理，例如跨域、广告拦截插件等





## 🌟 说出浏览器输入网址干了啥

```
浏览器输入网址回车
去DNS服务器找网址对应的IP地址 
根据IP地址加端口访问服务器软件 
服务器返回数据
浏览器通过renderer是渲染进程处理，
其中GUI线程主要负责页面布局，解析HTML、CSS构建DOM树、CSS规则树、然后结合成渲染树、最终绘制显示
```





## 🌛 说出JS为什么是单线程

> ### 先看一个比喻
>
> 进程就是一个公司，每个公司都有自己的资源可以调度；公司之间是相互独立的；而线程就是公司中的每个员工(你，我，他)，多个员工一起合作，完成任务，公司可以有一名员工或多个，员工之间共享公司的空间
>
> ### 什么是进程？
>
> 进程：是cpu分配资源的最小单位；（是能拥有资源和独立运行的最小单位）
>
> ### 什么是线程？
>
> 线程：是cpu调度的最小单位；（线程是建立在进程的基础上的一次程序运行单位，一个进程中可以有多个线程）
>
> #### 浏览器是多进程的
>
> 放在浏览器中，每打开一个tab页面，其实就是新开了一个进程，在这个进程中，还有ui渲染线程，js引擎线程，http请求线程等。 所以，浏览器是一个多进程的。
>
> ### 大家都在说js是单线程的，但是为什么要设计成单线程？
>
> 这主要和js的用途有关，js是作为浏览器的脚本语言，主要是实现用户与浏览器的交互，以及操作dom；这决定了它只能是单线程，否则会带来很复杂的同步问题。 举个例子：如果js被设计了多线程，如果有一个线程要修改一个dom元素，另一个线程要删除这个dom元素，此时浏览器就会一脸茫然，不知所措。所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变.
>
> #### 为了利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程，但是子线程完全受主线程控制，且不得操作DOM。所以，这个新标准并没有改变JavaScript单线程的本质。





## 🌛 说出JS是单线程 为什么不存在执行效率问题

JS是单线程执行程序代码，形成一个执行栈，挨个处理；

但是遇到特别耗费时间的代码 ，例如异步请求，事件等，

不会堵塞等待执行，而是交给浏览器其他线程处理后，再丢到执行栈中处理，从而保证还行效率



   

## 🌟 谈谈你对回流重绘的理解

回流/重排：页面布局流发生改变就叫做回流，例如：width、height、border、top等
重绘：重绘元素自身的样式发生改变但是不会影响布局流，例如：color、background、box-shadow等



## 🌟 哪些属性导致回流、哪些属性导致重绘

例如：width、height、border、top等
例如：color、background、box-shadow等

```
1、添加或删除可见的DOM元素
2、元素的位置发生变化
3、元素的尺寸发生变化（包括外边距、内边框、边框大小、高度和宽度等）
4、内容发生变化，比如文本变化或图片被另一个不同尺寸的图片所替代。
5、页面一开始渲染的时候（这肯定避免不了）
6、浏览器的窗口尺寸变化（因为回流是根据视口的大小来计算元素的位置和大小的）

而重绘是指在布局不变得情况下，比如background-color,或者改动一下字体颜色的color等。
```



## 🌟 如何避免或减少回流重绘

> **JavaScript优化法**
>
> ```
> （1）避免频繁操作样式，最好一次性重写style属性，或者将样式列表定义为class并一次性更改class属性。
> （2）避免频繁操作DOM，创建一个documentFragment，在它上面应用所有DOM操作，最后再把它添加到文档中，也就是虚拟DOM
> （3）避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
> ```
>
> 
>
> **CSS优化法**
>
> ```
> （1）使用 transform 替代 top
> （2）使用 visibility 替换 display: none ，因为前者只会引起重绘，后者会引发回流（改变了布局
> （3）避免使用table布局，可能很小的一个小改动会造成整个 table 的重新布局。
> （4）尽可能在DOM树的最末端改变class，回流是不可避免的，但可以减少其影响。尽可能在DOM树的最末端改变class，可以限制了回流的范围，使其影响尽可能少的节点。
> （5）避免设置多层内联样式，CSS 选择符从右往左匹配查找，避免节点层级过多。
> （6）将动画效果应用到position属性为absolute或fixed的元素上，避免影响其他元素的布局，这样只是一个重绘，而不是回流，同时，控制动画速度可以选择 requestAnimationFrame，详见探讨 requestAnimationFrame。
> （7）避免使用CSS表达式，可能会引发回流。
> （8）将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点，例如will-change、video、iframe等标签，浏览器会自动将该节点变为图层。
> （9）CSS3 硬件加速（GPU加速），使用css3硬件加速，可以让transform、opacity、filters这些动画不会引起回流重绘 。但是对于动画的其它属性，比如background-color这些，还是会引起回流重绘的，不过它还是可以提升这些动画的性能。
> ```





## 🌟 谈谈你对虚拟DOM的理解



通过js对象来描述真实的DOM，从而减少回流重绘





> 减少了同一时间内的页面多处内容修改所触发的浏览器reflow和repaint的次数，可能把多个不同的DOM操作集中减少到了几次甚至一次，优化了触发浏览器reflow和repaint的次数。。



## 🌟 说出VUE有哪些生命周期并说出应用场景



before开头的实际不用

非before开头

````
created   异步请求
mounted   异步请求、DOM操作（swiper、echarts、聊天默认滚到底部）
updated   监控数据变化进一步DOM操作，例如聊天窗口到底部、订单可视化图表重置等等
destroyed 清理非vue资源防止内存泄露，例如登陆倒计时定时器
````

剩余

```
activated	   组件被keep-alive缓存后，执行场景场景数据，例如添加后列表更新最新数据
deactivated  组件被keep-alive缓存后代替destroyed工作
errorCaptured 当页面发生错误是优雅降级，显示友好提示页面，react框架提示就是参考这一做法
```



> tips
>
> 优雅降级(`graceful degradation`)：一开始就构建站点的完整功能，然后针对浏览器测试和修复。 
>
>  ive enhancement`)：一开始只构建站点的最少特性，然后不断针对各浏览器追加功能。



渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进，达到更好的用户体验。 

优雅降级：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。



2109班面试追问

```
问1：created、和mounted区别
答1：created不可以dom操作 
问2：真的不可以吗
答2：可以通过 this.$nextTick()
问3：父子组件嵌套、生命周期执行顺序 created、mounted
答2：大方向  父created、子created、子mounted、父mounted
```





## 🌟 created里面可以操作DOM吗

通过ref不行，原生JS可以，因为该钩子函数触发还没有编译（不推荐

非要通过ref操作，可以写this.$nextTick来实现

```
<div id="root">
  <button ref="btn">a</button>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  const vm = new Vue({
    el: "#root",
    data: {},
    created() {
      let btnObj = document.querySelector("button");
      console.log("js可以", btnObj);
      console.log("ref不行🚫", this.$refs.btn);

      this.$nextTick(() => {
        console.log("ref可以", this.$refs.btn);
      });
    },
  });
</script>
```



> 追问1：created 定时器打印1   this.$nextTick 打印2   定时器打印3
>
> 回答1:  2、1、3
>
> 追问2：created Promise.then打印1   this.$nextTick 打印2   定时器打印3
>
> 回答2：1、 2、 3

```
// 追问1：created 定时器打印1   this.$nextTick 打印2   定时器打印3
// 回答1:  2、1、3
// setTimeout(() => console.log(1), 1000) 
// // Promise.resolve().then(() => console.log(2))
// this.$nextTick(() => console.log(2))
// setTimeout(() => console.log(3), 1000) 

// 追问2：created Promise.then打印1   this.$nextTick 打印2   定时器打印3
// 回答2：1、 2、 3
// Promise.resolve().then(() => console.log(1)) 
// this.$nextTick(() => console.log(2))
// setTimeout(() => console.log(3), 1000) 
```





## 🌛 watch与created() 哪个先执行？

watch 中的 immediate 会让监听在初始值声明的时候去执行监听计算，否则就是 created 先执行

````
<div id="root">
  <h1>{{msg}}</h1>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      msg: "hello",
    },
    created() {
      console.log("后created");
    },
    watch: {
      msg: {
        handler() {
          console.log("先watch");
        },
        immediate: true,
      },
    },
  });
</script>

````



## 🌛数据可视化 echarts

在项目中的使用细节，数据的使用，修改，销毁？



细节1：首次实例化渲染，mounted中注意dom是否挂载，特别是操作子组件

细节2：重置echarts数据，如果页面没有遍历显示数据明细，无法在updated钩子函数监控

> 解决：watch或者更新后直接调用methods方法

细节3：重置echarts数据，得重新实例化才能显示最新数据

细节4：离开组件手动关闭连接  ws.close()  （注：如果定时器写的要清除定时器





## 🌟 谈谈你对keep-alive的理解，并说出应用场景

vue中内置组件，主要将组件相关数据缓存到内存中，避免重复挂载卸载产生的性能开销

场景：后台管理系统数据、移动端长列表、tab选项卡等



周边问题

> 1-缓存组件使用哪个属性？
>
> ```
>   :include、:exclude、:max
> ```
>
> 2-此时多的哪两个钩子函数？ 
>
> ```
> activated 、deactivated
> ```
>
> 3-页面加载刷新的时候，被缓存的组件，会执行其中的方法吗？   
>
> ```
> 刷新就相当于首次打开  所以created、activated又重新出发
> ```

 



## 🌟 谈谈你对$nextTick的理解，并说出应用场景

理解：vue中用来确保，在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

场景：对话框放登录二维码，放表单选项获取数据、获取焦点，点击事件修改对话框状态后开始加载DOM，为确保能获取并操作DOM使用$nextTick包起来。

语法:

```
// 修改数据
vm.msg = 'Hello'
// DOM 还没有更新
Vue.nextTick(function () {
  // DOM 更新了
})

// 作为一个 Promise 使用 (2.1.0 起新增，详见接下来的提示)
Vue.nextTick()
  .then(function () {
    // DOM 更新了
  })
```





> vue确保模型数据更新完毕之后执行$nextTick里面的callback代码

  

## 🌟 说出$nextTick原理

> Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。Vue 在内部对异步队列尝试使用原生的 Promise.then、MutationObserver 和 setImmediate，如果执行环境不支持，则会采用 setTimeout(fn, 0) 代替。



Vue底层监控的数据更新会开启一个队列进行优化处理，然后在下一个的事件循环中去触发nextTick的callback执行，也就是会把nextTick的callback依次尝试放到用原生的 Promise.then、MutationObserver 和 setImmediate、setTimeout中，底层核心代码大致思路如下

```
1. 把回调函数放入callbacks等待执行
2. 将执行函数放到微任务或者宏任务中
3. 事件循环到了微任务或者宏任务，执行函数依次执行callbacks中的回调
```



https://github.com/vuejs/vue/blob/dev/src/core/global-api/index.js#L46

https://github.com/vuejs/vue/blob/dev/src/core/util/next-tick.js#L87

```
export function nextTick (cb?: Function, ctx?: Object) {
  let _resolve
  callbacks.push(() => { // 将拿到的回调函数存放到数组中
    if (cb) {
      try { // 错误捕获
        cb.call(ctx)
      } catch (e) {
        handleError(e, ctx, 'nextTick')
      }
    } else if (_resolve) {
      _resolve(ctx)
    }
  })
  if (!pending) { // 如果当前没有在pending的时候，就会执行timeFunc
    pending = true
    timerFunc() // 多次执行nextTick只会执行一次，timerFunc就是一个异步方法
  }
  if (!cb && typeof Promise !== 'undefined') {
    return new Promise(resolve => {
      _resolve = resolve
    })
  }
}
//
```

https://github.com/vuejs/vue/blob/dev/src/core/util/next-tick.js#L33

```
const callbacks = []
let pending = false

function flushCallbacks () {
  pending = false
  const copies = callbacks.slice(0)
  callbacks.length = 0
  for (let i = 0; i < copies.length; i++) {
    copies[i]()
  }
}


let timerFunc

//判断1：是否原生支持Promise
if (typeof Promise !== 'undefined' && isNative(Promise)) {
  const p = Promise.resolve()
  timerFunc = () => {
    p.then(flushCallbacks)
    if (isIOS) setTimeout(noop)
  }
  isUsingMicroTask = true
} else if (!isIE && typeof MutationObserver !== 'undefined' && (
	//判断2：是否原生支持MutationObserver
  isNative(MutationObserver) ||
  MutationObserver.toString() === '[object MutationObserverConstructor]'
)) {
  let counter = 1
  const observer = new MutationObserver(flushCallbacks)
  const textNode = document.createTextNode(String(counter))
  observer.observe(textNode, {
    characterData: true
  })
  timerFunc = () => {
    counter = (counter + 1) % 2
    textNode.data = String(counter)
  }
  isUsingMicroTask = true
} else if (typeof setImmediate !== 'undefined' && isNative(setImmediate)) {
  //判断3：是否原生支持setImmediate
  timerFunc = () => {
    setImmediate(flushCallbacks)
  }
} else {
  //判断4：上面都不行，直接用setTimeout
  timerFunc = () => {
    setTimeout(flushCallbacks, 0)
  }
}
```







# ■ week1-day6  Vue原理

## 💘 课题

week1-day6  Vue原理（语法原理：v-model语法原理、响应式原理、Vue源码分析、自定义Vue库）



##  🌟 说一下v-model原理

v-model其实是个语法糖底层是基于【:value】和【@input】 封装

```
<input type="text" :value="msg" @input="msg = $event.target.value">
```

  

##  🌟 VUE2响应式原理（中级）

Vue2在初始化数据时，会使用Object.defineProperty语法对data中的所有属性进行数据劫持，如果属性发生变化就会通知进行更新操作



##  🌟 VUE2响应式原理（高级）

````
底层通过Object.defineProperty进行数据劫持，然后通过发布订阅通知视图更新。

或者

vue在初始化数据时，会使用Object.defineProperty重新定义data中所有属性，当页面使用对应属性时，首先会进行依赖收集（watcher，如果属性发生变化就会通知相关依赖进行更新操作（发布订阅。
并且底层针对于对象、数组做了特殊处理，对象类型多次递归，数组类型重写数组方法
````



##  🌟 VUE2响应式数据无法劫持原因、和解决方案

原因：是因为原生Object.defineProperty针对复杂数据修改无法劫持，因此无法通知视图更新

解决：

```
自己解决：递归全搞定
VUE解决：
1-对象递归
2-数组重写（因为深度监听需要递归到底，而数组相对数据很多，一次性计算量大  所以改用重写方式）
3-增加额外api 
this.$forceUpdate()   
this.$set(this.data数据, 要劫持得数组索引或对象键, 默认值)
```



##  🌟 $forceUpdate 原理

这个之前有大概看过源码 

就是notify强制视图所有数据更新 



##  🌟 $set 原理

1、他是vue原型上的一个方法

> https://github.com/vuejs/vue/blob/dev/src/core/instance/state.js#L345
>
> https://github.com/vuejs/vue/blob/dev/src/core/instance/state.js#L14

2、这个之前有大概看过源码

主要两大核心

1、通过defineReactive进行数据劫持

2、通过notify进行视图更新

> https://github.com/vuejs/vue/blob/dev/src/core/observer/index.js#L201





##  🌛 $delete 原理 

删除对象的属性。如果对象是响应式的，确保删除能触发更新视图。这个方法主要用于避开 `Vue` 不能检测到属性被删除的限制，但是你应该很少会使用它。

  

语法：this/Vue.$delete(target，propertyName/index)



1、他是vue原型上的一个方法

> https://github.com/vuejs/vue/blob/dev/src/core/instance/state.js#L346 
>
> https://github.com/vuejs/vue/blob/dev/src/core/instance/state.js#L14

2、这个之前有大概看过源码

主要两大核心

1、通过delete 删除对象的属性

2、通过notify进行视图更新

> https://github.com/vuejs/vue/blob/dev/src/core/observer/index.js#L236





## 🌟 Vue.set/delete 原理

https://github.com/vuejs/vue/blob/0603ff695d2f41286239298210113cbe2b209e28/src/core/global-api/index.js#L44



```
import { set } from '../observer/index'

...
Vue.set = set
...
```





```
import { set } from '../observer/index'

...
Vue.prototype.$set = set
...

```



都是从 ../observer/index 文件中导出的

区别在于Vue.set()是将set函数绑定在Vue构造函数上，this.$set()是将set函数绑定在Vue原型上。



 

##  🆕 响应式原理

为啥VUE3要选择proxy和reflect

```
- Object.defineProperty 拦截的是对象的属性，会改变原对象。 proxy 是拦截整个对象，通过 new 生成一个新对象，不会改变原对象。
- proxy 语法更强，拦截方式除了上面的 get 和 set ，还有 11 种，以前就6个
- proxy 特性更强，可以监听未定义的，针对于N层则get时判断递归添加proxy拦截即可
```

不用reflect可以吗

```
- 简单场景可以，复杂场景不行
- 举例：https://blog.csdn.net/qq_34629352/article/details/114210386  存在BUG
- 其次：用了更方便推荐结合用 例如 has、deleteProperty、defineProperty友好提示等
```













# ■ week2-day1  路由相关

## 💘 课件

week2-day1  Vue进阶（项目准备：路由、重定向、路由模式、路由原理、路由参数、路由传参、嵌套路由、命名视图、导航守卫、路由addRoute）



## 🌛 路由-对象里面的键

{  

​	path,

​	component,

​	name,

​	redirect,

​	alias 

​	children,

​	components

​	meta

   ....

}



## 🌟 路由-你说下vue路由模式有几种？ 

<https://router.vuejs.org/zh/api/#mode> 

常用路由模式有2个，分别为hash和history  直接修改路 由构造函数加个mode键即可

准确说有3个，hash/history用于客户端，abstract用户服务端





## 🌟 路由-你说下vue路由原理？



首先vue路由是基于SPA单页面应用思想去开发的

利用BOM API 来使用



hash模式        通过 BOM  location对象的hash属性来改变路由   window.onhashchange

history模式     通过BOM history对象的pushState方法来改变路由    window.onpopstate





## 🌟 路由-history有什么问题，如何解决？

刷新无法加载网页问题

可以通过服务器配置来解决





## 🌟 路由-什么是单页面应用SPA优缺点，如何选择

SPA优点：减少HTTP请求、加载响应数据、提高用户体验度，方便增加动画
SPA缺点：首屏加载过慢、不利于SEO优化（就是百度可以搜到你）  

如何选择
根据项目需求，老板没有明确说就不管，
但是老板说需要seo优化则通过：Vue.js 服务器端渲染（nuxt.js）   



> tips
>
> 1-为什么单页面(SPA)网站无法被seo？：https://www.zhihu.com/question/416192007/answer/1424413130
>
> 2-多页面应用(MPA)也就是二升三锋团PC项目也是不利于seo优化，最终是否利于seo主要还是看页面数据是直接和html一起返回的、还是要重新发送ajax请求的。
>
> 3-vue中想利于seo则通过nuxt.js技术，react则通过next.js



##  🌟 路由-参数周边种类、方式

参数种类：query、params

传参方式

```
query、path
this.$router.push( {query, path} )		定义路由时【不用管】刷新【不丢失】

params、name 写冒号  
this.$router.push( {params, name} )  定义路由时【需要管】刷新【不丢失】 

params、name 不写冒号
this.$router.push( {params, name} )  定义路由时【不用管】刷新【丢失】
```





##  🌟 路由-谈谈你对编程式导航的理解

作用：就是利用js跳转网页

留心：声明式就是用a标签跳转

场景：登陆、添加按钮、删除按钮等

语法

```
this.$router.push( { path:'/路径', query: {参数名:值} } )
this.$router.push( { name:'名称', params: {参数名:值} } )

获取：this.$route.query/params.参数名
```



##  🌟 路由-说出嵌套路由&命名视图的场景

嵌套路由

```
概念：一个路由，显示多个组件，并且有父子关系所以通过children来定义
语法：子路由通过children来定义，然后父的组件内容通过router-view来显示匹配的子组件
场景：后台管理系统经典两栏布局 点击左侧菜单，右侧显示子组件内容
```



命名视图

```
概念：一个路由，显示多个组件，并且有兄弟关系所以component改为components
语法：定义路由把component改为components，然后视图给router-view 加name属性
场景：移动端navBar、tabBar
```





##  🌟 路由-全局导航守卫登陆鉴权

作用；没登陆不可以访问会员中心、后台首页

语法：router.beforeEach    判断h5  next

```
// 全局前置守卫
// 导航守卫：导航/地址栏门卫，监控路由变化
router.beforeEach((to, from, next) => {
  // ...
  // to 存放新的路由数据
  // from 存放旧的路由数据
  // next()    写- 允许后续代码执行，可以看到组件内容
  // next()   不写- 阻止后续代码执行，因此组件不渲染看不到内容
  // next({path: '/login'}) 跳转到login页面

  // console.log(to);
  // 检查当前访问的路径
  // 在数组中就直接next 不用检查是否登录
  // 白名单
  if (["/login", "/404"].includes(to.path)) {
    next();
  } else {
    // 上述白名单直接忽略不用判断
    // 但是其他得判断
    let token = localStorage.getItem("token");
    if (token) {
      next();
    } else {
      next({ path: "/login" });
    }
  }
```





##  🌟 路由-导航守卫种类&作用

种类：全局、路由、组件

> ```
> 全局：beforeEach				 登录状态、网页加载进度条
> 全局：beforeResolve	    不用（路由、组件守卫被解析也就是被调用后）
> 全局：afterEach			    关闭网页加载进度条 NProgress
> 
> 路由：beforeEnter		    不用
> 
> 组件：beforeRouteEnter   组件被创建前（注：不能用this）
> 组件：beforeRouteUpdate   动态路由匹配/动态获取路由参数
> 组件：beforeRouteLeave   未保存离开组件/清除定时器/切换组件保存数据等
> ```
>
> 

全局

> **全局前置守卫** beforeEach		  
>
> ````
> 场景1：登录验证，判断用户是否登录，登录-next()，没登录-重定向到登录页 next({path:'/login'})
> 场景2：显示网页加载进度条
> 
> 
> // 导航守卫（监控路由变化）
> // to 路由对象（新页面路由对象  to.path 可以获取当前新页面路由路径
> // form 路由对象（旧页面路由对象  form.path 可以获取当前旧页面路由路径
> // next 函数  可以控制页面正常访问或者重定向
> import store from "@/store";
> import router from "@/router";
> import NProgress from "nprogress";
> import "nprogress/nprogress.css";
> 
> const whiteList = ["/login", "/404", "/login/sms", "/login/token"];
> 
> router.beforeEach((to, from, next) => {
>   NProgress.start();
>   // ...
>   // 1 判断你访问的是什么页面
>   if (whiteList.indexOf(to.path) != -1) {
>     next();
>   } else {
>     // 登录相关的页面、404 直接next
>     // 其他 判断token是否存在
>     // let token = this.$store.state.login.token
>     let token = store.state.login.token;
>     // - 存在 next({})
>     // - 不存在 next({path: '/login'})
>     if (token) {
>       if (store.state.auths.menus.length <= 0) {
>         console.log("重新获取权限菜单");
>         store.dispatch("auths/FETCH_MENUS");
>       }
>       next();
>     } else {
>       next({ path: "/login" });
>     }
>   }
> });
> 
> router.afterEach(() => {
>   NProgress.done();
> });
> 
> ````
>
> **全局解析守卫**beforeResolve    2.5.0+
>
> ```
> 场景：不用
> 触发：路由、组件守卫被解析也就是被调用后
> ```
>
> **全局后置钩子**afterEach
>
> ```
> 场景：关闭网页加载进度条 NProgress
> 触发：最后、特色没有next不会改变导航本身：
> 
> 
> router.afterEach(() => {
>   NProgress.done();
> });
> ```

路由

> ```
> {
> 	path,
> 	component,
> 	...
> 	beforeEnter: (to, from, next) => {
> 	// ...
> }
> }
> ```
>
> 

组件

> ```
> Vue.component(组件名, {
> 	beforeRouteEnter    组件被创建前（注：不能用this）
> 	beforeRouteUpdate (2.2 新增)   动态路由匹配/动态获取路由参数
> 	beforeRouteLeave   未保存离开组件/清除定时器/切换组件保存数据等
> })
> 
> beforeRouteLeave (to, from, next) {
> // 禁止用户在还未保存修改前突然离开
> const answer = window.confirm('Do you really want to leave? you have unsaved changes!')
> if (answer) {
>  next()
> } else {
>  next(false)
> }
> }
> 或
> beforeRouteLeave (to, from, next) {
> window.clearInterval(this.timer) //清楚定时器
> next()
> }
> 或
> beforeRouteLeave (to, from, next) {
>  // 当用户需要关闭页面时, 可以将公用的信息保存到session或Vuex中
>  localStorage.setItem(name, content); //保存到localStorage中
>  next()
> }
> ```





##  🌛 路由-导航守卫执行顺序

```
导航被触发。
在失活的组件里调用 beforeRouteLeave 守卫。
调用全局的 beforeEach 守卫。
在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
在路由配置里调用 beforeEnter。
解析异步路由组件。
在被激活的组件里调用 beforeRouteEnter。
调用全局的 beforeResolve 守卫 (2.5+)。
导航被确认。
调用全局的 afterEach 钩子。
触发 DOM 更新。
调用 beforeRouteEnter 守卫中传给 next 的回调函数，创建好的组件实例会作为回调函数的参数传入。
```

beforeRouteLeave 组件离开

beforeEach       全局

beforeRouteUpdate  组件更新

afterEach     全局

beforeRouteEnter    组件进入







##  🌟 路由-动态路由如何实现

面试提问

````
如何实现权限控制
如何实现菜单权限
如何实现动态路由
如何动态添加路由规则
项目是前端路由还是后端路由
````

实战项目回答

````
见下面👇 
````



作用&语法

> 作用：不同角色，权限菜单看到的不一样
>
> 步骤1：页面菜单导航根据接口数据渲染
>
> 步骤2：路由不能全部写死，而是全部注释掉，利用addRoutes或addRoute动态添加路由规则
>
> ````
> 举个栗子：商品列表、用户列表、权限列表、订单列表等等
> 1、api目录定义接口导出
> 2、组件内导入
> 3、最后组件内的created钩子函数中调用
> 
> 
> 
> 动态路由特殊：
> 1-首先api目录定义接口导出
> 2-接着在vuex auth文件中去定义actions获取权限菜单数据
> 然后再全局导航守卫beforeEach中判断用户登录了，但是没有菜单数据 就通过dispatch触发actions获取权限菜单数据 
> 
> 目的1：登录页  跳转到  欢迎页    beforeEach  发现vuex中没有菜单数据  请求接口保存到vuex中
> 目的2：后期页面刷新vuex就丢了，没事 刷新页面也就是路由变化了 beforeEach 也会触发   发现vuex中没有菜单数据  请求接口保存到vuex中
> 
> 
> 
> 或
> 1、在vuex中定义actions获取权限菜单数据   actions拿到数据后 触发mutations添加动态路由addRoute并且保存到模型中
> 2、在全局导航守卫中   判断vuex中是否有权限菜单数据 ，没有就触发actions 去获取权限菜单数据 并保存到模型中
> ````







##  🌟 路由-元信息有啥用

meta 存放面包屑、也可以加标识控制是否缓存组件

实现1：页面菜单导航根据接口数据渲染

实现2：路由不能全部写死，利用addRoutes或addRoute动态添加路由规则



```
router.addRoute("admin", {
  path: twoMenu.url,
  component: () => import("@/views/" + twoMenu.component),
  meta: {
    name1: twoMenu.auth_pname,
    name2: twoMenu.auth_name,
    keep_alive: twoMenu.keep_alive,
  },
});
```



##  🌛 路由-过渡特效场景

项目中会用到

```
<transition class-enter-class="animated 类名">
  <router-view></router-view>
</transition>
```





# ■ week2-day2  脚手架相关

## 💘 课件

week2-day2  Vue进阶（项目准备：脚手架、ToDoList案例、组件封装、全局组件、Vue.config.js配置）

  



##  🌟 说出框架中做了哪些配置vue.config.js

别名

跨域（最终上线还得后端或运维处理

移出console

图片压缩

引入外部CDN

等等 



面试追问：为啥要引入外部cdn  

回答：减轻应用/代码服务器压力/并发，请求负载均衡/分发到其他服务器（注：银行原来有一个取款机，现在有n个）



## 🌟 说出跨域的解决方案

常用的

谷歌命令

谷歌插件

JSONP

http-proxy-middleware

等等



追问：项目中如何配置

```
vue中配置  devServer  配置就可以了
```

追问：在哪个文件中

```
vue.config.js 中

module.exports = {
	 // ...
	 devServer: {}
	 // ...
}
```



##  🌟 说出Vue.use原理

Vue.use主要用来在框架中全局注册插件，例如注册全局的组件等，

然后底层源码大致做了两件事

```
1 检查传递的插件有没有重复注册
2 判断plugin.install是不是函数 或 plugin 是不是函数  然后分别用apply调用让函数执行  注册，

Vue.component(组件名, 单文件组件)
```

源码 https://github.com/vuejs/vue/blob/dev/src/core/global-api/use.js

````
export function initUse (Vue: GlobalAPI) {
  // 接受一个plugin参数，限制为 Function | Object两种类型
  Vue.use = function (plugin: Function | Object) {
    // _installedPlugins 存储所有注册过的 plugin
    const installedPlugins = (this._installedPlugins || (this._installedPlugins = []))
    // 保存注册组件的数组，不存在则创建，存在则直接返回，不允许重复注册
    if (installedPlugins.indexOf(plugin) > -1) {
      return this
    }

    // additional parameters
    // 将传入的参数转换成数组
    const args = toArray(arguments, 1)
    // 将Vue对象拼接到数组头部
    args.unshift(this)
    // 如果提供了 install 方法，则直接调用
    if (typeof plugin.install === 'function') {
      // 如果组件是对象，且提供install方法，调用install方法将参数数组传入，改变`this`指针为该组件
      plugin.install.apply(plugin, args)
    } else if (typeof plugin === 'function') {
      // 否则直接执行
      plugin.apply(null, args)
    }
    // 将plugin存储到  installedPlugins，表示y已经注册过
    installedPlugins.push(plugin)
    return this
  }
}

````


```
/**
 * Convert an Array-like object to a real Array.
 */
export function toArray (list: any, start?: number): Array<any> {
  start = start || 0
  let i = list.length - start
  const ret: Array<any> = new Array(i)
  while (i--) {
    ret[i] = list[i + start]
  }
  return ret
}
```





# ■ week2-day3  UI组件库

## 💘 课件

week2-day3  Vue进阶am（项目准备：UI组件库ElemenUI、IView、AntdV、Vant、Mint等、自研UI组件库）





##  🌛 说出UI组件库/UI框架原理

步骤1：首选通过vue单页面应用定义好公共组件

步骤2：定义所有UI组件导出入口文件 src/components/index.js

```
import Kuangkuang from '@/components/kuangkuang/Index.vue'
import Page from '@/components/page/Index.vue'

export default Vue => {
 // 语法：Vue.component(后期调用的组件名, 单文件组件)
 // 注册：后期就可以直接调用，不需要单独导入
 // Vue.component('qfui-kuangkuang', Kuangkuang)
 // Vue.component('qfui-page', Page)
 // Vue.component(Kuangkuang.name, Kuangkuang)
 // Vue.component(Page.name, Page)

   const coms = [Kuangkuang, Page]
   coms.forEach(com => {
     Vue.component(com.name, com)
   })
}
```

步骤3：接着打包

> ```
> "scripts": {
>  "serve": "vue-cli-service serve",
>  "build": "vue-cli-service build",
>  																			    	       打包后文件名 打包后存的目录  打包的组件在哪
>  																									      -----			   ----		------------------
>  "build:ui": "vue-cli-service build --target lib --name qf-ui --dest dist2 ./src/components/index.js"
> },
> ```



步骤4：最后按照node包发布就可以使用



# ■ week2-day4/5  Vue锋团项目布局

##  🌟 项目开发中有没有封装过组件

有

或者用语言：开发过





##  🌟 项目中封装了哪些组件

有很多，

比如封装了公共的table、form等组件，

还有很多页面组件，例如例如编辑用户、分配角色，分配权限、门店创建、分类编辑等都有封装提取页面组件，从而便于后期维护





##  🌟 组件如何封装的

页面组件：首先在页面中完成功能，然后再views/模块名/components中定义单文件组件，然后导入使用，从而让组件更便于后期维护

> 概念：将组件中不同逻辑的代码提取封装，便于后期维护



公共组件：首先在src/components定义form公共组件，然后全局注册导入使用，最终根据需求利用props接受参数&创建自定义事件





##  🌟 样式相关

- 题目1：如何防止样式的污染？

```
scoped
```

- 题目2：scoped解决样式污染原理

> 说明：vue在编译的时候通过在DOM元素以及css样式上加上唯一标记，实现样式私有化，不污染全局样式。
>
> 举例：
>
> ```
> <div class="my-class"></div>
> 编译为
> <div class="my-class" data-v-56e7f952></div>
> 对应的样式.my-class编译为
> .my-class[data-v-56e7f952]
> ```
>
> 原理：利用前端自动化构建工具webpack结合PostCSS模块编译实现css模块化
>
> https://www.postcss.com.cn/   

- 题目3：项目中开启样式私有化后，无法修改子组件例如elementui、antdv如何解决

```
通过【深度作用选择器】，你可以使用 >>> 操作符；有些像 Sass 之类的预处理器无法正确解析 >>>。这种情况下你可以使用 /deep/ 或 ::v-deep 操作符取而代之——两者都是 >>> 的别名，同样可以正常工作。   
```

https://vue-loader.vuejs.org/zh/guide/scoped-css.html#%E6%B7%B1%E5%BA%A6%E4%BD%9C%E7%94%A8%E9%80%89%E6%8B%A9%E5%99%A8 





##  🌟 用户角色权限三者是如何关联的

首先在权限管理可以添加删除权限，实现后端路由

接着可以添加删除角色，然后给角色分配权限

最后在用户管理给用户分配角色，

后期不同用户登录就可以看到不同点权限菜单/导航







# ■ week3-day1  异步请求

## 💘 课件

week3-day1  Vue基础（项目准备：axios、fetch数据请求



##  🌟 谈谈你对HTTP理解

```
超文本传输协议、规定客户端和服务端如何通信，

他是是请求行，响应行，请求头，响应头，请求体，响应体组成，
之前我做项目的回收 请求行你们主要查看请求地址、请求状态、请求方式、请求体头里面主要放cookie、token、content-type等，请求体主要看参数有没有传递给后端、响应体后端返回的数据进行项目调试。
```

##  🌟 谈谈你对状态码的理解

```
2xx  200成功 201成功并创建新资源
3xx  301永久重定向 302临时重定向 304浏览器缓存
4xx  400参数有误 401密码错误 403无权访问 404文件不存在 405请求方式有误
5xx  500服务器错误
```



##  🌟 post、get区别

```
安全角度   post对象安全 get地址栏 后期可以通过历史记录查看登陆密码
数据角度   get地址栏 不同浏览器地址栏长度限制   post后端规定 2M 8M
```



##  🌟 xhr、fetch区别

```
xhr、fetch

相同点：1-都可以发送异步请求、2-都是ECMA定义的
不同点：前者异步回调地狱，后者promise
```



> 其他了解
>
> ```
> 最初ajax（XMLHttpRequest ECMA组织）   瑕疵：1-语法麻烦太多，2-异步回调地狱，3-语法有兼容性问题
> 后台jq（第三方作者） 
> 	明确：JQ里面的$.ajax/get/post是基于XMLHttpRequest封装的  function + ajax + callback
> 	好处：语法更简单、解决很多兼容性问题
> 	瑕疵：异步回调地狱还在
> 
> 	解决：通过promise技术
> 
> 最后fetch（ECMA组织）  ：结合promise技术而生，代替传统xhr
> ```



##  🌟 fetch、axios区别

```
相同点：1 都可以发送异步请求，2 都是promise
不同点：1 fetch官方、axios社区，2 axios更强并发、拦截器等
```



##  🌟 axios之前有没有封装过

````
- 封装axios导出request实例对象（timeout、baseURL、headers content-type、.env
- 请求拦截器（开启Loading、token
- 响应拦截器-成功（关闭Loading、res.data.data过滤 、 接口权限、TOKEN过期
- 响应拦截器-失败（关闭Loading、timeout处理 、404、canceled、邮件报警捕捉前端异常
````



##  🌟  axios原理

基于xmlhttprequest构造函数、和node中的http模块封装实现，动态判断浏览器环境、还是服务端环境

去选择对应语法返回promise对象

 



##  🌟 跨域如何解决

常用的

谷歌命令

谷歌插件

前端代理 http-proxy-middleware

JSONP



留心：不管前端咋操作最终上线都得后端或者服务器配置





追问：项目中如何配置

```
vue中配置  devServer  配置就可以了
```

追问：在哪个文件中

```
vue.config.js 中

module.exports = {
	 // ...
	 devServer: {}
	 // ...
}
```





# ■ week3-day2  状态管理vuex相关

## 💘 课件

week3-day2  Vue进阶（项目准备：VUEX单库、VUEX数据持久化b、VUEX单库模块化、VUEX框架模块化b）



##  🌟 说出vuex有哪些键

```
state、getters、mutations、actions、plugins、modules
```





##  🌟 说出vuex工作流

```
state存放数据、
getters过滤
mutations更新
actions异步请求
```





##  🌟 说出vuex数据持久化

H5存储

第三方模块





## 🌟 2109

```
问1：vuex工作流
答1：通过state定义状态、通过getters过滤状态、通过mutations更新状态、通过actions异步请求
 - 追问：里面具体怎么写、或者面试官问的是vuex具体怎么写的？
 - 回答：state是对对象 里面写键:值，getter是对象  里面写函数  返回过滤的数据，mutations 是对象  里面写函数  形参是state。
 - 追问：vuex在项目中怎么用？
 - 回答：store文件中通过module模块化定义状态，然后通过辅助函数mapState、mapMutations去获取
 - 追问：具体场景呢？
 - 回答：比如我之前做xxx项目，登录成功之后用户名、角色、token、权限菜单等等就是存在vuex中，然后通过辅助函数获取显示；
 - 追问：怎么获取state的数据怎么取？
 - 回答：可以通过 this.$store.state.键获取   但是我之前做xxx项目主要使用vuex的辅助函数mapState
 - 追问：vuex属性之间的联系，还有辅助函数
 - 回答：getter过滤state里面，mutations去更新state里面，actions主要发送异步请求然后触发mutations更新state里面的数据；
 - 追问：为什么在action里面写异步请求，而不会mutation
 - 回答：首先mutation也可以写异步请求，但是官方推荐在action里面写，从而确保拿到数据之后再更新状态，避免mutation写异步请求存在同步异步问题，也就是拿到数据【之前】更新了状态。
 
问2：vuex有哪些键x
vuex中的键，和其他工作流，具体mutation和action的相同点，怎么用
问3：vuex怎么用
问4：vuex数据是永久的还是临时的
```







# ■ week3-day3/4/5  Vue锋团项目接口

##  🌟 说一下登录如何实现的

1、通过elementui布局 表单验证

2、给登录绑定点击事件，...  

3、然后通过vuex辅助函数 调用 actions 去请求接口

4、失败弹框提示，成功将token、uname、roleName存储vuex中，然后提示登录成功&&重定向



```
1 vuex周边问题 比如数据持久化、比如有哪些键
2 axios周边问题
3 token周边问题（过期问题
```





##  🌟 如何判断用户是否登录

##  🌟 登录是如何鉴权的

通过全局导航守卫判断，白名单直接next、非白名单判断h5或vuex中是否存在  不存在重定向到 登录页即可





##  🌟 说一下token过期机制

纯前端处理

```
1 登录既要存token  又要额外存一个时间
2 axios请求拦截器里面  判断是否过期 提示token过期，然后就重定向到登录页
```



前后端结合处理

```
1 登录就存token晚吃
2 请求拦截器每次请求携带token
3 相应拦截器判断是否过期  提示token过期，过期就重定向登录页
```



##  🌟 项目中是前端路由还是后端路由

##  🌟 权限菜单如何实现的

后端路由



追问：后端路由如何实现的？

回答：几个关键词  请求接口、addRoute、菜单还的遍历搞出来、vuex

```
1、首先通过vuex定义actions获取当前用户的权限数据，然后触发mutations、保存到state中、并且通过addRoute添加动态路由
2、在导航守卫中判断store中的权限数据是否存在，存在next不存在全局导航守卫beforeEach触发action获取



3、后台首页layout下面的menu中通过辅助函数获取遍历显示
```



其他备注：一般token有效期7200s  也就是2小时  具体看公司





##  🌟 ....













​    

## 🌟 项目做了哪些优化

- 交互角度

````
animate.css     
vue-lazyload  
nprogress
loading
preventReClick
等
````

-  代码角度

```
混入
过滤器
页面组件提取封装
公共组件提取封装
axios封装
全局配置文件  process.env
等等
```

- 性能角度  webpack

```
关闭prefetch预加载 
图片压缩  		  原理：image-webpack-loader
引入外部cdn  	   原理：configureWebpack  -> externals 
UI框架按需加载    原理：babel-plugin-import 实现自动按需引入
路由/组件懒加载   原理：es6 import动态加载 + webapck文件分割
等等
```

- 性能优化  web server 或 code

```
nginx服务器配置：开启强制缓存expires缓存（注：这个单词cookie中碰到过）
nginx服务器配置：开启gzip压缩
keep-alive组件缓存
等等
```



​    

## 🌟 说出路由懒加载原理

es6 动态导入 + webpack文件分割



> 普通导入：import  组件名  from  路径及文件名      打开就触发
>
> 动态导入：component: () => import(路径及文件名)   访问才触发



## 🌟 周边：async、await具体怎么用的

就是钩子函数中、或者vuex的actions中不经常需要写api请求接口吗

然后通过async、await来修饰完成功能



举例：比如权限菜单、各种登录咱们都用了



# ■ 查缺补漏





##  🌟 说一下Diff算法

算法规则

```
1 步骤一：用JS对象模拟DOM树
2 步骤二：比较两棵虚拟DOM树的差异（切记切记切记：一层一层比）
3 步骤三：把差异应用到真正的DOM树上
4 步骤四：在页面展示

虚拟DOM介绍：https://www.jianshu.com/p/616999666920  
如何实现一个Virtual DOM 算法：https://github.com/livoras/blog/issues/13 
深入理解Diff算法：https://blog.csdn.net/lunahaijiao/article/details/86741739
```



```
<div id="root">
    <div v-for="item in todos">
        <input type="checkbox" name="" id="">
        {{item.title}}
    </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
const vm = new Vue({
    el: "#root",
    data: {
        todos: [
            {id:1, title:'吃饭'},
            {id:2, title:'睡觉'},
            {id:3, title:'挤痘痘'},
        ]
    }
})
</script>

步骤1：通过浏览器运行 ，给第二个checkbox打钩
步骤2：在控制台 vm.todos.splice(1,1)
```







什么是虚拟DOM：就是使用javascript的对象来描述了DOM结构

为什么要虚拟DOM：提升性能（因为回流、重绘   浏览器工作机制）

如何更新DOM数据：通过diff算法（同层比较）

```
1 步骤一：用JS对象模拟DOM树
2 步骤二：比较两棵虚拟DOM树的差异(注：后期如果写写遍历 加上:key 提升性能的)
3 步骤三：把差异应用到真正的DOM树上
```

切记：当遍历数据的时候要写key   提升性能、也是避免BUG









# ■ 周边



## 🌟 【事件循环】谈谈你对Event Loop的理解

`Event Loop`即事件循环，

是指浏览器或`Node`的一种确保javaScript单线程运行时不会阻塞的一种机制，

也就是我们经常使用**异步**的原理。    



种类：浏览器的Event Loop、Node.js中的Event Loop



## 🌟 【事件循环】谈谈你对浏览器的Event Loop理解

  浏览器输入网址服务器响应数据后，

浏览器会通过render进程开始解析工作

GUI线程负责页面渲染

JS引擎线程负责执行JS代码

遇到异步代码会交给其他线程处理，然后放到队列中，

事件循环主要是从队列中取出代码放到执行栈中交给js引擎线程处理





## 🌛【事件循环】谈谈你对Node.js中的Event Loop理解



> libuv引擎中的事件循环分为 6 个阶段，它们会按照顺序反复运行。每当进入某一个阶段的时候，都会从对应的回调队列中取出函数去执行。当队列为空或者执行的回调函数数量到达系统设定的阈值，就会进入下一阶段。



```
timers 阶段：这个阶段执行timer（setTimeout、setInterval）的回调
I/O callbacks 阶段：处理一些上一轮循环中的少数未执行的 I/O 回调
idle, prepare 阶段：仅node内部使用
poll 阶段：获取新的I/O事件, 适当的条件下node将阻塞在这里（轮训阶段）  
check 阶段：执行 setImmediate() 的回调
close callbacks 阶段：执行 socket 的 close 事件回调
```







## 🌟 【事件循环】说出宏任务、微任务各有哪些



> 单词含义：I input 输入、 O output 输出 
>
> 用户角度IO操作：鼠标键盘-是计算机输入信息，显示器-是输出设备
>
> 电脑角度IO操作：CPU、内存与其他设备之间数据转移过程就是IO操作，例如数据从磁盘读到内存，或者内存写到磁盘
>
> 编程角度IO操作：进程读取数据操作



- 宏任务：

```
整体代码（script）
定时器（setTimeout、setInterval）
I/O操作（DOM事件、AJAX异步请求）

setImmediate（node环境）
requestAnimationFrame（浏览器环境）
```

- 微任务

```
Promise.then catch finally
async/await（底层还是promise）
process.nextTick（node环境） 
MutationObserver（浏览器环境）
```





## 🌟 【事件循环】说出先执行宏任务还是微任务

算整体代码script：1宏n微

不算整体代码script：先n微，再1宏 ->  n微，再1宏



## 🌟 【事件循环】浏览器和node中event loop区别

浏览器：一个宏走完清空所有微任务

node：一个阶段走完  再清空所有微
