# jQuery

## jQuery初步

- JQuery是一个快速、简洁的JavaScript库；学习jQuery本质： 就是学习调用这些函数（方法）。

**优点：链式编程、隐式迭代**

- 链式编程：指可以在元素属性后面继续写当前元素的属性；
- 遍历内部 DOM 元素（伪数组形式存储）的过程就叫做隐式迭代；

### jQuery的入口函数

```js
//第一种方法
$(function () {   
​    ...  // 此处是页面 DOM 加载完成的入口;
 }) ;   
//第二种方法
$(document).ready(function(){
   ...  //  此处是页面DOM加载完成的入口;
});       
```

### jQuery的基本使用

#### jQuery的顶级对象$

- $ 是 jQuery 的别称，在代码中可以使用 jQuery 代替 $，为了方便，通常都直接使用 $ 。
- .$ 是jQuery 的顶级对象， 相当于原生JavaScript中的 window。

#### 与Dom对象相互转换

- DOM 对象转换为 jQuery 对象： $(DOM对象)；
- jQuery 对象转换为 DOM 对象）；$('div') [index]       index 是索引号 ；

## jQuery事件

### 事件注册

- 语法：element.事件(function(){})；
- **事件名称:mouseover、mouseout、blur、focus、change、keydown、keyup、resize、scroll** 等；
- 区别：其他事件和原生基本一致。

```
$(“div”).click(function(){  事件处理程序 }) 
```

### on()--绑定事件

- on() 方法在匹配元素上绑定一个或多个事件的事件处理函数；

- 语法：element.on(events,[selector],fn)
- **如果有的事件只想触发一次， 可以使用 one()来绑定事件。**

```
1. events:一个或多个用空格分隔的事件类型，如"click"或"keydown" 。
2. selector: 元素的子元素选择器 。
3. fn:回调函数 即绑定在元素身上的侦听函数。
```

**on() 方法优势1：**

- 可以**绑定多个事件**，多个处理事件处理程序。 

```js
同处理程序： $('div').on('mouseenter click',function () {
			console.log(123);
		});
不同处理程序： $(“div”).on({
  mouseover: function(){}, 
  mouseout: function(){},
  click: function(){}  
});    
```

**on() 方法优势2：**

- 可以**事件委派操作**。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。
- 在此之前有bind(), live()，方法来处理事件绑定或者事件委派，最新版本的请用on替代他们；

```js
$('ul').on('click', 'li', function() {
   alert('hello world!');
}); 
```

**on() 方法优势3：**

- 动态创建的元素，click()没有办法绑定事件，on() 可以给**动态生成的元素绑定事件**；

```js
 $(“div").on("click",”p”, function(){
     alert("俺可以给动态生成的元素绑定事件")
 });
```

### off()--解绑事件

- **作用：off() 方法可以移除通过 on() 方法添加的事件处理程序。**

```js
$("p").off() 		            // 解绑p元素所有事件处理程序;
$("p").off( "click")           // 解绑p元素上面的点击事件 后面的 foo 是侦听函数名;
$("ul").off("click", "li");   // 解绑事件委托;
```

### trigger()--自动触发事件

- 作用：有些事件需要自动触发, 比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发；

- 语法：element.click()  // 第一种简写形式；
- 语法：element.trigger("type")//第二种自动触发模式；

### 事件对象

- 事件被触发，就会有事件对象的产生；

```js
element.on(events,[selector],function(event){})   
【event==》 事件对象】；
```

#### 阻止默认行为

- **阻止默认行为：event.preventDefault() **
- **在标签地址中添加  'Javascript:'；例如：<a href="Javascript:;">**
- **直接输入return  false（输入return后，后面的程序不在执行）**

#### 阻止冒泡

- **阻止冒泡： event.stopPropagation() **

## jQuery获取或设置元素

### 1.获取元素对象的方法

#### 1.jQuery选择器

- $('#id')：指定id元素；
- $('*')：所有元素；
- $('.class')：指定class元素；
- $('div')：根据标签获取元素；
- $('div,p,li')：获取多个；
- $('li.class')：交集获取；
- $('ul>li')：子代；
- $('ul li')：后代；

#### 2.jQuery筛选选择器

- $('li:first')：第一个元素；
- $('li:last')：最后一个元素；
- $('li:eq(2)')：索引为2【查找指定索引的元素，不如筛选方法常用）；
- $('li:odd')：索引为奇数；
- $('li:even')：索引为偶数；

#### 3.jQuery筛选方法

