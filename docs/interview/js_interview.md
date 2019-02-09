### 1 split 和 join 的区别
   * Split()方法用于把一个字符串分割成字符串数组.   
     stringObject.split(a,b)这是它的语法  
     a是必须的决定个从a这分割  
     b不是必须的，可选。该参数可指定返回的数组的最大长度 。  
     如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。
     注意返回的数组中不包括a本身。
--------------------- 
   * Join()方法是将数组转换成字符串。  
      1.join() 方法用于把数组中的所有元素放入一个字符串。  
      元素是通过指定的分隔符进行分隔的。  
      指定分隔符方法join("#");其中#可以是任意.  

### 2 详细介绍了解的for循环 
  ##### 一 for 
* 1 for循环中的i在循环结束之后任然存在于作用域中，因为ECMAScript中不存在块级作用域，即使i是在循环内部定义的一个变量，但在循环外部仍然可以访问到它，所以为了避免影响作用域中的其他变量，使用函数自执行的方式将其隔离起来()();
* 2 避免使用for(var i=0; i<demo1Arr.length; i++){} 的方式，这样的数组长度每次都被计算，效率低于上面的方式。也可以将变量声明放在for的前面来执行，提高阅读性；  
    1 var i = 0, len = demo1Arr.length;
    2 for(; i<len; i++) {};
* 3 跳出循环的方式有如下几种
    return 函数执行被终止
    break 循环被终止，退出当前循环
    continue 循环被跳过，即退出当次循环，继续下一次循环
    
  ##### 二 for in
*    for(var item in arr|obj){} 可以用于遍历数组和对象
    遍历数组时，item表示索引值， arr表示当前索引值对应的元素 arr[item]
    遍历对象时，item表示key值，obj表示key值对应的value值 obj[item]

  ##### 三 foreach 
* demoArr.forEach(function(arg) {}) arg表示数组中的每一项元素
* 注意事项：
* 回调函数中有2个参数，分别表示值和索引，这一点与jQuery中的$.each相反
* forEach无法遍历对象
* forEach无法在IE中使用，firefox和chrome实现了该方法
* forEach无法使用break，continue跳出循环，使用return时，效果和在for循环中使用continue一致
* 最重要的一点，可以添加第二参数，为一个数组，而且回调函数中的this会指向这个数组。而如果没有第二参数，则this会指向window。
  
```js
var newArr = [];
demoArr.forEach(function(val, index) {
     this.push(val); // 这里的this指向newArr
 }, newArr) 
```

  ##### 四 do/while

  ##### 五 $.each
 * $.each(demoArr|demoObj, function(e, ele))
 * 注意事项：
* 使用return 或者return true为跳过一次循环，继续执行后面的循环
* 使用return false为终止循环的执行，但是并不终止函数执行
* 无法使用break与continue来跳过循环

  ##### 六 $(selecter).each 专门用来遍历DOMList


### 3 js如何检测变量是字符串类型，写出函数实现

```js
function a(obj){
   return typeof(obj)=="string";
}
alert(a(123));
alert(a("abc"));

function b(obj){
   return obj.constructor === String
}
alert(b(123));
alert(b("abc"));

function type(data){
   return Object.prototype.toString.call(data).slice(8,-1).toLowerCase();
}
alert(type(123));
alert(type("abc"));
--------------------- 
```

### 4 如何让判断Js数据类型
typeof、instanceof、 constructor、 prototype方法比较
  > 1.使用typeof操作符

    (1) undefined：如果这个值未定义
    (2) boolean：如果这个值是布尔值
    (3) string：如果这个值是字符串
    (4) number：如果这个值是数值
    (5) object：如果这个值是对象或null
    (6) function：如果这个值是函数

    需要注意：typeof不适合用于判断是否为数组。当使用typeof判断数组和对象的时候，都会返回object
          可以使用isArray()来判断是否为数组。

  > 2.instanceof

    instanceof 运算符用来判断一个构造函数的prototype属性所指向的对象是否存在另外一个要检测对象的原型链上。需要区分大小写。
    简单的来说，instanceof 用于判断一个变量是否某个对象的实例。

```js
　　    var arr = new Array( );
　　　　alert(arr instanceof Array);   // 返回true
 ```
　　注意：instanceof只能用来判断对象和函数，不能用来判断字符串和数字等。判断它是否为字符串和数字     时，只会返回false。

   > 3.constructor

     constructor 属性返回对创建此对象的数组函数的引用。  
     在JavaScript中，每个具有原型的对象都会自动获得constructor属性。

```js
// String
var str = "字符串";
alert(str.constructor); // function String() { [native code] 这是JavaScript的底层内部代码实现，无法显示代码细节。　　}
alert(str.constructor === String); // true

// Array
var arr = [1, 2, 3];
alert(arr.constructor); // function Array() { [native code] }
alert(arr.constructor === Array); // true

// Number
var num = 5;
alert(num.constructor); // function Number() { [native code] }
alert(num.constructor === Number); // true
```

  > 4.prototype

    以上三种方法多少都会有一些不能判断的情况。为了保证兼容性，可以通过Object.prototype.toString方法，判断某个对象值属于哪种内置类型。

```js
// 注意区分大小写
alert(Object.prototype.toString.call(“字符串”) === ‘[object String]’) -------> true;
alert(Object.prototype.toString.call(123) === ‘[object Number]’) -------> true;
alert(Object.prototype.toString.call([1,2,3]) === ‘[object Array]’) -------> true;
alert(Object.prototype.toString.call(new Date()) === ‘[object Date]’) -------> true;
alert(Object.prototype.toString.call(function a(){}) === ‘[object Function]’) -------> true;
alert(Object.prototype.toString.call({}) === ‘[object Object]’) -------> true;

```