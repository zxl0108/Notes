## 显示模式

- 标签显示模式的转换:display；

### 块级元素

#### 介绍

- 每个块元素通常都会独自占据整行或多整行,可以设置宽高，对齐等属性,常用于网页布局和网页结构的搭建。

- ```j
  常见的块元素<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>；
  ```

#### 特点

1. 总是从新行开始；
2. 高度，行高、外边距以及内边距都可以控制；
3. 宽度默认是容器的100%；
4. 可以容纳内联元素和其他块元素；
5. 是一个容器及盒子，里面可以放行内或者块级元素；

### 行内元素

#### 介绍

- 行内元素（内联元素）不占有独立的区域，仅仅靠自身的字体大小和图像尺寸来支撑结构，一般不可以设置宽度、高度、对齐等属性，常用于控制页面中文本的样式。

- ```css
  常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中<span>标签最典型的行内元素。
  ```

#### 特点

1. 和相邻行内元素在一行上。
2. 高、宽无效，但水平方向的padding和margin可以设置，垂直方向的无效。
3. 默认宽度就是它本身内容的宽度。
4. 行内元素只能容纳文本或则其他行内元素。

### 行内块元素

#### 介绍

- 行内块元素可以对它们设置宽高和对齐属性。

- ```css
  行内块元素中的标签<img />、<input />、<td>；
  ```

#### 特点

1. 和相邻行内元素（行内块）在一行上,但是之间会有空白缝隙。
2. 默认宽度就是它本身内容的宽度。
3. 高度，行高、外边距以及内边距都可以控制。

![1565397603207](D:/Document/GitHub/Notes/images/1565397603207.png)

## 盒子模型

### border（盒子边框）

- border : border-width (宽度)|| border-style (样式)|| border-color(颜色)；
- border-style：
  - double：边框为双实线；
  - dotted：边框为点线；
  - dashed：边框为虚线 ；
  - none：没有边框即忽略所有边框的宽度（默认值）；
  - **solid：边框为单实线(最为常用的)；**

#### 圆角边框

- 语法格式：border-radius: 50%;   让一个正方形变成圆圈。

### padding（内边距 ）

- padding属性用于设置内边距。指边框与内容区域之间的距离。
- 如果没有给一个块元素指定宽度， 此时，如果给这个块元素指定左右padding， 则不会撑宽盒子。

### margin（外边距）

- margin属性用于设置外边距。margin就是控制盒子和盒子之间的距离；
- 可以让一个块元素实现水平居中，需要满足一下两个条件：
  - 必须是块级元素；盒子必须指定了宽度（width）；
  - 然后给左右的外边距都设置为auto，就可使块级元素水平居中；

### 盒子阴影

![1565357211702](D:/Document/GitHub/Notes/images/1565357211702.png)

- box-shadow：水平阴影 垂直阴影 模糊距离（虚实）阴影尺寸（影子大小）阴影颜色  内/外阴影；

## CSS布局

- CSS布局三种机制:普通流、浮动和定位；

### Float（浮动及清除浮动）

#### 浮动

##### 浮动作用

- 浮动最早是用来控制图片，实现文字环绕图片的效果。
- 让多个盒子(div)水平排列成一行，使得浮动成为布局的重要手段。
- 浮动语法:float:left/right。

##### 浮动特点:

- 浮：加了浮动的盒子是浮起来的，漂浮在其他标准流盒子的上面。 
- 漏：加了浮动的盒子是不占位置的，它原来的位置漏给了标准流的盒子。
- 特：注意1. 浮动的盒子需要和标准流的父级搭配使用；2. 浮动可以使元素具有行内块特性。

#### 清除浮动

##### 1.额外标签法

- 通过在浮动元素末尾添加一个空的标签例如 <div style="clear:both"></div>，或则其他标签等亦可;

##### 2.父级添加overflow属性方法

- 可以给父级添加： overflow为 hidden| auto| scroll  都可以实现。
- 缺点：内容增多时候容易造成不会自动换行导致内容被隐藏掉，无法显示需要溢出的元素。

##### 3.使用after伪元素清除浮动法

```html
clearfix:before/after {
	content: ""; display: block; height: 0; clear: both; visibility: hidden;  
	} 
clearfix {*zoom: 1;}
```

### position（定位）

#### 作用

- 概念：定位 = 定位模式 + 边偏移，将盒子定在某一个位置。
- 左右箭头压在图片上，方便用户交互；hot、new 压在盒子上方,吸引用户的眼球。

#### 边偏移border

