# Vue的学习

## Vue基础

### Vue的认识

- Vue是一个优秀的**前端框架**，开发者按照Vue的规范进行开发。

### Vue的特点

- 数据驱动**视图**可以让我们只关注数据，完全解耦：数据和视图  =>响应式数据 => 数据变化 =>视图一定变化。
- **MVVM** 双向绑定  => v-model => 数据变化 => 视图变化   视图变化 => 数据变化 ；
- 当下各种新框架都采用了**类Vue**或者**类React**的语法去作为主语法，微信小程序/MpVue/uni-app ；
- 通过指令增强了html功能新特性，开发者一般只需要关注数据。

### 实例化Vue对象

步骤：

```html
1. body中,设置Vue管理的视图<div id="app"></div>
2. 引入vue.js
3. 实例化Vue对象 new Vue();
4. 设置Vue实例的选项:如el、data...     
	new Vue({选项:值});
5. 在<div id='app'></div>中通过{{ }}使用data中的数据
```

### Vue实例选项

#### el（管理视图）

- **作用**：当前Vue实例管理所管理的html视图；
- **值**：**通常**是id选择器(或者是HTMLElement实例)  ，而且el一旦确定,就不再更改；
- **注意**：
  - el管理的视图不能是HTML和body。
  - class选择器 只匹配第一个满足条件的元素（Vue实例 => 管理视图 1对1）。

```js
new Vue({
// el: '#app' ,  id选择器
// el: '.app',   class选择器
el: document.getElementById("#app") // dom对象
})
```

#### data（数据）

**`数据驱动视图`**=> 数据变化 => 视图一定变化  所以只需要关注数据；

- Vue实例的数据对象，是响应式数据(数据驱动视图) 数据变化 => 视图变化；
- 可以通过**vm.$data**访问原始数据对象；
- Vue 实例也代理了 data 对象上所有的属性，因此访问**vm.a**等价于访问 **vm.$data.a**；
- 视图中绑定的数据必须**显式**的初始化到data中；
- 数据对象的更新方式 直接 采用**实例.属性 = 值**；

```js
var vm = new Vue({
el:"#app",
data:{
showMessage: false,
}
})
console.log(vm.showMessage)
vm.showMessage = true
```

#### methods（方法的集合）

- methods是一个**对象**；可以直接通过 Vue 实例对象访问这些方法，或者在**插值表达式中使用**。
- 方法中的 `this` 自动绑定为 Vue 实例。同样所有的方法也被代理到了Vue实例对象上，都可通过this访问。
- 在data中命名时 不能和methods中的方法重名。
- 注意：不应该使用`箭头函数`来定义methods函数(例如：plus: () => this.a++)；
  - 理由是箭头函数绑定了`父级作用域`的上下文，所以 this 将不会按照期望指向 Vue 实例，`this.a`将是 undefined；

```js
new Vue({
el:"#app",
data:{
name:"Hello world",
name2:"Hello world2"
},
methods:{
fn1:function(){
  // 常规写法
  console.log(this.name)
  this.fn2() // 调用方法2
},
fn2() {
  // es6 写法
  console.log(this.name2)
}
}
})
```

#### 插值表达式

- 作用:会将绑定的数据实时的显示出来：数据变化后=>所有绑定插值表达式的部分都会更新；
- 形式：通过 {{ 插值表达式 }}包裹的形式；
- 通过任何方式修改所绑定的数据，所显示的数据都会被实时替换(**响应式数据**)**数据驱动视图**；
- 插值表达式可以进行多种操作；例如：(进行js表达式、三元运算符、方法调用等)；
- 注意：Vue实例上代理了data中所有的属性和methods中的方法，而我们的el作用的视图直接可使用这些**属性和方法**；但是并不需要**写this.属性 和 this.方法()**；

```html
<!-- js表达式 -->
<p>{{ 1 + 2 + 3 }}</p>
<!-- name为data中的数据 -->
<p>{{ name + ':消息' }}</p> 
<!-- count 为data中的数据 -->
<p>{{ count === 1 ? "成立" : "不成立" }}</p>
<!-- 方法调用 -->
<!-- fn为methods中的方法 -->
<p>{{ fn() }}</p>
```

