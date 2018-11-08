# 本地数据加工

通过函数计算将设备数据加工后再发送至云端。

在控制台为产品自定义一个Topic，并将该Topic配置到函数代码中，然后可设置通过消息路由将数据发送至云端和通过规则引擎将数据发送至其他阿里云产品。

1. 在[物联网平台控制台](https://iot.console.aliyun.com/)**设备管理** &gt; **产品**页面选中一个产品，单击**查看**。 
2. 在产品详情页面，选择消息通信，为该产品创建自定义Topic，并将**设备操作权限**设置为**发布**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15161/15408907006605_zh-CN.png)
3. 单击**确认**，可在Topic类列表中查看。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15161/15408907006606_zh-CN.png)

4. 通过以下示例代码，在[函数计算控制台](https://fc.console.aliyun.com/)创建一个函数。在函数配置代码中，定义将上一步定义的Topic中的消息发送至云端。

   \`\`\`

   module.exports.handler = function\(event, context, callback\) {

   console.log\('my script is runing ... '\);

   deviceData = JSON.parse\(event\);

```text
const linkedge = require("linkedge"); 

// 定义为将光照指数值除于10后，再上报云端。
deviceData.payload.MeasuredIlluminance.value = deviceData.payload.MeasuredIlluminance.value / 10; 

// 定义通过原topic发送数据，您也可以设置为通过其他topic发送。
linkedge.publish('/a1**********/mygw/user/myselftopic', JSON.stringify(deviceData.payload), function(err, status){
console.log('publish message topic=' + deviceData.topic + ',result=' + status); 
callback(null, 'finish'); 
}); 
}
```
```

1. 在[物联网平台控制台](https://iot.console.aliyun.com/)边缘实例的实例详情页面，选择**消息路由**，并配置消息路由规则，将函数发送的数据路由至IoT Hub。 
2. 在[物联网平台控制台](https://iot.console.aliyun.com/)设置[规则引擎](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/规则引擎/概览.md)，将IoT Hub接收到的数据，转发至阿里云其他产品。 

