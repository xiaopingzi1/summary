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
### 4 html中什么是标签tag,举例说明
  * 单标签，双标签
### 5 什么是HTML WEB 存储？列举两种不同类型的HTML WEB 存储 和 html5 web 存储的好处?