#### 计算属性

**介绍**

- 场景:当(插值表达式/v-bind表达式)过于复杂的情况下，可以采用计算属性对于任何`复杂逻辑`**都可以采用计算属性**，简单逻辑也可以采用计算属性；
- 使用: 在Vue实例选项中定义: computed:{ (key)计算属性名: `带返回值`的函数 }；
- 说明：计算属性的值 依赖 数据对象中的值  数据对象发生改变 => 计算属性发生改变=> 视图改变；
- 计算属性每计算一次都会有结果缓存，如果 data中的数据没变化，则直接从缓存中取数据；如果 data中变化了，则会执行 新的计算方法 => 缓存；
- 计算属性会每次比较`data更新`前后的值，如果前后一致则不会引起视图变化；

**methods和计算属性的区别**

- methods每次都会执行；性能计算属性比较差；
- 计算属性是有缓存机制的，更智能化，更有效率；
- 计算属性不需要调用形式的写法；而methods方法必须采用方法()调用的形式；

##### 基本使用

- 由于计算属性中要return值需要立刻返回，所以计算属性方法: `必须写同步代码`；
- 注意：**ajax/setTimeout** 不能写在计算属性中；

```js
computed: {
nameReverse() {
return this.name.split("").reverse().join("");
}} // 定义计算属性
//当数据对象中name发生变化时,计算属性也会重新计算计算=> 改变页面视图
```

#### watch（监听数据）

- 场景：当需要根据`数据变化`进行相应业务操作, 且该操作是`异步操作`时, `计算属性不能再使用`,可以使用监听watch特性。
- watch选项不需要返回值、不需要return，只需要在函数体中执行对应的逻辑即可。
- watch:  {  data属性名(监视谁写谁的名字): function(newValue(新值),oldValue(旧值)){} } ；

**计算属性和watch的区别**：

- 计算属性必须要有返回值，所以说不能写异步请求，因为有人用它的返回值(插值表达式)；
- watch选项中可以写很多逻辑，不需要返回值，因为没有人用它的返回值；

```js
watch: {
//newValue是最新的值 oldValue为后面的旧值
city(newValue, oldValue) {
this.list = this.list.map(item => ({
city: item.name,
count: newValue
}));
}
}
```

#### 钩子函数

- 生命周期是指Vue实例或者组件从诞生到消亡经历的每一个阶段，在这些阶段的前后可以设置一些函数当做事件来调用。
- 钩子函数，就是一个vue实例被生成后调用这个函数。一个vue实例被生成后还要绑定到某个html元素上，之后还要进行编译，然后再插入到document中。
- 每一个阶段都会有一个钩子函数，方便开发者在不同阶段处理不同逻辑。

![img](images/lifecycle.png)

```js
 beforeCreate (实例被创建前)
 created(实例被创建后)
 beforeMount(文档被挂载前)
 mounted(文档被挂载后)
 beforeUpdate(数据变化 页面更新前)
 updated(数据变化 页面更新后)
 beforeDestory(视图销毁前)
 destoryed(视图销毁后)
```

##### created

- created:在模板渲染成html前调用，即通常初始化某些属性值，然后再渲染成视图。
- 作用：created函数一般用于调用ajax，获取页面初始化所需的数据。

### Vue的指令

#### 指令的介绍

- 指令 (Directives) 是带有 **v-** 前缀的特殊特性。 v- 相当于标识  ng-   wx- ；

- 指令特性的值预期是**单个 JavaScript 表达式**；

- 指令的职责是，当表达式的值改变时，将其产生的连带影响，**响应式**地作用于 DOM；

- 指令位置:  **起始标签**；

  ```html
  <p v-text="'我是p标签的内容'"></p>
  ```

#### Vue系统指令

##### v-text 和 v-html（更新内容）

- 两个指令很像innerText和nnerHTML；
- **v-text:更新标签中的内容；**
- v-text与插值表达式区别：
  - v-text  更新**整个**标签中的内容；
  - 插值表达式: 更新标签中**局部**的内容；
