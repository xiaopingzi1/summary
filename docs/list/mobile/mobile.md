### 1 px rem 和 em 的区别
* px  
  px像素，相对长度单位，是相对于显示器屏幕分辨率而言  
  特点：IE无法调整使用Px作为单位的字体大小

* em  
  1.em的值是不固定的  
  2.em会继承父元素字体的大小  
  浏览器默认字体高是16px,在使用中将body设置为62.5%,em的值变为10px

* rem  
  是c3新增加的单位，相对的是html的跟元素,默认16px,通过rem可以做到只修改根元素就可按照比例调整所有字体的大小

* em 和 rem 的区别  
  em是根据父元素继承相应的大小，不是固定的  
  rem继承html跟元素的大小，只有改变html的值才可以改变rem的值

### 2 移动端让页面适配网页大小的meta标签
 * <meta name="eqMobileViewport" content="width=320,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/>

  