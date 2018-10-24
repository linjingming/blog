## 首先来看看我们在js中比较经==常用==到的==运算符==有哪些


```html

1 + 2 = 3;// 赋值运算符 =
 
条件 ? 表达式1 : 表达式2 // ?: 三元运算符

!表达式 // !取反

// 对象数组取值

window.location; // .可用用来对象取值

[1, 2][0] window['location'] // []用来数组取值，或者对象取值

// 算速运算符 加减乘除 取模 ++ --

1 + 1; // 加

2 - 1; // 减

1 * 1; // 乘

2 / 1; // 除

2 % 1; // 取模

a++ 或 ++a; // ++ 

a-- 或 --a; // -- 

// 比较运算符 小于、小于等于、大于、大于等于 等于、不等于、严格相等、严格不相等

1 < 2; // 小于

1 <= 1 // 小于等于

2 > 1; // 大于

1 >= 1; // 大于等于

1 == 1 // 等于

1 != 2 // 不等于

1 === 1 严格相等

1 !== 2 严格不相等

// 逻辑运算符 逻辑与 逻辑或

a && b // 逻辑与

a || b // 逻辑或

// 分组运算符 ()
(1 + 2) / (2 -1) // 分组
```
以上就是我们经常用到的运算符，但你真的了解这些运算符吗，如果运算符组合一起，哪个先执行，哪个后执行；下面我们先了解下运算符的优先级， 排序如下优先级从高到底排序，具有较高优先级的运算符先于较低优先级的运算符执行,相同优先级的运算符按执行顺序执行


运算符| 说明 | 执行顺序
---|---|---
() | 用于分组优先级最高 |
. [] () | .[]可以用于对象取值, ()函数调用; | 从左到右
++ -- | 后置递增或递减 列如a ++ | 从左到右
++ -- !| 前置递增或递减运算, 列如 --a, !取返 经常用来强制转换成布尔值 | 从右到左
* / % | 乘法 除法 取模 | 从左到右
+ - | 加法 减法 字符串相加 | 从左到右
< <= > >= |  小于、小于等于、大于、大于等于 | 从左到右
== != === !== | 等于、不等于、严格相等、严格不相等 | 从左到右
&& | 逻辑与 | 从左到右
\|\| | 逻辑或 | 从左到右
?: | 三元运算符 | 从右到左
= | 赋值运算符| 从右到左

## 先来看看几个运算符
### 逻辑与和逻辑或
> 逻辑与和逻辑非的运算结果不一定是布尔值,
列如a和b做逻辑运算，只要有一个不是布尔值，运算结果就不一定是布尔值。
1.  逻辑与运算，以a&&b为例;
-   假如a和b都是布尔值，有且a和b都为true结果才是true，否则为false   

```js
console.log(true && true); // true
console.log(true && false); // false
console.log(false && true); // false
console.log(false && false); // false
```
- 如果a为false,直接返回false,如果a为true,则直接返回b的值;
- 如果a不是布尔值;则首先通过Boolean(a)转成布尔值,如果Boolean(a)的值为false,则直接返回a的值, 如果Boolean(a)的结果为true,则返回b的值

```js
console.log(undefined && true); // 根据上面的规则 转换Boolean(undefined)值为false, 则直接返回a的值undefined 所以打印的值为undefined
console.log(NaN && {}); // 同理 结果为NaN
console.log(null && function(){}); // 同理 结果为null 
console.log('' && []); // 同理 结果为''
console.log(0 && ''); // 同理 结果为0
console.log([] && null); // 根据上面的规则 转换Boolean([])值为true, 则直接返回b的值null 所以打印的值为null
console.log({} && NaN); // 同理 结果为NaN
```
2.  逻辑或运算，以a||b为例;
-   假如a和b都是布尔值，当至少有一个值为true时，则返回true,否则为false   

```js
console.log(true && true); // true
console.log(true && false); // true
console.log(false && true); // true
console.log(false && false); // false
```
- 如果a为false,直接返回b的值,如果a为true,则直接返回true;
- 如果a不是布尔值;则首先通过Boolean(a)转成布尔值,如果Boolean(a)的值为false,则直接返回b的值, 如果Boolean(a)的结果为true,则直接返回a的值

```js
console.log(false || '') //根据规则 结果为 ''
console.log(true || '') // 结果为 true
console.log(0 || '') // 结果为 ''
console.log(null || 0) // 结果为 0
console.log([] || 0) // 结果为 []
```

### 递增++和递减--
1. i++ 与 ++i;
> 都能让i的值加1;区别在于返回值,i++的返回值是i, ++i的返回值是i + 1后的值。强调下这里返回值跟i要区分开理解, i是i, 返回值是返回值,两者不一样.
```js
// 列子1
var i = 1;
var a = i++;
console.log(a); // i++ 返回的是i的值 为1
console.log(i); // i递增了 值为2 
// 列子2
var i = 1;
var a = ++i;
console.log(a); // i++ 返回的是i + 1的值 为 1 + 1 = 2
console.log(i); // i递增了 值为2 

// 列子3
var a = 10, b = 20, c = 30, d;
a++;
++a;
d = ++a + (++b) + (c++) + a++;
console.log(d); // ？
```
2. i-- 和 --i;
> 同理,都能让i的值减1;区别在于返回值,i--的返回值是i, --i的返回值是i - 1后的值。
###  三元运算符 
> a ? b : c;  当a为真时就执行b否则执行c;  如果操作语句比较简单，建议用三目运算替代if..else, 让代码更加简洁.

```js
var a = true, b = false, res;

res =  a ? b ? 2 : 3 : 0; 
console.log(res) // res = 3; 相同优先级从右至左顺序执行， 先执行 b ? 2 : 3 的结果为 3 然后 a ? 3 : 0;

res = a || b ? 2 : 3; 
console.log(res); // res = 2; || 优先级较高 先执行 a || b 为 true ? 2 : 3; 所以结果为2；
```
