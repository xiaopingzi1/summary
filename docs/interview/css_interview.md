### 1 什么是css，列举例子来表示如何创建css规则以及如何应用于这个css至html元素(element)
### 2 如何用css控制html元素的图层，举例
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