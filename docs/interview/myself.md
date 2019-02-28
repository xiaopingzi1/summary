## 1 Json对象和字符串的相互转化
  JSON.stringify(obj)      将JSON对象转为字符串。  
  JSON.parse(string)       将字符串转为JSON对象格式。 parse(解析，理解)
## 2 ajax  axios 和 fetch 的区别
  > 1.jQuery ajax 

  ```js
    $.ajax({
      type: 'POST',
      url: url,
      data: data,
      dataType: dataType,
      success: function () {},
      error: function () {}
    });
  ```
  > 优缺点：

    本身是针对MVC的编程,不符合现在前端MVVM的浪潮
    基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
    JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）

  > 2.axios

  ```js 
  axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
  })
    .then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.log(error);
    });



    文档
    // 为给定 ID 的 user 创建请求
    axios.get('/user?ID=12345')
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });

    // 可选地，上面的请求可以这样做
    axios.get('/user', {
        params: {
          ID: 12345
        }
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      });

  ```

  > 优缺点：  

    从 node.js 创建 http 请求  
    支持 Promise API  
    客户端支持防止CSRF  
    提供了一些并发请求的接口（重要，方便了很多的操作）  

  > 3.fetch

  ```js
    try {
      let response = await fetch(url);
      let data = response.json();
      console.log(data);
    } catch(e) {
      console.log("Oops, error", e);
    }
  ```
  
  >优缺点：
    
    优点
    符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里
    更好更方便的写法
    更加底层，提供的API丰富（request, response）
    脱离了XHR，是ES规范里新的实现方式
    
    缺点
    1）fetchtch只对网络请求报错，对400，500都当做成功的请求，需要封装去处理
    2）fetch默认不会带cookie，需要添加配置项
    3）fetch不支持abort，不支持超时控制，  
    使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了量的浪费
    4）fetch没有办法原生监测请求的进度，而XHR可以

   > fetch 

     fetch是基于Promise设计，支持async和await

  > 为什么要用axios

    axios 是一个基于Promise 用于浏览器和 nodejs 的 HTTP 客户端，它本身具有以下特征：

    从浏览器中创建 XMLHttpRequest,本质也是对原生xhr的封装
    从 node.js 发出 http 请求
    支持 Promise API
    拦截请求和响应
    转换请求和响应数据
    取消请求
    自动转换JSON数据
    客户端支持防止CSRF/XSRF
    防止CSRF:就是让你的每个请求都带一个从cookie中拿到的key, 根据浏览器同源策略，  
    假冒的网站是拿不到你cookie中得key的，这样，后台就可以轻松辨别出这个请求是否是用户在假冒网站上的误导输入，  
    从而采取正确的策略。

## 3 h5plus
  > h5 plus 是什么

    HTML5+是中国HTML5产业联盟的扩展规范，基于HTML5扩展了大量调用设备的能力，使得web语言可以想原生语言一样强大。

  >HTML5+运行环境

   *Runtime版 – for App（运行环境与项目代码打包为原生APP）*  
   使用HTML5开发，然后使用HBuilder提供的云打包或本地打包将可以把5+ Runtime和开发者编写的HTML5页面打包为原生App的安装包，包括Android的apk和iOS的ipa。发行到原生应用市场。

   *SDK版 – for Hybrid（原生APP中构建H5+运行环境）*  
   在你的原生应用中内嵌5+ SDK，替代手机默认的webview，无论使用Hybrid开发模式，还是在原生App中构建web应用生态，都将能体验到更强大的内核动力。

  > 配套工具
   
   HBuilder  
   HTML5+项目的开发工具，既是代码编辑器，也是基于H5+的APP打包工具。

   MUI框架  
   一个与HTML5+配套的样式框架

## 3 jquery和zepto的区别
   * zepto是针对高级浏览器的js库，有触摸事件，不兼容IE