- **v-html:更新标签中的内容/标签；**
- v-html可以渲染内容中的HTML标签(尽量避免使用，容易造成危险不太安全。)；
- v-text 和 v-html区别：v-text指令的值会替换标签内容，而v-html指令的值(包括标签字符串)会替换掉标签的内容；

```js
<div id="app">
  <p>{{str}}</p>
  <p v-text="str">我是p标签中的内容</p>
  <p v-text="strhtml">我是p标签中的内容</p>
  <p v-html="str"></p>
  <p v-html="strhtml">我是p标签中的内容</p>
</div>
<script src="./vue.js"></script>
<script>
	new Vue({
		el: '#app',
		data: {
			str: 'abc',
			strhtml: '<span>content</span>'
         }
     });
</script>
```

##### v-if 和 v-show（条件渲染）

- 场景:  需要**根据条件**决定元素是否显示及使用以上指令。
- 使用: v-if 和 v-show 后面的表达式返回的布尔值来决定该元素显示隐藏。
- **区别**：
  - v-if 是直接决定元素的添加或者删除；而 v-show 只是根据样式来决定显示隐藏。
  - v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。
  - 如果在运行时条件很少改变，则使用 v-if 较好；如果切换频繁前者开销更大； 

- 如果多个元素需要 v-if或者v-show 控制，可以用**template**标签来包裹多个元素，v-if作用在template上，最终template不会形成任何元素。

```js
<div id="app">
<!-- 如果isShow的值是true ,就显示p标签 -->
<p v-if="isShow">我是p标签中的内容</p>
<p v-show="isShow">我是p标签中的内容</p>
</div>
<script src="./vue.js"></script>
<script>
new Vue({
   el: '#app',
   data: {
       isShow: false
   }
});
</script>
```

##### v-on（绑定事件）

- 场景: 使用v-on指令给元素绑定事件；
- 使用: 绑定 v-on:事件名.修饰符(可不写)="方法名" 可使用@事件名="方法名的方式"（写括号和不写括号有区别）；
- **注意**：方法名中可以采用$event的方式传形参，也可以直接写事件名，默认第一个参数为event事件参数；
- `.once`  只触发一次回调。
- `.prevent` 调用 `event.preventDefault()`。
- 事件传参有两种形式 ：
  - 匿名传参：当只写方法名时，方法中默认第一个参数就是event(事件参数)；
  - 显示传参：当写方法名()，如果想要获取event,必须显示的用$event传到方法里；

```js
<div id="app">
<!-- v-on:xx事件名='当触发xx事件时执行的语句' -->
<!-- 执行一段js语句:可以使用data中的属性 -->
<button v-on:click="count += 1">增加 1</button>
<!-- v-on的简写方法 -->
<button @click="count += 1">增加 1</button>
<!-- 执行一个方法 -->
<button @click="add">增加 1</button>
<!-- 执行一个方法、这种写法可以传形参 -->
<button @click="fn1(count)">执行fn1方法</button>
<!-- 执行一个方法、这种写法可以传形参,特殊的形参$event -->
<button @click="fn1($event)">执行fn1方法</button>
<hr>
<!-- v-on修饰符 如 once: 只执行一次 -->
<button @click.once="fn1">只执行一次</button>

<p>上面的按钮被点击了 {{ count }} 次。</p>
</div>
<script src="./vue.js"></script>
<script>
new Vue({
  el: '#app',
  data: {
      count: 0,
      items: ['a', 'b', 'c']
  },
  methods: {
      add: function() {
          this.count += 1;
      },
      fn1: function(count) {
          console.log(count);
          console.log('fn1方法被执行');
      }
  }
});
</script>
```

##### v-for（循环数组与对象）

- 作用：列表渲染，当遇到相似的标签结构时,就用v-for去渲染；

- v-for 指令：需要使用 `item in items` 或者 `item of items` 形式的特殊语法；items 是源数据数组 /对象；

  ```js
  item in items   // item为当前遍历属性数组项的值;
  (item, key, index) in  items //item为当前遍历属性对象的值 key为当前属性名的值  index为当前索引的值
  ```

- **注意**：
  - v-for写的位置应该是重复的标签上，不是其父级元素上需要注意；(循环生成谁，就在谁的标签上写v-for)；
  - 如果 v-for 中同样有多个元素，但是不想增加额外标签，同样可以用**template**；

