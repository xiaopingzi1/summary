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