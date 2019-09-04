# ECMAScript 6

## ECMAScript 6 介绍

- JS包含下面三个方面:ECMAScript（语法标准）   DOM（操作标签的一套API）   BOM（浏览器对象）；
- ES6 是新的 JS 的代码规范，提供了一些新特性，使我们可以开发大型应用；

### ES6的优点

- 提供了更加方便的新语法，**弥补** JS 语言本身的**缺陷**，新增了便捷的语法；
- 给内置对象增加了更多的方法；
- ES6 让 JS 可以开发复杂的大型项目，成为企业级开发语言；
- 新的前端项目中大量使用 ES6 的新语法；

## ECMAScript 6 新增语法

### let 和 const

- **let**
  - let 定义变量，变量不可以再次定义，但可以改变其值；
  - 具有块级作用域；
  - 没有变量提升，必须先定义再使用；
  - let声明的变量不会压到window对象中，是独立的；

```js
// 1.变量不可以再次定义，但可以改变其值；
	let a=2233;
	a=2222;
	console.log(a); //输出a为2222;
	let a=5555;
	console.log(a); //输出为Uncaught SyntaxError: Identifier 'a' has already been declared;

// 2.具有块级作用域，（块就是括号）；
	{
    	let age=18;
    	console.log(age);   //输出为 18
	}
    	console.log(age);       //输出为Uncaught ReferenceError: age is not defined
	for (let i = 0; i < 3; i++) {
    	}
	console.log(i);    //// 报错，此作用域中没有i的定义;
 
//3.没有变量提升,必须先定义再使用;
	console.log(age);   //未捕获的ReferenceError：在初始化之前无法访问'age';
    let age='男';

//4.let声明的变量不会压到window对象中,是独立的;
   let age=18;
   console.log(window.age); //输出为undefined;
```

> 如果使用var声明了变量，也不能再次用let声明了，反之也是不行的。实际开发要么全部使用var，要么全部使用let。

- **const**
  - 使用const关键字定义常量，常量名一般大写;
  - 常量是不可变的，一旦定义，则不能修改其值;
  - 初始化常量时，必须给初始值;
  - 具有块级作用域;
  - 没有变量提升，必须先定义再使用;
  - 常量也是独立的，定义后不会压入到window对象中;

```js
//2.一旦定义，则不能修改其值;
	const A=333;
    A=2222;     //输出Assignment to constant variable;
//3.初始化常量时,必须给初始值;
	const B;   // Missing initializer in const declaration;
```

- 小结

  | 关键字 | 变量提升 | 块级作用域 | 初始值 | 更改值 | 通过window调用 |
  | :----: | :------: | :--------: | :----: | :----: | :------------: |
  |  let   |    ×     |     √      |   -    |  Yes   |       No       |
  | const  |    ×     |     √      |  Yes   |   No   |       No       |
  |  var   |    √     |     ×      |   -    |  Yes   |      Yes       |

###  解构赋值

- ES 6 允许按照一定**模式**，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

#### 数组的解构

- 作用：方便获取数组中的某些项。

```js
let arr=[10,5,9,6]
// 情况1，变量少，值多(再变量,值相同下输出正常);
let [a,b,c]=arr;
console.log(a,b,c); //输出10,5,9;

// 情况2，变量多，值少;
let[g,h,i,j,k]=arr;
console.log(g,h,i,j,k); //输出10 5 9 6 undefined;

// 情况3，按需取值;
let[, ,n,]=arr;
console.log(n); //输出为9;

// 情况4，剩余值;
let cn = ['zhangsan', 18, ['175cm', '65kg']];
let[, ,[s,z]]=cn;
console.log(s,z);    // 175cm 65kg;
```

#### 对象的解构

- 作用:方便解析对象中的某些属性的值。

```js
//情况1，默认要求变量名和属性名一样
let{name,age}={name:'张扬',age:18};
console.log(name,age);  //输出张扬 18;

// 情况2，可以通过:为变量改名
let {a,b:c}={a:'hellow',b:'world'};
console.log(a,c);   // hello, world

// 情况3，变量名和属性名一致即可获取到值，不一定要一一对应;
let {b}={a:'hellow',b:'world'};
console.log(b); //输出为world;

// 情况4，剩余值
let obj={name:'张扬',age:18,gender:'男'};
let{name,...a}=obj;
console.log(name,a);    //输出张扬 b为{age: 18 gender: "男"}

//情况5，复杂的情况，只要符合模式，即可解构;
    let obj={
        name:'张扬',
        age:18,
        dog:{
            name:'毛毛',
            age:3,
        }
    };
    let{dog:{name,age}}=obj;
    console.log(name,age);  //输出毛毛 3
```

