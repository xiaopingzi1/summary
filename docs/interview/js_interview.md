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


 