- **$('li').parent()		父级**
- **$('li').parents() **      祖先
- **$('ul').children('li')**		子集【儿子级】【如果不加参数，获取所有的，如果添加指定的元素，按照指定的找】；
- **$('ul').find('li')**		后代【后代级】
- **$('li').siblings('li')**		兄弟
- $('li'),nextAll()		后面所有
- $('li').prevAll()		前面所有
- 判断是否具有某个类名：$('div').hasClass('aaa')
- **$('div').eq(index)**		指定索引方法【eq推荐用方法】；

#### jQuery里面的排他思想

- **目的：想要多选一的效果，排他思想：当前元素设置样式，其余的兄弟元素清除样式。**

案例1：多个按钮点击改变当前按钮颜色其他的不变；

```js
$(this).css(“color”,”red”);//设置当前元素下颜色；
$(this).siblings(). css(“color”,””); //当前元素的其他兄弟元素清除样式；
```

案例2：淘宝服饰精品案例（通过index()获取索引值）；

```js
①核心原理：鼠标经过左侧盒子某个小li，就让内容区盒子相对应图片显示，其余的图片隐藏；
②需要得到当前小li 的索引号，就可以显示对应索引号的图片；
③jQuery 得到当前元素索引号 $(this).index()  ；
④中间对应的图片，可以通过  eq(index) 方法去选择 ；
⑤显示元素 show()   隐藏元素 hide()；
```

#### 修改css样式

##### 1.操作CSS方法

- 语法$(元素对象 ).css(''属性'',"属性值")；

```js
参数只写属性名，则是返回属性值$(this).css(''color'');

参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号$(this).css(''color'', ''red'');

参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号，
$(this).css({ "color":"white","font-size":"20px"});
```

##### 2.设置类样式方法

- 作用等同于以前的 classList，可以操作类样式，注意操作类里面的参数不要加点；
- 原生 JS 中 className 会覆盖元素原先里面的类名。
- jQuery 里面类操作只是对指定类进行操作，不影响原先的类名。

###### 语法

1.添加类：$(“div”).addClass(''类名'');

2.移除类：$(“div”).removeClass(''类名'');

3.切换类：$(“div”).toggleClass(''类名'');

```
案例：tab栏切换；
点击上部的li，当前li 添加current类，其余兄弟移除类；
点击的同时，得到当前li 的索引号；
让下部里面相应索引号的item显示，其余的item隐藏；
```

### 2.设置或获取元素性值(prop or attr)

#### 获取或设置元素固有属性值 prop()

```
所谓元素固有属性就是元素本身自带的属性，比如 <a>元素里面的 href ，比如 <input>元素里面的 type。
```

