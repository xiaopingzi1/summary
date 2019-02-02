### 1 vuex是什么，如何使用，那种功能场景使用
 * 专为 Vue.js 应用程序开发的状态管理模式，它采用集中式存储管理应用的所有组件的状态，并以相应的    规则保证状态以一种可预测的方式发生变化。
  
### 2 vue解决跨域的方法？详细说明
  * 1 后台更改header  
    header('Access-Control-Allow-Origin:*');  允许所有来源访问   
    header('Access-Control-Allow-Method:POST,GET');  允许访问的方式 　 　

  * 2 使用JQuery提供的jsonp 
    
    ```js
    methods: { 
      getData () { 
        var self = this 
        $.ajax({ 
          url: 'http://f.apiplus.cn/bj11x5.json', 
          type: 'GET', 
          dataType: 'JSONP', 
          success: function (res) { 
            self.data = res.data.slice(0, 3) 
            self.opencode = res.data[0].opencode.split(',') 
          } 
        }) 
      } 
    }  

    ```

  * 3 使用http-proxy-middleware 代理解决（项目使用vue-cli脚手架搭建）  
    例如请求的url: “http://f.apiplus.cn/bj11x5.json”

    ```js
    //打开config/index.js,在proxyTable中添写如下代码
    proxyTable: { 
     '/api': {  //使用"/api"来代替"http://f.apiplus.c" 
    target: 'http://f.apiplus.cn', //源地址 
    changeOrigin: true, //改变源 
    pathRewrite: { 
      '^/api': 'http://f.apiplus.cn' //路径重写 
      } 
    } 
  }
    //使用axios请求数据时直接使用“/api”
    getData () { 
     axios.get('/api/bj11x5.json', function (res) { 
       console.log(res) 
     })

    //通过这中方法去解决跨域，打包部署时还按这种方法会出问题。解决方法如下：
    let serverUrl = '/api/'  //本地调试时 
    // let serverUrl = 'http://f.apiplus.cn/'  //打包部署上线时 
    export default { 
       dataUrl: serverUrl + 'bj11x5.json' 
    }
    ```

### 3 vue常用的指令和用法