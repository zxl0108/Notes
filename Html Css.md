# HTML标签

# 1.HTML基本标签

​	HTML:超文本标记语言；

## 字符集的问题


​	**meata标签的作用就是指定当前网页的字符集**

​	常用解决网页上的乱码的现象  在head标签中添加<meta charset="GBK”"/>

那么在企业开发中我们因该使用GBK(GB2312)还是UTF-8呢？

-如果网站仅仅包含中文，推荐使用GB2312，因为它的提及更小，访问速度更快；

-如果网站除了中文以外，还包含其他国家的语言，推荐使用UTF-8；

-推荐直接使用UTF-8即可。

​	**注意点：**在HTML文件中指定的字符集必须要和保存这个文件的字符集一致，否则还是会出现乱码。

​	所以仅仅指定字符集不一定能解决出现乱码的问题，还是需要保存文件的时候，文件保存的格式和指定的字符集一致才能保证没有出现乱码的问题。                                             

## DTD文档声明


​	任何一个标准的HTML网页，第一行一定是DTD文档声明，也就是说DTD文档说明必须写在HTML的第一行，且不区分大小写。

​	第一行必须要有DTD文字声明<!DTDCTYPE html>；

## 1.基本标签

### 1.H标签（标题）

​	H标签是用来给文本添加标题语义的，而不是用来修改文本的样式,H标签只有6个,且标签从大到小,在企业开发一般情况中只有一个H1标签(和SEO有关)。

### 2.Hr标签（分割线）

​	Hr就是在浏览器中添加一条分割线 ` <hr/>`  在HTML5中写不写斜杠都可以。

### 3.img标签

​	Img标签格式：`<img src="">` 显示图片 如果img标签指定的宽高，那么系统就会按照指定的宽高来显示。通俗的说就是指定一个宽度，另外的高度就会自动生成。`<img src="" width=……>`;

​	Title 用于告诉浏览器，挡鼠标悬停在图片上时，需要弹出描述框显示什么内容。使用方法`<img src="" title="……">`;

​	Alt其实是英文alternate 的缩写，它的作用就是用于告诉浏览器，当需要显示的图片找不到是显示什么  例如`<img src="" alt="对不起你需要查看的图片不见了">`;

### 4.Br标签（换行）

​	br标签，如何在HTML中换行？可以使用br标签；多个br标签使用就会换多行。

### 5.文本格式化标签

​	`b，I，s ，u `只有使用强调的意思,而`strong(加粗) em(倾斜) del(删除线) ins(下划线) `语义更加强烈；

### 6.A标签的基本使用及属性

​	a标签作用：控制页面与页面之间的跳转的;
​      ` <a href="指定需要跳转的目标界面">需要展现给用户查看的内容</a>`;

注意点： 1.a标签不仅可以让文字可以点击，还0.可以让图片也能够被点击(默认打开)；

​                2.一个a标签必须有一个href属性，否则a标签不知道要跳转到什么地方；
​                3.如果通过a标签的href属性指定一个地址，那么必须在地址前面加上http://或者是https：//；

### 7.Base标签

​	作用：专门用来统一的指定当前网页中所有的超链接需要如何打开。
​	注意点：1、base标签必须写在head标签的开始标签和接受标签之间。

​			2、就近原则，a标签中的target比base中的target更高级。

​			3、base标签放到head下边。

### 8.列表标签

HTML中列表标签的分类
       1无序列表（最多）（unordered list)；

<ul>
    <li>定义想要的内容</li>
</ul>

​	2有序列表（最少）(orderedlist)；

​       3定义列表（其次）(definitionlist)；

```html
 <dl>
      <dt>	</dt>
      <dd>	</dd>
</dl> 
//先通过dt标签定义列表中的所有标题，然后通过dd标签给每个标题添加描述信息;
```
### 9.表格标签


```html
<table>
	<tr>
       <td>单元内的文字</td>
   	</tr>
</table>
```

2.表格标签作用：用来给一堆数据添加表格语义
	 其实表格是一种数据的展现形式，当数据量非常大的时候，表格这种展现形式被认为是最为清晰的一种展现形式。

​       1.宽度（width）和高度（height）的属性：可以给table和td标签使用。
​        2.水平对齐（align）和垂直对齐（valign）的属性：就只有table标签不能使用valign。
​        3.外边距（cellspacing）和内边距（cellpadding）的属性：只能给table标签使用。

3.细线表格的制作方式： border   border=”1；
        1.给table标签设置bgcolor；
        2.给tr标签设置bgcolor；
        3.给table标签设置cellspacing="1px ；

​       4.align=”center”如果用在table上,是整个表格居中的方式,如果用在tr,th上是整行整列的居中。 

注意点：table标签和tr标签以及td标签都支持bgcolor属性。

