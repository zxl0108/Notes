# Vue的学习

## Vue基础

### Vue的认识

- Vue是一个优秀的**前端框架**，开发者按照Vue的规范进行开发。

### Vue的特点

- 数据驱动**视图**可以让我们只关注数据，完全解耦：数据和视图  =>响应式数据 => 数据变化 =>视图一定变化。
- **MVVM** 双向绑定  => v-model => 数据变化 => 视图变化   视图变化 => 数据变化 ；
- 当下各种新框架都采用了**类Vue**或者**类React**的语法去作 为主语法, 微信小程序/MpVue/uni-app ；
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

#### 1.el（管理视图）

- **作用**：当前Vue实例所管理的html视图；
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

2.data（数据）

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

#### 3.methods（方法的集合）

- methods是一个**对象**；可以直接通过 Vue 实例对象访问这些方法，或者在**插值表达式中使用**。
- 方法中的 `this` 自动绑定为 Vue 实例。同样所有的方法也被代理到了Vue实例对象上，都可通过this访问。
- 在data中命名时 不能和methods中的方法重名。
- 注意：不应该使用`箭头函数`来定义methods函数(例如 `plus: () => this.a++`)；
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

#### 4.插值表达式

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
- v-text 和 v-html区别：v-text指令的值会替换标签内容，而v-html指令的值的值(包括标签字符串)会替换掉标签的内容；

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

- 场景:  使用v-on指令给元素绑定事件；
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

- v-for作用:列表渲染，当遇到相似的标签结构时,就用v-for去渲染；

- v-for 指令需要使用 `item in items` 或者 `item of items` 形式的特殊语法；items 是源数据数组 /对象；

  ```js
  item in items   // item为当前遍历属性数组项的值;
  (item, key, index) in  items //item为当前遍历属性对象的值 key为当前属性名的值  index为当前索引的值
  ```

- **注意**：
  - v-for写的位置应该是重复的标签上，不是其父级元素上需要注意；(循环生成谁，就在谁的标签上写v-for)；
  - 如果 v-for 中同样有多个元素，但是不想增加额外标签，同样可以用**template**；

###### key

- 场景:列表数据变动会导致视图列表重新更新，为了提升性能方便更新需要提供一个属性key；
- 使用: 通常是给列表数据中的唯一值 也可以用**索引值**；
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

