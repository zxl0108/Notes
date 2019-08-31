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

