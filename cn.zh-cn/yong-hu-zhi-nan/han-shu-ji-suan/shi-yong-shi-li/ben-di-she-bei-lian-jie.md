# 本地设备连接

通过函数计算可实现设备连接网关。设备连接网关的API，请参见[设备接入开发](../../../kai-fa-zhi-nan/bian-yuan-kai-fa-zhi-nan/she-bei-jie-ru-kai-fa/she-bei-jie-ru-kai-fa-zong-he-shi-li.md)。

以定义光照传感器数据发送至云端为例。

1. 在[物联网控制台](https://iot.console.aliyun.com/)创建名称为光照感应器的高级版产品和设备。具体操作，可参考[高级版创建产品与设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/创建产品与设备/高级版/创建产品.md)。

   * 产品**节点类型**选择为**设备**。
   * 产品**设备类型**选择为**光照度传感器**。
   * 产品**数据格式**选择为**Alink JSON**。
   * 设备创建成功后，获取设备三元组：ProductKey、DeviceName、和DeviceSecret。编写函数代码时，将需填入设备的ProductKey和DeviceName信息。

     ![&#x521B;&#x5EFA;&#x4EA7;&#x54C1;](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/函数计算/使用示例/images/6951_zh-CN.png)

   ![&#x521B;&#x5EFA;&#x8BBE;&#x5907;](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/函数计算/使用示例/images/6953_zh-CN.png)

2. 编写设备接入函数的代码，然后将函数代码的内容压缩为一个zip包（需确保index.js在顶级目录下）。

   以下是函数的代码示例。本示例中`productKey: 'Your Product Key',deviceName: 'Your Device Name'`内容需替换成具体设备的ProductKey和DeviceName。示例代码中没有定义连接具体设备，而是将如何实现设备连接类的代码做了描述。

   \`\`\`

```text
/*
* Copyright (c) 2018 Alibaba Group Holding Ltd.
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/
'use strict';


const {
RESULT_SUCCESS,
RESULT_FAILURE,
ThingAccessClient,
} = require('linkedge-thing-access-sdk');


var configs = [
{
productKey: 'Your Product Key',
deviceName: 'Your Device Name'
},
];
var args = configs.map((config) => {
var self = {
lightSensor: {
illuminance: 100,
},
config,
callbacks: {
setProperties: function (properties) {
console.log('Set properties %s to thing %s-%s', JSON.stringify(properties),
config.productKey, config.deviceName);
return {
code: RESULT_FAILURE,
message: 'The property is read-only.',
};
},
getProperties: function (keys) {
console.log('Get properties %s from thing %s-%s', JSON.stringify(keys),
config.productKey, config.deviceName);
if (keys.includes('MeasuredIlluminance')) {
return {
code: RESULT_SUCCESS,
message: 'success',
params: {
'MeasuredIlluminance': self.lightSensor.illuminance,
}
};
}
return {
code: RESULT_FAILURE,
message: 'The requested properties does not exist.',
}
},
callService: function (name, args) {
console.log('Call service %s with %s on thing %s-%s', JSON.stringify(name),
JSON.stringify(args), config.productKey, config.deviceName);
return {
code: RESULT_FAILURE,
message: 'The requested service does not exist.',
};
}
},
};
return self;
});
args.forEach((item) => {
var client = new ThingAccessClient(item.config, item.callbacks);
client.setup()
.then(() => {
return client.registerAndOnline();
})
.then(() => {
// Push events and properties to LinkEdge platform.
return new Promise(() => {
setInterval(() => {
if (item.lightSensor.illuminance >= 600) {
item.lightSensor.illuminance = 100;
} else {
item.lightSensor.illuminance += 100;
}
var properties = {'MeasuredIlluminance': item.lightSensor.illuminance};
console.log(`Report properties: ${JSON.stringify(properties)}`);
client.reportProperties(properties);
}, 2000);
});
})
.catch(err => {
console.log(err);
client.cleanup();
})
.catch(err => {
console.log(err);
});
});


module.exports.handler = function (event, context, callback) {
console.log(event);
console.log(context);
callback(null);
};




```
```

1. 在[函数计算控制台](https://fc.console.aliyun.com/)创建函数计算的服务和函数。 
   * **函数名称**可填写为**LightSensor**。
   * **运行环境**选择为**nodejs8**。
   * **代码上传方式**选择为**代码包上传**，并上传已压缩好的zip代码包。
   * **函数入口**栏填写**index.handler**。
2. 在物联网平台控制台，创建一个边缘分组，并配置分组内容。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15398/6955_zh-CN.png)

   1. 在分组详情页面，为该分组配置**网关**、**设备**。 
      * 网关：选择[配置边缘计算节点](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/函数计算/使用示例/cn.zh-CN/用户指南/配置边缘计算节点.md)中创建的网关。
      * 设备：选择第一步中创建的光照传感器产品下的所有设备。
   2. 为该分组配置**函数计算**和**消息路由**。 
      * 函数：选择第三步中创建的函数LightSensor。函数运行模式选择为**持续运行**。
      * 消息路由设置：
        * **消息来源**：光照传感器产品下的全部设备。
        * **TopicFilter**：全部。
        * **消息目标**：IoT Hub。

3. 单击分组详情页面右上角**部署分组**，将已分配到分组的资源部署至网关中。 

部署成功后，设备上报的属性和事件将会每隔2秒被同步到云端，您可以在IoT控制台设备运行状态页面查看具体信息。

