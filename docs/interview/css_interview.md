### 1 什么是css，列举例子来表示如何创建css规则以及如何应用于这个css至html元素(element)
    
    CSS 指层叠样式表 (Cascading Style Sheets)
    样式定义如何显示 HTML 元素
    样式通常存储在样式表中
    把样式添加到 HTML 4.0 中，是为了解决内容与表现分离的问题
    外部样式表可以极大提高工作效率
    外部样式表通常存储在 CSS 文件中
    多个样式定义可层叠为一

### 2 如何用css控制html元素的图层，举例
  定位
### 3 外部css和内部css之间有什么不同
  * 1 行内样式  
    p  style="font-size:14px;color:green;"直接在HTML标签中设置的样式</p>
  * 2 内部样式表  
    style标签写在head中
  * 3 外部样式表  
    链接式  
    link type="text/css" rel="styleSheet"  href="CSS文件路径" /  
    导入式  
    @import url("css文件路径");
  * 链接式和导入式的区别  
      link  
      1、属于XHTML  
      2、优先加载CSS文件到页面  

      @import  
      1、属于CSS2.1  
      2、先加载HTML结构在加载CSS文件。
    
### 4 如何使用原生的js(vanilla js)更改css规则，举例
  * 1通过在javascript代码中的node.style.cssText="css表达式1；css表达式2；css表达式3  "的方式直接更改CSS样式。  
    2先在CSS样式表中对特定的类如“active类”设置样式（这里的active类是假定的，暂时不存在），然后再在javascript代码中通过node.classname="active"使得CSS样式表中对active类的样式设置附加到该node节点上来。  

```js 
  <style type="text/css">
      div {
        float: left;
        padding: 20px;
        margin: 10px;
        border: 1px solid #000;
        background-color: #fff;
        color: #000;
      }
      .active
        {
          background-color:blue
        }
  </style>
  <body>
        <div class="root">
        </div>
  </body>

  <script type="text/javascript">  
     var root=document.getElementsByClassName("root")[0];
     root.style.cssText="background-color: blue;color: #fff;";
  </script>

  // 方式二
  <script type="text/javascript">  
      var root=document.getElementsByClassName("root")[0];
      root.className="active";
  </script>
```

### 5 什么是文件物模型(dom),画张简单的图来描述结构
DOM (Document Object Model) 译为文档对象模型，是 HTML 和 XML 文档的编程接口。  
HTML DOM 定义了访问和操作 HTML 文档的标准方法。  
DOM 以树结构表达 HTML 文档。

![](../assets/img/ct_htmltree.gif)

### 6 渐进增强和优雅降级
* 渐进增强原则   
   1 基本网页内容应该被所有浏览器访问  
   2 基本网页内容可以在所有浏览器中运行  
   3 增强的网页布局由外部提供的css引入
   4 尊重用户使用的浏览器首选项

* 优雅降级原则  
  争对最高级最完善的浏览器来设计网站，然后再争对浏览器测试和恢复