4.**表格标题**
        在表格标签中提供了一个专门用来设置表格的标题，这个标签叫做caption。只要将标       题写在caption标签中，那么标题就会自动相对于表格的宽度居中。
        注意点：1.caption一定要写在table标签中，否则无效。

​                     2.caption一定要紧跟在table标签后面
 5.**标题单元格标签**
​               表格标签照片那个提供了一个标签专门用力存储每一列的标题，这个标签叫做th标签，只要将当前的标题存储在这个标签中就会自动居中+加粗文字。
​        到此为止我们就发现，其实表格中有两种单元格，一种是td，一种是th。td是专门用来存储数据的，th是专门用用来存储当前的标题的。

6.**caption:指定表格的标题(放在表格中,table下面)**
        thead作用：指定表格的表头信息(thead放在整个tr上边包裹整个tr的双标签)；
        tbody作用：指定表格的主体信息；
        tfoot作用：指定表格的附加信息；

7.**水平方向上的单元格合并(跨列合并)**
        可以给td标签添加一个colspan属性，来指定把某一个单元格当做多个单元格来看待；

```html
例如：	<td colspan="2"></td>；
```

8.**垂直向下的单元格合并(跨行合并)**

​	可以给td标签添加一个rowspan属性，来指定把某一个单元格当做多个单元格来看待；

```html
例如：	<td rowspan="2"></td>；
```

​      **含义：**把当前单元格当做两个单元格来看待；

**注意点：**
        1.由于把某一个单元格当做了多个单元来看到，所以就会多出一些单元格，所以需要删掉一些单元格才能正常显示；

           2. 横行竖列一定要记住单元格合并永远是先上后下或者先左后右，而不能向前或向上合并；

### 10.表单标签

![1566730340710](images/1566730340710.png)

​	作用：表单就是专门用来收集信息的。

```html
格式：
   <form>
          <表单元素>
   </form>
```
**常见的表单元素**

#####   1.明文输入框（可以看见）

```html
	<input type="text">;	placeholder占位符(用于控制输入框文字属性)；
```

#####   2.暗文输入框（看不见）

```html
	<input type="password">;
```

#####   3.给输入框设置默认值

```html
	<input type="text" value="（想设置的默认值）">;（在input标签里加上value标签）；
```

#####   4.单选框

```html
	<input type="radio">；
```

1. 在默认情况下单选框不会互斥，要想单选框互斥那么必须给每一个单选框标签都设置一个name属性，然后name属性还必须设置相同的值；
2. 如果要让单选框默认选中某一个框子，那么可以给input标签添加一个checked属性；
3. 在HTML中如果属性的取值和属性的名称一样可以只写一个（尽量不要忽略取值）；

```html
案例：       
	<input type="checkbox" checked="checked">唱歌(默认选择)
	<input type="checkbox" checked="checked">跳舞(默认选择)
	<input type="checkbox" checked="checked">绘画(默认选择)
	<input type="checkbox">篮球
	<input type="checkbox">足球
```

##### 5.按钮（表单标签）

​	**1.普通按钮	<input type="button" value="">**

​	**2.图片按钮	<input type="image" src="">**

