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

 ## 8 移动端常见的兼容性问题
 1、安卓浏览器看背景图片，有些设备会模糊。用同等比例的图片在PC机上很清楚，但是手机上很模糊
 
 是devicePixelRatio作怪，因为手机分辨率太小，如果按照分辨率来显示网页，这样字会非常小，所以苹果当初就把iPhone 4的960* 640分辨率，在网页里只显示了480* 320，这样devicePixelRatio＝2。
 
 现在android比较乱，有1.5的，有2的也有3的。想让图片在手机里显示更为清晰，必须使用2x的背景图来代替img标签（一般情况都是用2倍）。例如一个div的宽高是100* 100，背景图必须得200*200，然后background-size:contain;，这样显示出来的图片就比较清晰了。
 
 代码可以如下：
 ```css
 background:url(../images/icon/all.png) no-repeat center center;  
 -webkit-background-size:50px 50px;
 background-size: 50px 50px;
 display:inline-block; 
 width:100%; 
 height:50px;
 或者background-size:contain;
 ```

2、假如手机网站不用兼容IE浏览器，一般我们会使用zeptojs
zeptojs内置Touch events方法，Touch events看了一下zeptio新版的API，已经支持IE10以上浏览器，对zeptojs可以选择使用！

3、防止手机中网页放大和缩小
```css
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=0" />
```

4、长时间按住页面出现闪退
```css
element {

-webkit-touch-callout:none;

}
```
5、iphone及ipad下输入框默认内阴影
```css
Element{

-webkit-appearance:none;

}
```
6、ios和android下触摸元素时出现半透明灰色遮罩
```css
Element {

-webkit-tap-highlight-color:rgba(255,255,255,0)

}
```
设置alpha值为0就可以去除半透明灰色遮罩，备注：transparent的属性值在android下无效。

7、旋转屏幕时，字体大小调整的问题
```css
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6{

-webkit-text-size-adjust:100%;

}
```

8、圆角bug

某些Android手机圆角失效
```css
background-clip: padding-box;

background-clip 属性规定背景的绘制区域。
border-box 	背景被裁剪到边框盒。 	
padding-box 	背景被裁剪到内边距框。 	
content-box 	背景被裁剪到内容框。
```

9、设置缓存

手机页面通常在第一次加载后会进行缓存，然后每次刷新会使用缓存而不是去重新向服务器发送请求。如果不希望使用缓存可以设置no-cache。

10、 IOS中input键盘事件keyup、keydown、keypress支持不是很好
问题是这样的，用input search做模糊搜索的时候，在键盘里面输入关键词，会通过ajax后台查询，然后返回数据，然后再对返回的数据进行关键词标红。

用input监听键盘keyup事件，在安卓手机浏览器中是可以的，但是在ios手机浏览器中变红很慢，用输入法输入之后，并未立刻相应keyup事件，只有在通过删除之后才能相应！

解决办法：可以用html5的oninput事件去代替
```js
keyupdocument.getElementById('testInput').addEventListener('input',function(e){varvalue = e.target.value;});
```
然后就达到类似keyup的效果！

11、ios 设置input 按钮样式会被默认样式覆盖

解决方式如下：
```css
input,

textarea {

border: 0;

-webkit-appearance: none;

}
```
设置默认样式为none

12、移动端点透问题
div是绝对定位的蒙层,并且z-index高于a。而a标签是页面中的一个链接

我们给div绑定tap事件：
```js
$('#haorooms').on('tap',function(){$('#haorooms').hide();});
```
我们点击蒙层时 div正常消失，但是当我们在a标签上点击蒙层时，发现a链接被触发，这就是所谓的点透事件。

原因：touchstart 早于 touchend 早于click。 即click的触发是有延迟的，这个时间大概在300ms左右，也就是说我们tap触发之后蒙层隐藏， 此时 click还没有触发，300ms之后由于蒙层隐藏，我们的click触发到了下面的a链接上。

解决：

（1）尽量都使用touch事件来替换click事件。例如用touchend事件(推荐)。  
（2）用fastclick
（3）用preventDefault阻止a标签的click  
（4）延迟一定的时间(300ms+)来处理事件 （不推荐）  
（5）以上一般都能解决，实在不行就换成click事件。

下面介绍一下touchend事件，如下： 

$("#haorooms").on("touchend",function(event) {event.preventDefault();});

