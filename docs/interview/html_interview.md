### 1 position中absolute和fixed的区别
 * 共同点  
  (1) 改变行内元素的呈现方式，display被置为block；

  (2) 让元素脱离普通流，不占据空间；

  (3) 默认会覆盖到非定位元素上

 * 不同点：

   absolute的”根元素“是可以设置的，而fixed的”根元素“固定为浏览器窗口。

   当你滚动网页，fixed元素与浏览器窗口之间的距离是不变的。

### 2 img设置属性alt和title的区别 
  * alt 用于图片没显示时在图片显示区域显示一个说明文字。
  * title 表示鼠标在图片上停留时，显示一个悬浮框，其中显示的文字。 
  
### 3 行内元素，块级元素和空元素
  * 块级元素：div、ul、li、dl、dt、dd、p、h1-h6、blockquote    
    块级元素的特点：  
    1.总在新行上开始，占据一整行  
    2.默认情况下，其宽度自动填满其父元素宽度  
    3.宽度始终是与浏览器宽度一样，与内容无关  
    4.它可以容纳内联元素和其他块元素  
    5.display属性为block  
    6.块级元素的垂直相邻外边距margin会合并。

  * 行内元素：a、b、span、img、input、strong、select、label、em、button、textarea   
    行内元素的特点：  
    1.和其他元素都在一行上  
    2.高，行高及外边距和内边距部分可改变  
    3.宽度只与内容有关  
    4.行内元素只能容纳文本或者其他行内元素  
    5.display属性为inline  

    水平方向的padding-left、padding-right、margin-left、margin-right都产生边距效果，
    但竖直方向的padding-top、padding-bottom、margin-top、margin-bottom却不会产生边距效果。
    不可以设置宽高，其宽度随着内容增加，高度随字体大小而改变，内联元素可以设置外边界，但是外边界不对上下起作用，只能对左右起作用。

  * 空元素:br、meta、hr、link、input、img
    空元素的特点：

    1.没有内容的 HTML 内容被称为空元素。空元素是在开始标签中关闭的。br 就是没有关闭标签的空元素  
    2.在 XHTML、XML 以及未来版本的 HTML 中，所有元素必须被关闭。  
    3.在开始标签中添加斜杠，比如 < br />，是关闭空元素的正确方法，HTML、XHTML 和 XML 都接受这种方式。  
    4.即使 <br> 在所有浏览器中都是有效的，但使用 <br /> 其实是更长远的保障。

### 3 通过html控制默认浏览器版本，举例
  在html的header标签中添加  meta name="renderer" content="webkit"

### 4 html中什么是标签tag,举例说明
  * 单标签  br hr
  * 双标签  em i斜体 b strong p u del

### 5 什么是HTML WEB 存储？列举两种不同类型的HTML WEB 存储 和 html5 web 存储的好处?
cookie 不适合大量数据的存储，因为它们由每个对服务器的请求来传递，这使得 cookie 速度很慢而且效率也不高。

在 HTML5 中，数据不是由每个服务器请求传递的，而是只有在请求时使用数据。它使在不影响网站性能的情况下存储大量数据成为可能。

对于不同的网站，数据存储于不同的区域，并且一个网站只能访问其自身的数据。
  
检查浏览器是否支持

```js
 <script>
// 检查是否支持
if (typeof(Storage) !== "undefined") {
    // Store
    localStorage.setItem("lastname", "Gates");
    // Retrieve
    document.getElementById("result").innerHTML = localStorage.getItem("lastname");
} else {
    document.getElementById("result").innerHTML = "抱歉！您的浏览器不支持 Web Storage ...";
}
</script>

```
localStorage 和 sessionStorage 
客户端存储数据的两个对象为：

    localStorage - 用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去除。
    sessionStorage - 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。

localStorage 对象

    localStorage 对象存储的数据没有时间限制。第二天、第二周或下一年之后，数据依然可用。

sessionStorage 对象

    sessionStorage 方法针对一个 session 进行数据存储。当用户关闭浏览器窗口后，数据会被删除。

常用的API

    保存数据：localStorage.setItem(key,value);
    读取数据：localStorage.getItem(key);
    删除单个数据：localStorage.removeItem(key);
    删除所有数据：localStorage.clear();
    得到某个索引的key：localStorage.key(index);