- 在 CSS 中，通过 top、botto,left和right属性定义元素的边偏移；
- 相对定位是元素相对于它在标准流中的位置 + 边偏移属性来设置元素的位置。（自恋型）；

#### 1 静态定位(static)不脱标

- 静态定位是元素的默认定位方式，也就是说网页中所有元素默认都是静态定位的 —— 按照标准流特性摆放位置。在不需要定位元素时，元素的定位属性就是 static 的。

#### 2 相对定位(relative)不脱标

- 以自己在标准流位置的左上角为基点 + 边偏移属性定位元素新的位置；

2. 原来在标准流的区域继续占有，后面的盒子仍然以标准流的方式对待它；

#### 3 绝对定位(absolute)完全脱标

- 完全脱标 —— 完全不占位置。
- 父元素要有定位 —— 父元素在标准流中的位置 + 边偏移属性来设置元素的位置。
  - 如果当前父元素没有定位（相对、绝对或固定有定位的父元素)；
  - 如果所有父元素都没有定位，则以浏览器为准定）；如果父亲有定位，则以父亲为准；

#### 4 子绝父相

- 父元素相对定位不脱标,在标准流占据位置,子元素绝对定位,可以移动到父元素的任意位置；
- 父元素占位置,下边盒子不能上来,布局正常；

#### 5 固定定位(fixed)完全脱标

- 完全脱标1.完全不占位置；
- 只认浏览器的可视窗口 浏览器可视窗口 + 边偏移属性来设置元素的位置；
  - 跟父元素没有任何关系；2.不随滚动条滚动。

## 三大特性

### CSS层叠性

- 所谓层叠性是指多种CSS样式的叠加,是浏览器处理冲突的一个能力,如果一个属性通过两个相同选择器设置到同一个元素上，那么这个时候一个属性就会将另一个属性层叠掉。

### CSS继承性

- 所谓继承性是指书写CSS样式表时，子标签会继承父标签的某些样式，如文本颜色和字号想要设置一个可继承的属性，只需将它应用于父元素即可。
- 注意:a标签不能继承父元素的文字颜色；标题标签不会继承父元素的文字大小。

### CSS优先级

![1565356702422](D:/Document/GitHub/Notes/images/1565356702422.png)

- 总结：权重是优先级的算法，层叠是优先级的表现；

## 常见选择器

- 标签选择器（元素选择器）：标签名{属性1:属性值1; 属性2:属性值2; }；
- 类选择器：Class  {   属性1:属性值1; 属性2:属性值2; }；
- 多类名选择器：我们可以给标签指定多个类名，<div class=“多个类名">；
- ID选择器：#id名 {属性1:属性值1; 属性2:属性值2;}；
- 通配符选择器："*" 它是所有选择器中作用范围最广的，能匹配页面中所有的元素;

### 复合选择器

#### 后代选择器

- 后代选择器又称为包含选择器，用来选择元素或元素组的后代，其写法就是把外层标签写在前面，内层标签写在后面，中间用空格分隔。当标签发生嵌套时，内层标签就成为外层标签的后代。
- 后代选择器：用来选择元素或元素组的后代是选择所有的子孙后代；较多，div p { color：red;}； 

#### 子元素选择器

- 子元素选择器只能选择作为某元素子元素的元素。其写法就是把父级标签写在前面，子级标签写在后面，中间跟一个 >; 进行连接，符号左右两侧各保留一个空格；
- 子代选择器：选择作为某元素子元素的元素,只选亲儿子；较少   .nav>p { color: red; } ；

#### 交集选择器

- 交集选择器 是 并且的意思。  即...又...的意思   比如p.one 选择的是： 类名为 .one的段落标签。(用的相对较少,不建议)；
- 交集选择器：选择两个标签交集的部分；较少 a:link {color: red;}   

#### 并集选择器