​	**3.重置按钮	<input type="reset"> (清空表单中的内容）;**

​	**4.提交按钮	<input type="submit"> **

​	**5.隐藏域       <input type="hidden">（配合提交按钮，在后台提交数据，用户看不到）；**

提交按钮将表单中的数据提交到远程服务器需要具备的条件：

 	1. 给form标签添加action属性，通过其提交到指定服务器 action="http//:..."；
 	2. 给需要提交的元素添加name元素 name="username"（值可以随便写）；

#### 6.lable标签

**Label标签为input元素定义标注(标签)**

- label标签需要配合input使用 label for=”id”,for=input ”id属性的值”；

-  label标签作用:用于绑定一个表单元素,当点击label标签的时候,被绑定 的表单元素就会获得输入焦点。(便于用户体验)；

#### 7.Textrarea控件（文本域）

```html
用法：<textarea cols="每行中的字符数" rows="显示的行数">文本内容</ textarea>；
```

#### 8.下拉菜单(select)

使用select控件定义下拉菜单的基本语法格式如下:

```html
<select>

	<option>选项1</option>
	<option>选项2</option>
	<option>选项3</option>
</select>
```

**注意：**

​       1.<select></select>中至少应包含一对<option></option>。

​       2.在option 中定义selected =" selected "时，当前项即为默认选中项。

#### 9.表单域

- 在HTML中，form标签被用于定义表单域，即创建一个表单，以实现用户信息的收集和传递，form中的所有内容都会被提交给服务器。创建表单的基本语法格式如下：

```
	<form action="url地址" method="提交方式" name="表单名称">
    	（各种表单控件）；
	</form>
```

- 常用属性： 
  - Action 在表单收集到信息后，需要将信息传递给服务器进行处理，action属性用于指定接收并处理表单数据的服务器程序的url地址。
  - method 用于设置表单数据的提交方式，其取值为get或post。
  - name 用于指定表单的名称，以区分同一个页面中的多个表单。
  - 注意： 每个表单都应该有自己表单域。

# CSS3

CSS样式三种:行内式（内联样式）；内部样式表（内嵌样式表）；外部样式表（外链式）；

## CSS属性

### 1.文本样式

#### font-size（字号大小）

- 属性值：normal、bold、bolder、lighter、100~900（100的整数倍）多喜欢用于数字表示；
- font-size推荐使用像素值px(现在网页普遍使用14px)；

#### font-family（字体）

- 宋体(\5B8B\4F53)   微软雅黑(\5FAE\8F6F\96C5\9ED1)；

#### font-weight（字体粗细）

- 用于定义字体的粗细，其可用属性值：normal（400）、bold（700）、bolder、lighter；

#### font-style（字体风格）

- normal：默认值，浏览器会显示标准的字体样式；
- italic：浏览器会显示斜体的字体样式；
- oblique：浏览器会显示倾斜的字体样式；

#### letter-spacing （控制文字距离）

- 控制字(母)和字(母)之间的距离 值越大,间距越大,可以为负值；

#### line-height（行间距）

- 用于设置行间距，就是行与行之间的距离；

#### font（文字连写）

```html
{font: font-style  font-weight  font-size/line-height  font-family;}(必须保留font-size和font-family属性)
```

#### text-indent（首行缩进）

- 常用em(一个em一个汉字)；

#### text-align（文本水平对齐方式）

- 文本水平对齐方式:left,center,right；

#### text-decoration（文本的装饰）

- none (默认)   定义标准的文本， 取消下划线；
- underline      定义文本下的一条线，下划线 也是我们链接自带；
- overline         定义文本上的一条线；
- line-through 定义穿过文本下的一条线；

#### line-height（行高）

- 如果行高等height高度文字会垂直居中;如果行高大于高度文字偏下;如果行高小于高度文字偏上；

### 外观属性

#### background（背景）

##### Color三种方法

预定的颜色值 ；rgb代码rgb(255,0,0)；十六进制如(#FF6600)；

##### 背景颜色:background-color

- transparent (颜色透明);

##### 背景图片:background-image

- none(无背景) | url (图片地址);

##### 背景平铺:background-repeat

- repeat | no-repeat | repeat-x | repeat-y (背景在X,Y轴平铺);

##### 背景位置:background-position

- 1.length(百分数)；2.top , center , ,left , center ,right(方位名词)；

##### 背景固定滚动:background-attachment

- scroll(背景图像随对象滚动) ；fixed(背景图像固定)；

##### 背景简写:background

- 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置；

##### 背景尺寸:backgroud-size

- 该属性提供2个参数值(特性值cover和contain除外)。 
  - cover：  将背景图像等比缩放到完全覆盖容器，背景图像有可能超出容器。 
  - contain：  将背景图像等比缩放到宽度或高度与容器的宽度或高度相等，背景图像始终被包含在容器内。
- 如果提供两个具体的值(百分比或者像素值)，第一个定义背景图像宽度,第二个定义背景图像高度；
- 如果只提供一个值，该值将用于定义背景图像的宽度，第2个值默认为auto，此时背景图宽度等比缩放；

##### 背景线型渐变

- background-image: linear-gradient(to 方向,颜色, 颜色);

##### 多背景图片

- background:url(test1.jpg) no-repeat  10px 20px/50px 60px, url(test2.jpg) no-repeat  10px 20px/70px 90px;
- 注意， 背景颜色只能设置一次，且由于写在前面的背景会叠在之后的背景之上，所以背景色通常都定义在最后一组上，避免背景色将图像盖住。

##### 精灵技术

- CSS的精灵图需要配合背景图片(background-image)和背景定位(background-position)来使用。

- background-position属性进行背景定位。其中最关键的是使用background-position 属性精确地定位。

  ```css
  <style>
  	.box{
  		width: 86px;
  		height: 28px;
  		background-image: url(images/weibo.png);
  		background-position: -425px -200px;
  		}
  </style>
  <div class="box"></div>
  ```

#### 元素的显示与隐藏

##### 1.display（显示）

- display 设置或检索对象是否及如何显示。特点：隐藏之后，不再保留位置。
- display : none 隐藏对象；它相反的是 display：block除了转换为块级元素之外，同时还有显示元素的意思。

##### 2.visibility（可见性）

- 设置或检索是否显示对象。1.visible：对象可视 ；2.hidden ：对象隐藏；特点： 隐藏之后，继续保留原有位置。

##### 3.overflow（溢出）

- 检索或设置当对象的内容超过其指定高度及宽度时如何管理内容。
  - visible : 　不剪切内容也不添加滚动条。
  - auto : 　 超出自动显示滚动条，不超出不显示滚动条。
  - hidden : 　不显示超过对象尺寸的内容，超出的部分隐藏掉。
  - scroll : 　不管超出内容否，总是显示滚动条。

#### 用户界面样式

##### 1.cursor（鼠标样式）

- 设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。 cursor :  default  小白 | pointer  小手  | move  移动  |  text  文本。

##### 2.outline（轮廓 ）

- 绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。最直接的写法是： outline: 0; 或者outline: none。

##### 3.resize（防止拖拽文本域）

- resize：none 这个单词可以防止火狐，谷歌等浏览器随意的拖动文本域。

##### 4.white-space（溢出的文字隐藏）

- white-space设置或检索对象内文本显示方式。通常我们使用于强制一行显示内容 。

##### 5.text-overflow （文字溢出）

- 先强制一行内显示文本 white-space: nowrap;
- 超出的部分隐藏  overflow: hidden;
- 文字用省略号替代超出的部分 text-overflow: ellipsis;

##### 6.vertical-align（行内块垂直对齐方式）

- 设置或检索对象内容的垂直对其方式。	vertical-align : baseline |top |middle |bottom；
- vertical-align 不影响块级元素中的内容对齐，它只针对于行内元素或者行内块元素，特别是行内块元素,通常用来控制图片/表单与文字的对齐。

##### 7.CSS过渡动画

- 含义:过渡就是从一种状态到另一种状态,过渡需要出发条件，通常过渡写在开始状态。

## CSS3新特性

### 2D转换

#### 1.位移语法：transform: translate(x,y)

1. translate最多设置2个值，第一个值是水平，第二个值是垂直。
2. translate偏移的位置，参照的是自身原有的位置。
3. translate若设置负值时，会实现逆方向移动。
4. 若设置一个值时，只有水平方向有效。
5. 可以设置百分比，百分比参照的是自身的大小。

#### 2.旋转语法：transform:rotate(角度deg) 

- 正值：顺时针旋转；负值：逆时针旋转；

#### 3.旋转源点设置语法：transform-origin: 水平 垂直;

- 默认是按照中心点旋转的；
- 水平取值：left| center| right |像素；
- 垂直取值：top | center| bottom|像素；

#### 4.缩放语法：transform:scale(number,number)

1. 最多设置2个值，第一个值表示缩放宽度，第二值表示高度；
2. 缩小：若设置的值大于0小于1表示缩小；
3. 放大：若大于1表示放大多少倍；
4. 若设置一个值时，表示宽高一起缩放多少倍；

### 动画

#### 1.定义动画

```css
@keyframes 动画序列名称 {
	 from/0% {
      开始状态
  }  
 	to/100% {
      结束状态
  }}
```

#### 2.调用动画

##### animation-name（名称）

- 规定 @keyframes 动画的名称；

##### animation-duration（持续时间）

- 规定动画完成一个周期所花费的时间；

##### animation-timing-function（运动曲线）

- 规定动画的速度曲线。默认是 "ease" 缓冲，linear匀速，steps步长；

##### animation-delay（延迟时间）

- 规定动画何时开始。默认是 0；

##### animation-iteration-count（动画次数）

- 规定动画被播放的次数。默认是 1。还有 infinite；

##### animation-direction（是否逆播)

- 动画是否在下一周期逆向地播放。默认是 "normal"，alternate逆播放；

##### animation-play-state（运行暂停）

- 规定动画是否正在运行或暂停。默认是 "running"。还有“paused”；

##### animation-fill-mode(结束状态)

- 规定动画结束后状态，保持 forwards 回到起始 backwards；

##### animation: （连写）

- 动画的名称 动画持续的时间 运动的曲线 延迟时间 动画的次数 是否可以逆播 是否保持结束状态；

### 3D转换

#### 3D介绍

- 特点:近大远小。物体后面遮挡不可见；

#### 3维坐标系

- x轴：水平向右      注意： x 右边是正值，左边是负值 ；
- y轴：垂直向下      注意： y 下面是正值，上面是负值；
- z轴：垂直屏幕      注意： 往外面是正值，往里面是负值；

#### 位移

- transform: translateX/Y/Z(数值px)；

#### 透视语法：perspective: 像素值;

- 透视要设置给父元素；
- 设置3d透视，可以实现近大远小效果；
- 给设置了transform属性元素的上级元素设置透视即可；

#### 旋转 transform: rotateX/Y/Z(角度); 

- 对于立方体是由多个盒子旋转和位移组成的，多个盒子需要有一个父盒子；
- 若要显示立体空间，需要给父盒子设置样式属性：transform-style: preserve-3d；