- **获取属性语法：prop(''属性''；**
- **设置属性语法：prop(''属性'', ''属性值'')**
- **change事件，表单中checked属性**

#### 获取或设置元素自定义属性值attr()

```
用户自己给元素添加的属性，我们称为自定义属性。比如给 div 添加 index=“1”。 
```

- **获取属性语法：attr(''属性'')**       		  //类似原生 getAttribute()；

- **设置属性语法attr(''属性'', ''属性值'')**   //类似原生 setAttribute()；

#### 数据缓存data()【了解】

```
data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构，所以元素上无法查看。一旦页面刷新，之前存放的数据都将被移除。
```

- 附加数据语法：data(''name'',''value'')   // 向被选元素附加数据；

- 获取数据语法：data(''name'')             //   向被选元素获取数据；

### 3.获取或设置元素内容

#### 1.html()--获取或设置普通元素内容

- 获取：html()                   // 获取元素的内容；
- 设置：html(''内容'')        // 设置元素的内容；
- 相当于原生inner HTML；

#### 2.text()--获取或设置普通元素文本内容

- 获取：text()   					// 获取元素的文本内容；
- 设置：text(''文本内容'')    // 设置元素的文本内容；
- 相当于原生innerText；

#### 3.val()--获取或设置表单的值

- 获取：val()   				// 获取表单的值；
- 设置：val(''内容'')        // 设置表单的值；
- 相当于原生value；

### 4.获取与设置元素尺寸、位置

#### jQuery 尺寸

1. 语法：width()、height()	【只算width和height】
2. 语法：innerWidth()、innerHeight()	【包含padding+width】
3. 语法：outerWidth()、outerHeight()	【包含padding、border、width】
4. 语法：outerWidth(true)、outerHeight(true)	【包含padding、border、margin、width】

##### 注意：

- 以上参数为空，则是获取相应值，返回的是数字型。
- 如果参数为数字，则是修改相应值。
- 参数可以不必写单位。

#### jQuery 位置

##### 1.offset()（设置或获取元素偏移）

​	用法：offset：距离文档的距离【left，top】

1. offset() 方法设置或返回被选元素相对于**文档**的偏移坐标，跟父级没有关系。
2. 该方法有2个属性；offset().top  用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离;
3. 可以设置元素的偏移：offset({ top: 10, left: 30 })；

##### 2.position()（获取元素偏移）

1. position() 方法用于返回被选元素相对于**带有定位的父级**偏移坐标，如果父级都没有定位，则以文档为准。
2. 该方法有2个属性;position().top 用于获取距离定位父级顶部的距离，position().left 用于获取距离定位父级左侧的距离。**该方法只能获取！**

##### 3.scrollTop/Left()（设置或获取元素被卷去的头部、左侧）

1. scrollTop() 方法设置或返回被选元素被**卷去的头部**。
2. **不跟参数是获取**，参数为不带单位的数字则是设置被卷去的头部。

### 设置元素效果

#### 1.hover([over,]out)	事件切换

- over：鼠标移到元素上要触发的函数（相当于mouseenter==mouseover）；
- out：  鼠标移出元素要触发的函数（相当于mouseleave==mouseout）；
- 如果只写一个函数，则鼠标经过和离开都会触发它；

#### 2.stop()	动画队列及其停止排队方法

- **动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。**
- stop() 方法用于停止动画或效果。
- 注意：stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画。

#### 3.show/hide	显示隐藏效果

- **语法：show(显示)/hide(隐藏)/toggle(切换)([speed,[easing],[fn]])；**

#### 4.slideDown/Up	滑动效果

- **slideDown(向下)/slideUp(向上 )/slideToggle(切换)([speed,[easing],[fn]])；**

#### 5.fadeIn/Out	淡入淡出效果

- **语法：fadeIn(淡入)/fadeOut(淡出)//fadeToggle(切换)([speed,[easing],[fn]]);**
- **fadeTo([[speed],opacity,[easing],[fn]])；将选元素的不透明度度逐渐改变为指定的值；**
- **注意fadeTo必须写两个参数，speed和opacity(透明度取值范围 0~1)**；

#### 6.animate	自定义动画

- **语法：animate(params,[speed],[easing],[fn])**
- 注意：params: 想要更改的样式属性，以对象形式传递，必须写。 属性名可以不用带引号， 如果是复合属性则需要采取驼峰命名法 borderLeft。其余参数都可以省略。

#### 注意

- speed，easing，fn三种参数都可以省略。
- speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值。
- easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear(匀速)”。
- fn: 回调函数，在动画完成时执行的函数，每个元素执行一次。

## jQuery元素操作

- 主要是遍历、创建、添加、删除元素操作。

### 遍历元素

#### each()方法

- **语法：$("元素对象").each(function(index, domEle) { xxx; }）;**

#####   特点

- 1.each() 方法遍历匹配的每一个元素。主要用DOM处理。:each 每一个；

- 2.所以要想使用jquery方法，需要给这个dom元素转换为jquery对象  $(domEle)；
- 3.里面的回调函数有2个参数：index 是每个元素的索引号;  demEle 是每个DOM元素对象，不是jquery对象

#### $.each()方法

- **语法：$.each(遍历对象，function(index, element){ xxx;}）**

#####   特点

- 1.$.each()方法可用于遍历任何对象。主要用于数据处理。比如数组，对象；
- 2. 里面的函数有2个参数：  index 是每个元素的索引号;  element  遍历内容

### 创建元素

- 语法：$(''<li></li>'');    

### 添加元素（内部添加--父子关系）

####  append()（从后添加）

- **语法：element.append(''内容'')** 	把内容放入匹配元素内部最后面，类似原生 appendChild。

####  prepend()（从前添加）

- **语法：element.prepend(''内容'')** 	把内容放入匹配元素内部最前面。

### 外部添加（外部添加--兄弟关系）

####  after（放入后面）

- **语法：element.after(''内容'') **		把内容放入目标元素后面。

####  before（放入前面）

- **语法：element.before(''内容'')**	   把内容放入目标元素前面。

### 删除元素

#### remove()（删除本身）

- **语法：element.remove()**		删除匹配的元素（本身）。

#### empty() （删除子节点）

- **语法：element.empty()** 		删除匹配的元素集合中所有的子节点。

#### html('''')（清空内容）

- **语法：element.html('''')**		清空匹配的元素内容。
- 注意：empt() 和  html('''') 作用等价，都可以删除元素里面的内容，只不过 html 还可以设置内容。