- 并集选择器和的意思，就是说，只要逗号隔开的，所有选择器都会执行后面样式。比如  .one, p {color: #F00;}表示 .one 和 p，这两个选择器都会执行颜色为红色。  (通常用于集体声明)；
- 并集选择器：选择某些相同样式的选择器,可以用于集体声明；较多  .nav, .header {color: red;} ；

### 伪类选择器

1. :active  选定的链接 ；:link  未访问的链接；:visited  已访问的链接；:hover  鼠标移动到链接上 ；

### 特殊选择器

#### 结构伪类选择器

##### 1.E:first-child

- 选择父元素的第一个子元素E。

##### 2.E:last-child

- 选择父元素的最后一个子元素E。

##### 3.E:nth-child(n)

- 匹配父元素的第n个子元素E，假设该子元素不是E，则选择器无效。

##### 4.E:nth-last-child(n)

- 匹配父元素的倒数第n个子元素E，假设该子元素不是E，则选择器无效。

##### 5.E:nth-of-type(n)

- 匹配同类型中的第n个同级兄弟元素E。

#### 占位符选择器

- E::placeholder ；修改占位符样式。

#### 属性选择器

- 通过属性来选择标签 [href="abc.html"]；

  

# Web移动开发

## CSS扩展语言LESS

### 简介:

1. Less（Leaner Style Sheets 的缩写）是一门 CSS 扩展语言，它扩展了CSS的动态特性。 CSS 预处理器；
2. 常见的CSS预处理器：Sass、Less、Stylus；
3. 预处理器是程序中处理输入数据，产生能用来输入到其他程序的数据的程序；

### 变量:

- 简介:
  - 变量是指没有固定的值，可以改变的。
  - 我们CSS中的一些颜色和数值等经常使用，可以设置为变量；			
- 变量名:值;@bg:#333;	引用:.box_1 { background-color: @bg;}

### 运算:

- 1.Less提供了加（+）、减（-）、乘（*）、除（/）算术运算。2.任何数字、颜色或者变量都可以参与运算。注意：运算符中间左右有个空格隔开； 
- 2.取值:  1.如果两个值之间只有一个值有单位，则运算结果就取该单位。2.对于两个不同的单位的值之间的运算，运算结果的值取第一个值的单位； 

## 移动开发

### 理想视口

- 我们移动端布局想要的是理想视口就是手机屏幕有多宽，我们的布局视口就有多宽；
- 想要理想视口，我们需要给我们移动端页面添加meta视口标签；
- 配置方式:<meta name="viewport" content="width=device-width, user-scalable=no,initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">

### 二倍图

- 在标准的viewport设置中，使用倍图来提高图片质量，解决在高清设备中的模糊问题；

### 背景缩放

- 语法：background-size: 背景图片宽度 背景图片高度；
- 单位：像素|百分比|cover|contain；
  - cover把背景图像扩展至足够大，以使背景图像完全覆盖背景区域；
  - contain把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域；
  - 百分比，参照背景图所在的盒子大小；

### CSS3盒子模型

- 传统模式宽度计算：盒子的宽度=CSS中设置的width+border+padding ；
- CSS3盒子模型：盒子的宽度=CSS中设置的宽度width里面包含了border和padding；
- 也就是说，我们的CSS3中的盒子模型， padding和border不会撑大盒子了；

### 总结

- 现在市场常见的移动端开发有单独制作移动端页面和响应式页面两种方案；
- 现在市场主流的选择还是单独制作移动端页面；

## 流式布局

#### 介绍

1. 流式布局，就是百分比布局，也称非固定像素布局。(常见页面京东)；
2. 通过盒子的宽度设置成百分比来根据屏幕的宽度来进行伸缩，不受固定像素的限制，内容向两侧填充；
3. 流式布局方式是移动web开发使用的比较常见的布局方式；
4. max-width  最大宽度（max-height  最大高度）；
5. min-width  最小宽度（min-height  最小高度）；

#### 二倍图精灵图使用方式

1. 在firework里面把精灵图等比例缩放为原来的一半；
2. 之后根据大小 测量坐标；
3. 注意代码里面background-size也要写： 精灵图原来宽度的一半；

#### 新增图片格式

- 1.DPG图片压缩技术(京东自主研发图片压缩技术)；
- 2.webq图片格式(谷歌研发加快图片加载速度图片格式)；

## Flex布局

### flex布局原理

1. flex 是 flexible Box的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为 flex 布局。
2. 当我们为父盒子设为 flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。
3. 总结：就是通过给父盒子添加flex属性，来控制子盒子的位置和排列方式。

### flex布局父项常见属性

#### flex-direction：设置主轴的方向

1. row 默认值从左到右 	row-reverse从右到左；
2. column默认值从上到下	column-reverse从下到上；

#### justify-content：设置主轴上的子元素排列方式 

1. flex-start 默认值从头部开始,如果主轴是X轴,则从左到右	flex-end 从尾部开始排列；
2. center 在主轴居中对齐(如果主轴是 X轴则水平居中)；
3. space-around 平分剩余空间；
4. space-between 先两边贴边,再平分剩余空间(重要)；

#### flex-wrap：设置子元素是否换行

1. nowrap 默认值不换行；wrap 换行；

#### align-content：设置侧轴上的子元素的排列方式(多行)

1. flex-start：默认值在侧轴的头部开始排列；
2. flex-end：在侧轴的尾部开始排列；
3. center：在侧轴的中间显示；
4. space-around：子项在侧轴平分剩余空间；
5. space-between：子项在侧轴先分布在两头,再平分剩余空间；
6. stretch：设置子项元素高度平分父元素高度；

#### align-items：设置侧轴上的子元素排列方式(单行)

1. flex-start：从上到下(默认值)；
2. flex-end：从下到上；
3. center：挤在一起居中(垂直居中)；
4. stretch：拉伸；

#### flex-flow：复合属性

1. 相当于同时设置了 flex-direction 和 flex-wrap；
2. 用法flex-flow:row/column	wrap/nowrap;

### flex布局子项常见属性

#### 子项属性介绍

1. flex 子项目占的份数；
2. align-self 控制子项自己在侧轴的排列方式；
3. order属性定义子项的排列顺序(前后顺序)；

#### flex属性

1. flex属性定义子项目分配容器的剩余空间,用flex来表示占多少份数；
2. 类名 {flex: <number> | 百分百; /* default 0 */}；

#### align-self： 控制子项自己在侧轴上的排列方式

1. align-self 属性允许单个项目有与其他项目不一样的对齐方式,可覆盖 align-items 属性。默认值为 auto，表示继承父元素的 align-items 属性,如果没有父元素,则等同于 stretch。
2. 类名 {/* 设置自己在侧轴上的排列方式 */  align-self: flex-end; }

#### order ：定义项目的排列顺序

1. 类名 {order: <number>;}；
2. 数值越小，排列越靠前，默认为0；

#### flex布局：最为重要的三个属性

1. 确认主轴: flex-direction;
2. 侧轴对齐: align-items:center;
3. 划分份数：flex:1;

## Rem布局

#### 介绍

- rem布局，最为直观的效果，页面全部元素现实等比缩放，包括文字，盒子大小。

#### 媒体查询

- 简介: 是一个查询屏幕的过程，通过查询当前屏幕尺寸属于哪个范围，从而有哪个范围的样式生效；
- @media mediatype(screen手机/all所有设备/print打印机) and(且)/not(非)/only (仅)(media feature)    {  CSS-Code;{	}				}

#### rem初体验

- rem布局的核心：rem+媒体查询；
- 优点:
  - 等比计算：计算出来的rem前面的那个比例，这个比例在各个档位下，一直不变，变的是rem背后的那个值;
  - 唯一控制；只要用rem作为单位，当 HTML字体大小发生改变，使用rem单位元素都会发生改变;
  - 档位划分：媒体查询，里面设置要变化的内容 ;
  - 里面设置：语法上设置HTML字体大小其实设置rem单位背后的值 ;

#### rem布局操作步骤

第一步：

- 原稿实现：先拿到设计稿（只有一份）：750px；页面上所有的元素，在750px设计稿上进行测量，代码实现；（流式、flex）所有的属性都写死，写成固定的px值；

第二步：用rem替换px

- 准备各个档位下的rem：提前准备好各个档位下的HTML 的font-size大小；
- 拿到当前设计稿屏幕尺寸对应的rem背后的值；
- 达到目标：那么，屏变化时，1rem也会变化，自然就是等比缩放；我们需要手动设置这两个范围媒体查询:
  - CSS文件:没有行内权重高,需要它提高权重!!!
- 因为我现在是750px的设计稿，可以得到750px这个尺寸属于的档位下的HTML的font-size大小；也就是750px设计稿下的1rem值背后的代表的值是多少；
- 计算比例：把页面刚才所有的元素的PX值替换为 rem 比例值；（82px  82rem/75= 1.785rem ）;

## 响应式布局

#### 介绍

- 响应式布局通过同一份代码快速、有效适配手机、平板、PC设备；

#### 档位划分

- w<768 超小屏幕（手机，学习rem布局里面的档位划分都是在这个范围）；
- 768<= w <992  小屏设备（平板）；
- 992<= w <1200  中等屏幕（桌面显示器）；
- 1200<=w 大宽屏设备（大桌面显示器）；

#### 版心

- 所有的子元素都是归于版心控制，那么不同版心，就意味着子元素要以不同的布局达到合理的要求；
- 除超小屏以外：版心的宽度设置都是小于当前档位最小界值，比如 min-width: 768px，版心是750px；
- 原因：两边留空，体验好。

![1567604618297](D:/Document/GitHub/Notes/images/1567604618297.png)