## 4 富文本编辑器的原理
## 5 上传图片时图片较大怎么处理
* 进行压缩处理，再转成file文件上传

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<img src ="">
<input type="file" style="" accept="image/*">
<script src="jquery-1.js"></script>
<script>
    $("input").on("change",select_img);
    function select_img() {//当input file值改变时触发的事件
        console.log($("input")[0].files);
        var img_size = $("input")[0].files[0].size; //用来判断大小
        const reader = new FileReader();//图片预览
        reader.readAsDataURL($("input")[0].files[0]);
        reader.onload = function(e) {
            if (img_size >= 1024 * 1024 *0.1) { //意思是大于0.5m 就进行处理
                console.log("图片太大");
                compressImage(e.target.result);//调用自定义方法来处理图片
            }
            else {
                const src = e.target.result;
                $("img").attr("src",src) ;
            }
        }
    }
    function  compressImage(bdata) {//压缩图片
        console.log(bdata);
        var quality = 1; //压缩图片的质量
        var oldimglength = bdata.length;//压缩前的大小
        var compresRadio = 0;// 压缩率
        var canvas = document.createElement("canvas"); //创建画布
        var ctx = canvas.getContext("2d");
        var img = new Image();
        img.src = bdata;
        img.onload = function(){
            var width = img.width;
            var height = img.height;
            canvas.width = 500;   //这里可以自定义你的图片大小
            canvas.height = 500 * (img.height / img.width);
            ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
            var cdata = canvas.toDataURL("image/png",quality);  //将图片转为Base64 之后预览要用
            $("img").attr("src",cdata);
            var newimglength = cdata.length;
            console.log("img-blob:"+oldimglength);//压缩前大小
            console.log("ctx-blob:"+newimglength) ;//压缩后大小
            compresRadio = (((oldimglength-newimglength)/oldimglength*100).toFixed(2))+'%';
            console.log("压缩率:"+compresRadio)
            var arr = cdata.split(',');
            var mime = arr[0].match(/:(.*?);/)[1];
            var bstr = atob(arr[1]);
            var n = bstr.length;
            var u8arr = new Uint8Array(n);
            while(n--){
                u8arr[n] = bstr.charCodeAt(n);
            }
            console.log(new File([u8arr],"压缩", {type:mime}))
        }
    }
 
 
</script>
</body>
</html>
```
## 6 HTML中& nbsp; & ensp; & emsp; & thinsp;等6种空白空格的区别 

HTML提供了5种空格实体（space entity），它们拥有不同的宽度，非断行空格（& nbsp;）是常规空格的宽度，可运行于所有主流浏览器。其他几种空格（ & ensp; & emsp; & thinsp; & zwnj;& zwj;）在不同浏览器中宽度各异。
 
& nbsp;        
 
它叫不换行空格，全称No-Break Space，它是最常见和我们使用最多的空格，大多数的人可能只接触了&nbsp;，它是按下space键产生的空格。在HTML中，如果你用空格键产生此空格，空格是不会累加的（只算1个）。要使用html实体表示才可累加，该空格占据宽度受字体影响明显而强烈。
 
& ensp;        
 
它叫“半角空格”，全称是En Space，en是字体排印学的计量单位，为em宽度的一半。根据定义，它等同于字体度的一半（如16px字体中就是8px）。名义上是小写字母n的宽度。此空格传承空格家族一贯的特性：透明的，此空格有个相当稳健的特性，就是其占据的宽度正好是1/2个中文宽度，而且基本上不受字体影响。
 
& emsp;        
 
它叫“全角空格”，全称是Em Space，em是字体排印学的计量单位，相当于当前指定的点数。例如，1 em在16px的字体中就是16px。此空格也传承空格家族一贯的特性：透明的，此空格也有个相当稳健的特性，就是其占据的宽度正好是1个中文宽度，而且基本上不受字体影响。
 
& thinsp;        
 
它叫窄空格，全称是Thin Space。我们不妨称之为“瘦弱空格”，就是该空格长得比较瘦弱，身体单薄，占据的宽度比较小。它是em之六分之一宽。
 
& zwnj; 
 
它叫零宽不连字，全称是Zero Width Non Joiner，简称“ZWNJ”，是一个不打印字符，放在电子文本的两个字符之间，抑制本来会发生的连字，而是以这两个字符原本的字形来绘制。Unicode中的零宽不连字字符映射为“”（zero width non-joiner，U+200C），HTML字符值引用为： & #8204;
 
& zwj;
 
它叫零宽连字，全称是Zero Width Joiner，简称“ZWJ”，是一个不打印字符，放在某些需要复杂排版语言（如阿拉伯语、印地语）的两个字符之间，使得这两个本不会发生连字的字符产生了连字效果。零宽连字符的Unicode码位是U+200D (HTML: & #8205; & zwj;）。
 
此外，浏览器还会把以下字符当作空白进行解析：空格（& #x0020;）、制表位（& #x0009;）、换行（& #x000A;）和回车（& #x000D;）还有（& #12288;）等等。

## 7 vue项目中遇到的坑
 1 当我们在路由中配置了不同的router-link对应于不同的组件的时候，会发现npm run dev之后什么都没有，比如我的路由如下：
 ```js