###### key

- 场景：列表数据变动会导致视图列表重新更新，为了提升性能方便更新需要提供一个属性key；
- 使用：通常是给列表数据中的唯一值 也可以用**索引值**；
- key通常是一个唯一值 => 身份证(循环项的身份证)；

```
<li v-for="(item,index) in list" :key="index">{{item}}---{{index}}</li>
养成好习惯:建议在写v-for时 设置:key="唯一值";
```

###### v-if和v-for（同时用）

-  v-for 的优先级大于v-if ,所有v-if才能使用v-for的变量；

```html
<p v-if="index>1" v-for="(item,index) in list"></p>
<!--以上代码执行: 会将数组中前两个元素忽略掉-->
```

```js
 <!-- 循环数组的用法 -->	
<div id="app">
 <!-- v-for作用:列表渲染,当遇到相似的标签结构时,就用v-for去渲染
 v-for="数组中的元素 in data中的数组名"-->
 <p v-for="item in list">{{item}}</p>
</div>
<script src="./vue.js"></script>
<script>
 new Vue({
     el: '#app',
     data: {
         list: ['a', 'b', 'c'],
     },
     methods: {
     }
 })
</script>

<!-- 循环对象的用法 -->
<div id="app">
<!-- (v,k,i)in 对象(数组和对象) v:值，k:键，i:对象中每对key-value的索引 从0开始（ v,k,i是参数名,）-->
<p v-for="value in per">{{value}}</p>
<hr>
<p v-for="(value,key) in per">{{value}}----{{key}}</p>
<hr>
<p v-for="(value,key,i) in per">{{value}}----{{key}}--{{i}}</p>
</div>
<script src="./vue.js"></script>
<script>
new Vue({
    el: '#app',
    data: {
        per: {
           name: '老王',
            age: 38,
            gender: '男'
        }
    }
})
```

##### v-bind（绑定标签属性）

- 作用：绑定标签上的任何属性；
- 场景：当标签上的属性是变量/动态/需要改变的；
- 语法：<p :属性="数据对象中的属性名"></p>；

```html
<p v-bind:id="ID"></p>   // ID为数据对象中的变量值;
<p :id="ID"></p>  // 简写
```

###### 绑定class对象

- 语法 :class="{ class名称": 布尔值 }"；
- 注意：绑定class和原生class会进行合并;

```html
<p :class="{left:showClass}">内容</p>
```

###### 绑定class数组语法

- 语法 :class="[class变量1,class变量2..]"；

```html
<p :class="[activeClass,selectClass]" class="default">内容</p>
```

###### 绑定style对象语法

- 语法 :style="{css属性名: 变量}"；
- css属性名需要写成驼峰格式。例如：(font-size要写成 fontSize)。
- 注意：
  - 绑定属性变量也可以直接输入属性样式，必须要加单引号。
  - 原有的style不受影响，但是后面的样式会顶替到前面的样式。因为合并时原生样式在前面。

```html
<p :style="{fontSize:fontsize}"></p>
```

###### 绑定style数组语法

- 语法  :style="[对象1,对象2...]"；
- **注意**：对象可以是多个属性的集合同样里面的css属性需要遵从小驼峰命名的规则。

```html
  <p :style="[a,b,c]" style="color:red">内容</p>
```

##### v-model（绑定表单数据）

- 作用：表单元素的绑定；
- 特点：双向数据绑定；
  - 数据发生变化可以更新到界面 =>响应式数据；
  - 通过界面可以更改数据   表单数据变化 =>通过v-model =>数据变化；

- 注意：v-model会**忽略所有表单元素的value、checked、selected特性的初始值**，而总是**将Vue实例的数据作为来源**，应该在data选项中声明初始值。

###### v-model（语法糖原理）

- 分析：表单数据改变 =>数据发生改变    数据改变 =>页面数据变化。

