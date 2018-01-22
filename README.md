
#APICloud阿里推送模块文档

项目地址:ssh://git@code.blog-mine.com:8082/~wuyuming/apicloud-alipush.git

***配置***<br /> 
在config.xml加入模块配置参数
```html
<feature name="aliPush">
  <param name="AppKey" value="24772250"/>
  <param name="AppSecret" value="fbb19cf90e87cfd2fd6afde385e10207"/>
 </feature>
 AppKey:注册阿里推送应用的key
 AppSecret:注册阿里推送应用的AppSecret
 [网址](https://www.aliyun.com)
```



##1.registerSdk
*注册阿里推送是否成功 
```html
registerSdk(callback(ret, err))<br /> 
ret：<br /> 
类型：JSON对象<br/> 
内部字段：<br /> 
{
    status: true   //布尔型；true
}
err：

类型：JSON对象
内部字段：
{
    status: false   //布尔型；false
}
```
####示例代码
```javascript 
var obj = api.require('aliPush');
obj.registerSdk(function(ret,err) {
    
  alert(JSON.stringify(ret))
})
```
##2. api.addEventListener
*拦截通知，接收消息，获取推送中的扩展字段
 
```html
addEventListener({params}, callback(ret, err))
params

1
name：'onMessage'

类型：字符串
描述：（可选项）用于接收服务端推送的消息（控制台选择推送消息，则不会触发弹窗，而会回调该方法。反之，推送通知不会触发该方法。）。
2
name：'onNotification'

类型：字符串
描述：（可选项）用于在接收通知后，用户需要自定义操作的场景，或者用于获取扩展字段。 
3
name：'notificationClick'

类型：字符串
描述：（可选项）在用户打开（某个）notification的时候，会回调该方法。

callback(ret, err)
ret：

类型：JSON对象
内部字段：
{
"status":"true",//布尔型；true||false
"title":"",标题
"summary":"",内容
"userinfo"://扩展字段，以json字段形式表示
}

```
####示例代码
```javascript 
    api.addEventListener({name: 'onMessage'},
            function (ret, err) {
                alert("onMessage>>>addEventListener>>>>" + JSON.stringify(ret));
            });
})
```
####示例代码
```javascript 
registerSdk(function(ret,err) {
    
  alert(JSON.stringify(ret))
})
```
##3. bindTag
*客户端自定义标签
 
```html
bindTag({params}, callback(ret, err))
params

target：

类型：数字型
描述：（可选项）目标类型，1：本设备； 2：本设备绑定账号； 3：别名。
默认值：1
tag：

类型：字符串
描述：（可选项）标签名，支持多个标签，用空格隔开。
alias：

类型：字符串
描述：（可选项）别名（仅当target = 3时生效）。
callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    errorCode: "",
    errorMessage:""
}

```
####示例代码
```javascript 
    var obj = api.require('aliPush');
    obj.bindTag({
        target : 1,
        tag : "apicloud1 apicloud2",
        alias : ''
    },
    function(ret, err) {
        alert(JSON.stringify(ret));
    });
})
```
##4. unbindTag
*移除客户端自定义标签
 
```html
unbindTag({params}, callback(ret, err))

params

target：

类型：数字型
描述：（可选项）移除目标类型，1：本设备； 2：本设备绑定账号； 3：别名。
默认值：3
tag：

类型：字符串
描述：（可选项）移除标签名，支持多个标签，用空格隔开。
alias：

类型：字符串
描述：（可选项）移除别名（仅当target = 3时生效）。
callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    errorCode: "",
    errorMessage:""
}
```
####示例代码
```javascript 
    var obj = api.require('aliPush');
    obj.unbindTag({
        target : 1,
        tag : "apicloud1 apicloud2",
        alias : ''
    },
    function(ret, err) {
        alert(JSON.stringify(ret));
    });
})
```
##5. getDeviceId
*获取设备DeviceId
 
```html
getDeviceId(callback(ret, err))

callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true
    DeviceId : ''   //设备ID
}
```
####示例代码
```javascript 
    var demo = api.require('aliPush');
    demo.getDeviceId(function(ret) {
        alert(JSON.stringify(ret));
    });
})
```     
##6. unbindAccount
*解绑和指定账号的本设备的绑定
 
```html
unbindAccount(callback(ret, err))

callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    errorCode: "",
    errorMessage:""
}
```
####示例代码
```javascript 
    var obj = api.require('aliPush');
    obj.unbindAccount(function(ret, err) {
        alert(JSON.stringify(ret));
    });
})
```    

##7. bindAccount
*将本设备和指定账号做绑定
 
```html
bindAccount({params}, callback(ret, err))

params

account：

类型：字符串
描述：（必填项）账号名称。
callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    errorCode: "",
    errorMessage:""
}
```
####示例代码
```javascript 
   
var obj = api.require('aliPush');
obj.bindAccount({
    account: "apicloud"
},
function(ret, err) {
    alert(JSON.stringify(ret));
});
```     
##8. listAliases
*查询设备别名
 
```html
listAliases(callback(ret, err))

callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    msg: ""
}}
```
####示例代码
```javascript 
   var demo = api.require('aliPush');
   demo.listAliases(function(ret, err) {
       alert(JSON.stringify(ret));
   });

```     
##9. removeAlias
*删除设备别名；
 
```html
removeAlias({params}, callback(ret, err))

params

alias：

类型：字符串
描述：（可选项）移除别名（为空则删除全部别名）。
callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    errorCode: "",
    errorMessage:""
}
```
####示例代码
```javascript 
  
var obj = api.require('aliPush');
obj.removeAlias({
    alias : ''
},
function(ret, err) {
    alert(JSON.stringify(ret));
});
```    

####示例代码
```javascript 
   var demo = api.require('aliPush');
   demo.listAliases(function(ret, err) {
       alert(JSON.stringify(ret));
   });

```     
##10. addAlias
*添加别名
 
```html
addAlias({params}, callback(ret, err))

params

alias：

类型：字符串
描述：（必填项）别名。
callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    errorCode: "",
    errorMessage:""
}

```
####示例代码
```javascript 

var obj = api.require('aliPush');
obj.addAlias({
    alias : 'test01'
},
function(ret, err) {
    alert(JSON.stringify(ret));
});
```    
##11. listTags
*查询目标绑定标签，当前仅支持查询设备标签；
 
```html
listTags(callback(ret, err))

callback(ret, err)

ret：

类型：JSON对象
内部字段：
{
    status: true,   //布尔型；true||false
    response :     //
}
err：

类型：JSON对象
内部字段：
{
    msg: ""
}
```
####示例代码
```javascript 

var obj = api.require('aliPush');
obj.listTags(function(ret, err) {
        alert(JSON.stringify(ret));
    });
```    