export default new Router({
  routes: [
    {
      path: '/Mall',
      component: Mall
    },
    {
      path: '/personal-center',
      component: personalCenter
    }, 
    {
      path: '/order',
      component: AlipayHint
    },
    {
      path: '/commodity',
      component: Commodity
    }
  ]
});
 ```
 运行之后，是空白页，这是因为路由中并没有配置一进来是“/”的路由，所以什么都没有显示，这时就需要重定向了。如下所示：
 ```js
routes: [
    {
      path: '/Mall',
      component: Mall
    },
    {
      path: '/personal-center',
      component: personalCenter
    }, 
    {
      path: '/order',
      component: AlipayHint
    },
    {
      path: '/commodity',
      component: Commodity
    },
    {
      path: "/",
      redirect: "/commodity"
    }
  ]
 ```
 2 在vue中，我们可以使用v-on:click.once对click处理函数只绑定一次，


## 8 node的优缺点
## 9 html的兼容性问题
1、浏览器默认的margin和padding不同。  
解决办法：使用*{margin：0；padding：0；}

2、IE6双边bug问题。  
如果给块级元素同时设置了margin-left和float：left；lIE6浏览器会解析margin-left值为2倍。或者设置了margin-right和float: right;浏览器会解析margin-right值为2倍。  
解决办法：加上_display:inline; （_display是IE6特有的写法） 

3、超链接访问之后hover样式不出现了，被点击后也不具有active和hover样式。  
方法：按照顺序写 ：a:link{   }  a:visited{  } a:hover{  } a:active{   }

4、上下margin会重合的问题。
margin-left和margin-right不会重合，但是margin-top和margin-bottom会重合。  
解决办法：养成良好的书写习惯，同时书写margin-top或者同时书写margin-bottm。

## 10 异步上传图片
```html
<form class="form-horizontal"enctype="multipart" id="form_edit">
  <div class="form-group">
    <label class="col-sm-3 control-label">头像</label>
    <div class="col-sm-6">
      <label class="form-image">
        <input id="avatar" type="file" name="file_img">
        <img src="<?php echo $info['admin_pic'];?>" id="avatar_img">
        <i class="mask fa fa-upload"></i>
      </label>
      <!-- 用来保存图片的信息 -->
      <input type="hidden" name="temp" id="temp">
    </div>
  </div>
</form>

```

```js
    //上传管理员头像
    $('#avatar').change(function () {
      //转化为jquery对象
      var file = document.getElementById('avatar').files[0];
      var fd = new FormData();
      fd.append('f',file);
      // console.dir(file);
      $.ajax({
        url:'uploadImg.php',
        data:fd,
        type:'post',
        dataType:'text',
        contentType:false,
        processData:false,
        success:function (data) {
          // console.log(data);
          if (data == 2) {                                                                                                                                                                                          
            layer.msg('头像上传失败');
          } else {
            $('#avatar_img').attr('src',data);
            layer.msg('头像上传成功');
          }
        }
      })
    })


```

下面的代码将创建一个空的FormData对象:
```js
var formData = new FormData(); // 当前为空
```
你可以使用FormData.append来添加键/值对到表单里面；
```js
formData.append('username', 'Chris');
```
* FormData对象的优势就是能够一次性将表单中的所有数据全部取出，包括文件域，文件对象
* 使用formdata对象后，必须使用post方式来发送ajax请求
* 将formdata对象作为参数传入send中

## 11常见的加密方式
1.Base64

2.MD5