```html
<div id="app">
<input type="text" @input="changeInput" :value="name" />
{{ name }}
</div>
<script src="./vue.js"></script>
<script> 
var vm = new Vue({
el: "#app",
data: {
name: "张三"
},
methods: {
changeInput(event) {
  // 值发生改变时 会触发这个方法
  //  取value值
  this.name = event.target.value;
}
}
});
</script>
```

###### 绑定其他表单数据

- 表单元素：input  textarea checkbox radio  select；
- 注意：
  - checkbox在input标签中需要是指value值；
  - 所有表单元素一旦绑定v-model就会忽略掉原有的value值，checked值、selected值需要从数据对象中取默认值。

```html
任务：
1.checkbox绑定一个属性 nameCheckbox 实现 checkbox同步
2.多个checkbox绑定同一个属性 nameCheckboxs 实现 checkbox同步:北京、上海、天津
3.select绑定属性nameSelect 实现同步:北京、上海、天津 
<div id="app">
<p>{{ nameCheckbox }}</p>
<input type="checkbox" v-model="nameCheckbox" />您是否成年？
<p>{{ nameCheckboxs }}</p>
<input type="checkbox" value="bj" v-model="nameCheckboxs" />北京
<input value="tj" type="checkbox" v-model="nameCheckboxs" />天津
<input value="sh" type="checkbox" v-model="nameCheckboxs" />上海
<p>{{ nameSelect }}</p>
<select name="" id="" v-model="nameSelect">
	<option value="北京">北京</option>
	<option value="上海">上海</option>
	<option value="天津">天津</option>
</select>
</div>
<script src="./vue.js"></script>
<script>
var vm = new Vue({
	el: "#app",
	data: {
		nameCheckbox: true,
		nameCheckboxs: [],
		nameSelect: "上海"
	},
	methods: {}
});
</script>
```

##### v-cloak（解决页面闪烁）

- 场景：解决页面初次渲染时，页面模板闪屏现象。
- 注意：可以一次性将v-cloak引用在实例视图上，避免多次写入标签。

```html
<div v-cloak id="app">
<p>{{ name }}</p>
 <!--写入style样式中-->
[v-cloak] {
 display: none;
}
```

##### v-once（渲染一次）

- 作用: 使得所在元素只渲染一次。
- 场景:静态化数据 。

```html
 <p v-once>{{ name }}</p>
```

##### ref （操作 DOM）

- 作用：通过ref特性可以获取元素的dom对象；
- 使用：给元素定义ref属性，然后通过$refs.名称来获取dom对象；
- $refs是Vue实例的属性；
- $data/$event => $开头的属性和方法都是Vue实例的方法和属性；

```js
<input type="text" ref="myInput" /> // 定义ref
<!--vue实例方法：-->
focus() {
this.$refs.myInput.focus();
}  // 获取dom对象 聚焦
```

### 自定义指令

- 使用场景：需要对普通 DOM 元素进行操作，这时候就会用到自定义指令。
- 分类：`全局注册`和`局部注册`；

#### 全局自定义指令

- 在创建 Vue 实例之前定义全局自定义指令 Vue.directive()；
- Vue.directive('指令的名称'，{ inserted: (使用指令的DOM对象,表达式对象) => { 具体的DOM操作 } } )；
- 表达式对象 => value  => 表达式计算结果的值；
- 在视图中通过"v-自定义指令名"去使用指令；
- 注意：指令名称要全部小写；

```js
 // 定义指令
//  自定义指令是不需要加v-前缀的
// 第二个参数为一个对象  对象中要实现 inserted的方法
// inserted中的参数为当前指令所在元素的dom对象
Vue.directive("focus", {
        inserted(dom,expression) {
          dom.focus();
        }
 });
```

#### 局部自定义指令

- 需要注册在当前实例上directives:{}；

```js
directives: {
focus: {
inserted(dom,expression) {
dom.focus();
}
}
} // 局部自定义指令实现
```

### 过滤器

#### 过滤器的文档分析

- 场景：data中的数据格式(日期格式/货币格式/大小写等)需要数据时；
- 使用位置：{{}}和v-bind="表达式 | 过滤器名称"；
- 具体用法：{{msg | 过滤器名字}}；
- 分类：本地(局部)和全局；所有实例均可使用 Vue局部 过滤器只有当前实例才可以使用；
- 全局与局部区别：注册位置不同,应用范围不同；
- 局部过滤器：
  - 本地：通过el/data/methods`选项filters`；
  - 局部：在Vue实例上的选项上filters => 所有过滤器集合 =>当前实例使用。