```js
// 实际应用：假设从服务器上获取的数据如下
let response = {
    data: ['a', 'b', 'c'],
    meta: {
        code: 200,
        msg: '获取数据成功'
    }
}
// 如何获取到 code 和 msg
let { meta: { code, msg } } = response;
console.log(code, msg); // 200, 获取数据成功；
```

### 函数

#### 箭头函数

- ES6 中允许使用箭头定义函数 (=>  goes to)，目的是**简化函数的定义**并且里面的this也比较特殊。

基本定义：

```js
// 非箭头函数
let fn = function (x) {
    return x * 2;
}
// 箭头函数，等同于上面的函数
let fn = (x) => {
    return x * 2;
}
```

特点：

- 形参只有一个，可以省略小括号；

  ```js
  let fn= x =>{
  	return x * 2;
  }
  ```

- 函数体只有一句话，可以省略大括号，并且表示返回函数体的内容;

  ```js
  let fn = (x, y) => {
      return x + y;
  }
  // 等同于
  let fn = (x, y) => x + y;
  ```

- 箭头函数内部没有 arguments;

  ```js
  let fn = () => {
      console.log(arguments); // 报错，arguments is not defined;
  };
  fn(1, 2);
  ```

- 箭头函数内部的 `this` 指向外部作用域中的 `this` ，或者可以认为箭头函数没有自己的 `this`;

  ```js
  var name = 'lisi'; // 测试时，这里必须用var，因为用let声明的变量不能使用window调用
  let obj = {
      name: 'zhangsan',
      fn : () => {
          console.log(this); // window对象
          console.log(this.name); // lisi
      }
  };
  obj.fn();
  ```

- 箭头函数不能作为构造函数；

  ```js
  let Person = () => {
  	
  };
  let obj = new Person(); // 报错，Person is not a constructor
  // 换个角度理解，箭头函数中都没有自己的this，怎么处理成员，所以不能当构造函数；
  ```

####  参数的默认值

- ES6 之前函数不能设置参数的默认值；

  ```js
  // ES5 中给参数设置默认值的变通做法
  function fn(x, y) {
      y = y || 'world';
      console.log(x, y);
  }
  fn(1)
  // ES6 中给函数设置默认值
  function fn(x, y = 'world') {
      console.log(x, y);
  }
  fn(2)
  fn(2,3)
  ```

  #### rest 参数

- rest 参数：剩余参数，以 … 修饰最后一个参数，把多余的参数都放到一个**数组**中。可以替代 arguments 的使用；

  ```js
  function fn(a, b, ...values) {
      console.log(a); // 6
      console.log(b); // 1
      console.log(values); // [100, 9, 10]
  }// 调用
  console.log(fn(6, 1, 100, 9, 10));
  ```

  > **注意：rest 参数只能是最后一个参数**

## 内置对象的扩展

### Array 的扩展

#### 扩展运算符

- 可以看成 rest 参数的逆运算，也可以看做是 **...** 可以把数组中的每一项展开。

```js
   //合并两个数组
    let arr1=[1,2];
    let arr2=[3,5];
    let arr3=[...arr1,...arr2];
    console.log(arr3);  // [1, 2, 3, 5]
    // 把数组展开作为参数，可以替代 apply
    // 求数组的最大值
    let arr=[6,99,10,5];
    let max=Math.max(...arr);
    console.log(max);   // 等同于 Math.max(6, 99, 10, 1);
```

#### Array.from()

- 把伪数组转换成数组；
- 伪数组必须有length属性，没有length将得到一个空数组；
- 转换后的数组长度，是根据伪数组的length决定的；

```js
  let fakeArr={
        0:'a',
        1:'b',
        2:'c',
        length:3,
    };
    let arr=Array.from(fakeArr);
    console.log(arr);
    // 转数组的对象必须有length值，因为得到的数组的成员个数是length指定的个数
// 上例中，如果length为2，则得到的数组为 ['a', 'b']
```

#### forEach遍历数组

- 要为forEach传递一个函数进来；
- 为forEach传递的函数有三个形参，分别表示数组的值、下标、当前的数组；

```js
// [xxx,xxx].forEach(function (value, index, arr) {
    // value 表示数组的值
    // index 表示数组的下标、索引
    // arr 表示当前的数组
// });

[3, 8, 4, 9].forEach(function (v, i, a) {
    console.log(v); // 表示数组的值 ，输出的结果是 3,8,4,9
    // console.log(i); // 表示数组的下标
    // console.log(a); // 表示数组
});

// 如果不需要下标和当前的数组，只使用value即可
// 函数可以使用箭头函数
[3, 8, 4, 9].forEach((item) => {
    console.log(item);
});
// 下面的意思是循环，在循环数组的时候，输出数组的每个值
[3, 8, 4, 9].forEach(item => console.log(item));
```

#### 数组实例的 find() 和 findIndex()

