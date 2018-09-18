### 1. 先登录微信公众平台进入“公众号设置”的“功能设置”里填写“JS接口安全域名”。

### 2. 在分享的页面中添加js文件
  <script src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>

### 3、配置wxShare.js


### 4、组装微信的配置信息wxShare_data.js

##### 4.1 分享流程：

    用户创建时间戳，随机字符串，当前需要分享的页面的url三个变量，接着将自己的appid和APPsecret作为请求参数获取access_token，再根据access_token获取jsapi_ticket,  然后将获取的jsapi_ticket，以及自己创建的三个变量进行签名，注意签名过程案按照 key 值 ASCII 码升序排序，具体参加程序，

##### 4.2 请求后的响应程序无法处理 问题

    get_access_token（）函数中对微信发起获取access_token的请求，存在跨域问题，设置dataType:"jsonp"无法解决，通过浏览器查看请求发现微信相应的数据并没有包装数据，猜测微信不支持这个请求的跨域，因为ajax程序无法通过程序正常获取access_token的值，但可以在浏览器调式获取access_token的值，这个值有7200s，足够去获取jsapi_ticket ，获取jsapi_ticket的请求过程存在同样的问题，因此获取access_token和jsapi_token必须从服务端后端代码。

    这篇文章主要是想用js请求来完成分享的效果属于介绍篇，因而没有开发服务器端请求代码（勿喷），服务器篇代码见后续的应用篇

    那么如何正常才能让程序跑起来，正常的分享页面呢？？

    在wxShare_data.js 代码中，首先发起 wxdata.get_access_token();  注释②③④⑤代码，将浏览器获取的access_token，手动的放到②变量处，


    手动完成了access_token的赋值后，注释①，打开②③，开始  wxdata.get_jsapi_ticket();    注释④⑤处代码
    同样的操作 从浏览器获取 jsapi_ticket值将其赋值给④处变量，注释①③，打开②④⑤处代码，最终代码见wxShare_data.js

### 5、wxShare_sha1.js

    对数据进行签名

### 6、此时页面可以正常运行并完成微信分享了，