- 全局过滤器：
  - 全局: 在new Vue上面 Vue.filter()  => 所有实例都可以使用。

#### 全局过滤器

- 过程：
  1. 在创建Vue实例之前定义全局过滤器Vue.filter()；
  2. Vue.filter('该过滤器的名字'，(要过滤的数据)=>{return 对数据的处理结果})；
  3. 在视图中通过{{数据 | 过滤器的名字}} 或者v-bind使用过滤器；

- 注意：
  - 可使用多种表达式形式全局过滤器多个Vue实例可共享使用；
  - 过滤的数据必须return输出；

```js
Vue.filter("toUpper", function(value) {
return value.charAt(0).toUpperCase() + value.substr(1);
});// 过滤器核心代码
```

#### 局部过滤器

- 过程：
  1. 在vue实例对象的选项中配置过滤器filters:{}；
  2. (key)过滤器的名字：(value)(要过滤的数据)=>{return 过滤的结果}；
  3. 在视图中使用过滤器：{{被过滤的数据 | 过滤器的名字}}；

- 注意：局部过滤器只能用在当前Vue实例视图上；过滤的数据必须return输出；

```js
filters: {
toUpper(value) {
  return value.charAt(0).toUpperCase() + value.substr(1);
}}
```

##### 过滤器传参和串联使用

- 传参：过滤器可以传递参数,**第一个参数永远是前面传递过来的过滤值**；
- 过滤器也可以多个串行起来并排使用；
- 调试：debugger => 会在调试时 自动进入 该断点  => 调试完毕之后 debugger要删除；

```js
// index为传入的参数 
toUpper(value, index) {
   return value
     .split("")
     .map(function(item, i) {
       if (i === index) {
         return item.toUpperCase();
       }
       return item;
     })
     .join("");
 }
} // 根据传入的索引找到对应的字母换成大写字母
```

- 串行使用过滤器

```html
<p>{{ text | toUpper(2) | reverse }}</p> // 语法 多个过滤器用 | 分割
```

### Vue实现发送网络请求

**发送网络请求**

- 在Vue.js中发送网络请求本质还是ajax，我们可以使用插件方便操作。
- axios：**不是vue的插件**，可以在任何地方使用，推荐使用。
- 既可以在浏览器端又可以在node.js中使用的发送http请求的库，`支持Promise`，不支持jsonp；如果遇到jsonp请求，可以使用插件jsonp实现。

#### axios使用

**使用过程**：

- 引入方式：本地引入，npm；

```js
//第一种写法:
axios.get(url).then((res) => {
// 请求成功会来到这res响应体
}).catch((err) => {
// 请求失败会来到这处理err对象
})	
//第二种写法:
axios({
    method:"" ,	//默认为get请求
    url:"",
    data:""
}).then(reslut =>{})	//请求成功会来res响应体
```

#### json-server工具的使用

- 目的：没有后端的支撑下，前端难以为继，json-server可以快速构建一个后台的接口服务，供前端调用；
- json-server是一个命令行工具可以json文件变成接口文件；
- json-server遵循`restful`接口规则；
- 安装：npm i -g  json-server // 也可以采用yarn 和 cnpm；

```js
新建一个json文件 db.json,并在相对目录下运行命令行命令
{
// brands 相等于 我们数据库中的一个表
"brands": [
{
"name": "苹果",
"date": "2018-05-30T08:07:20.089Z",
"id": 1
}
],
}
json-server --watch db.json	//用来访问接口；
```

##### RESTFUL的接口规则

| **HTTP方法** | **数据处理** | **说明**                                           |
| ------------ | ------------ | -------------------------------------------------- |
| POST         | Create       | 新增一个没有id的资源                               |
| GET          | Read         | 取得一个资源                                       |
| PUT          | Update       | 更新一个资源。或新增一个含 id 资源(如果 id 不存在) |
| DELETE       | Delete       | 删除一个资源                                       |