> - find和findIndex方法，会遍历传递进来的数组。
> - 回调函数有三个参数，分别表示数组的值、索引及整个数组。
> - 回调函数中return的是一个条件，find和findIndex方法的返回值就是满足这个条件的第一个元素或索引。
> - **find** 找到数组中第一个满足条件的成员并**返回该成员**，如果找不到返回**undefined**。
> - **findIndex** 找到数组中第一个满足条件的成员并**返回该成员的索引**，如果找不到返回 **-1**。

```js
// 用法：找数组中特定的数字；
	let arr = [1, 2, 4, 0, -4, -6, -7];
    let result = arr.find(function (item, index, self) {
        return item > 3;	//遍历过程中，根据这个条件去查找
    })
    console.log(result);  //输出4
```

#### 数组实例的 includes()

> - 判断数组是否包含某个值，返回 true / false；
> - 参数1，必须，表示查找的内容；
> - 参数2，可选，表示开始查找的位置，0表示开头的位置；

```js
	let arr=[1,4,3,9];
    console.log(arr.includes(4));   	// true;
    console.log(arr.includes(4,2));    // false， 从2的位置开始查，所以没有找到4;
```

#### String的扩展--模板字符串

> - 模板字符串解决了字符串拼接不便的问题
> - 模板字符串使用反引号 **`** 括起来内容
> - 模板字符串中的内容可以换行
> - 变量在模板字符串中使用 `${name}` 来表示，不用加 + 符号

```js
let name = 'zs';
let age = 18;
// 拼接多个变量，在模板字符串中使用占位的方式，更易懂
let str = `我是${name}，今年${age}`;
```

#### includes(), startsWith(), endsWith()区别

- `includes(str, [position])`		 返回布尔值，表示是否找到了参数字符串。
- `startsWidth(str, [position])` 返回布尔值，表示参数字符串是否在原字符串的头部或指定位置。
- `endsWith(str, [length])`            返回布尔值，表示参数字符串是否在原字符串的尾部或指定位置。

```js
console.log('hello world'.startsWith('l', 2)); // 指定位置的字符是l，返回true;
console.log('hello world'.endsWith('d')); // 未指定位置，结尾是d，返回true;
```

#### repeat()

- `repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

```js
	let html = '<li>itheima</li>';
    html = html.repeat(10);
    console.log(html);	//输出<li>itheima</li>*10次
```

#### trim()

- `trim()` 方法可以去掉字符串两边的空白。

```js
console.log('    hello        '.trim()); // hello
```

###  Number的扩展

ES6 将全局方法`parseInt()`和`parseFloat()`，移植到`Number`对象上面，功能完全保持不变。

- Number.parseInt()
- Number.parseFloat()

```js
console.log(parseInt('123abc'))
// ES6中，将parseInt移植到了Number对象上;
console.log(Number.parseInt('123abc'))
```

### Set

ES6 提供了新的数据结构 Set。它类似于数组，但是==成员的值都是唯一的==，没有重复的值。

- `Set`本身是一个构造函数，用来生成 Set 数据结构。
- Set的特点就是该对象里面的成员不会有重复。

- Set 的成员
  - `size`：属性获取 set中成员的个数，相当于数组中的 length。
  - `add(value)`：添加某个值，返回 Set 结构本身。
  - `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
  - `has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
  - `clear()`：清除所有成员，没有返回值。

```js
let s=new Set();
    s.add(3);
    s.add(6);
    s.add(6);// Set对象中的成员都是唯一的，前面添加过6了，所以这里添加无效;
    console.log(s);	//输出成员个数2;
    console.log(s); // {3, 6};
```

另外初始化Set的时候，也可以为其传入数组或字符串，得到的Set对象中的成员不会有重复。

根据这个特点可以完成数组或字符串去重。

```js
// Set 可以通过一个数组初始化
let set=new Set([1,2,3,5,2,3]);
console.log(set);   //Set(4){1.2.3.5}
// 数组去重
let arr=[...set];    // 方式一
console.log(arr);   //输出[1,2,3,5]
console.log(Array.from(set)); //方式二 from是将伪数组变为数组;输出[1,2,3,5];

// 完成字符串去重;
let str=[...new Set('abcddcd')].join('');
console.log(str);   //abcd
```

## 定义对象的简洁方式

<!--04-语法-简洁的定义对象的方式-->

```js
let name = 'zhangsan', age = 20, gender = '女';
let obj = {
    name: name, // 原来的写法
    age, // 对象属性和变量名相同，可以省略后面的 “:age”，下面的gender同理
    gender,
    fn1: () => {  // 常规的箭头函数写法
        console.log(123);
    },
    fn2 () { // 可以省略 “:” 和 “=>”
        console.log(456);
    }
};
console.log(obj.age); // 20
obj.fn2(); // 456
```

