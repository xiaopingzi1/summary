### 1 数组去重

```js
    // 思路1：定义一个新数组，并存放原数组的第一个元素，
    // 然后将元素组一一和新数组的元素对比，若不同则存放在新数组中。
    function unique(arr) {
      var res = [arr[0]];
      for (var i = 0;i < arr.length;i++) {
        var repeat = false;
        for (var j = 0;j<res.length;j++) {
          if (arr[i] === res[j]) {
            repeat = true;
            break;           
            alert(1);                        
          }
        }
        if (!repeat) {
          res.push(arr[i]);
        }
      }
      return res;
    }
    console.log(unique([1,2,1,2,3,4,3,1,3,4]));


  function unique(arr) {
  var temp = [];
  for (var i = 0;i < arr.length;i++) {
    if (temp.indexOf(arr[i]) == -1) {
      temp.push(arr[i]);
    }
  }
  return temp;
}
var arr = [1,2,3,1,2,4];
console.log(unique(arr));
```

### 2 使用正则表达式验证邮箱格式
### 3 计算数组arr所有元素的和
```js
  var arr = [1,2,3];
  var sum = 0;
  for (var i = 0;i <= arr.length;i++){
    sum += i
  }
  console.log(sum)

```
## 4 20190221面试代码题
```js
  (function(x) {
    delete x;
    alert(x); //6
  })(1+5);
 

  var a = 6;
  setTimeout(function() {
    alert(a);
    var a = 66;
  },1000);
  a = 666;
  alert(a);

  0 == '';// true
  NaN == NaN // false  因为NaN 是:Not a number (不是一个数字的缩写)

  [] == false //  []隐式转化为boolen时true
  [] == ![] // true

  //0 是逻辑的 false
  //1 是逻辑的 true
  //空字符串是逻辑的 false
  //null 是逻辑的 false
  //NaN 是逻辑的 false
  
  for (var i = 0;i<=3;i++) {
    setTimeout(function() {
      console.log(i);//4,4,4,4
    },0);
  };
 
  var a = new Object();
  a.value = 1;
  b = a;
  b.value = 2;
  alert(a.value);//2 直接把a对象的内存地址（或者说指针）复制给b，换句话说a和b实际上还是同一个对象
```

![](../assets/img/隐式转化.png)

## 4 
```js
// 方式1：一个构造函数嘛，里面有个全部变量getName 指向一个匿名函数
function Foo() {
  getName = function() {
    console.log(1);
  }
  return this;
}
// 方式2：构造函数的一个属性getName 指向一个匿名函数
Foo.getName = function() {
  console.log(2);
}
// 方式3：构造函数的原型上有个getName方法
Foo.prototype.getName = function() {
  console.log(3);
}
// 方式4：定义一个变量指针指向一个匿名函数
var getName = function() {
  console.log(4);
}
// 方式5：声明一个叫getName的有名函数
function getName() {
  console.log(5);
}
Foo.getName();//2 函数Foo的静态方法

getName();//4 
//当定义的变量和声明的函数重名（5,4)，它们都会进行预解析，函数声明提前于变量声明，但是最终会被变量覆盖

Foo().getName();//1  先执行方式1的“Foo()”,结果是"this" 并指向window，并产生了一个全局getName(window.getName)指针指向一个匿名函数，然后再执行"this.getName()" , 其实就是执行刚刚造出来的那个全局getName指向的匿名函数，所以输出“1”.

getName();//1 此句执行的是方式1执行出来的那个全局变量getName 指针指向的匿名函数，有人问为啥不执行方式4？方式4已经被覆盖了！所以结果为 “1”.

new Foo.getName();//2 首先还是先看运算符优先级吧，【new Foo() >  Foo() > new Foo】，先运算方式2的Foo.getName() 结果为“2”，再new一个Foo实例对象。

new Foo().getName();//3 先执行 new Foo(), 结果产生一个新的实例对象，并且继承了Foo()这个构造函数中的getName方法，所以再执行方式3函数块

new new Foo().getName();//3 先执行new Foo(),变成了 new Foo的实例对象.getName(), 然后再执行 Foo的实例对象.getName(),又回到了方式3函数块，结果为“3”，最后执行new Foo的实例对象。
```