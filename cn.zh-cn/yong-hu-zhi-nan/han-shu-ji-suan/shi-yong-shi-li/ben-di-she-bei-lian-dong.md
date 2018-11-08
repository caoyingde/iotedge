# 本地设备联动

设备数据可通过消息路由能力流转至函数中，您可以通过函数控制其他设备。

以设置当光照指数&gt;500时关闭灯为例。

1. 在[函数计算控制台](https://fc.console.aliyun.com/)创建一个函数。

   函数的代码配置示例如下：

   \`\`\`

   /\*

   * Copyright \(c\) 2018 Alibaba Group Holding Ltd.

     \*

   * Licensed under the Apache License, Version 2.0 \(the "License"\);
   * you may not use this file except in compliance with the License.
   * You may obtain a copy of the License at

     \*

   * [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

     \*

   * Unless required by applicable law or agreed to in writing, software
   * distributed under the License is distributed on an "AS IS" BASIS,
   * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   * See the License for the specific language governing permissions and
   * limitations under the License.

     \*/

     'use strict';

```text
const edge = require('linkedge');


module.exports.handler = function (event, context, callback) {
var obj;
try {
obj = JSON.parse(event.toString());
} catch (err) {
callback(err);
return;
}
if (!obj.topic || !obj.topic.includes('thing/event/property/post')
|| !obj.payload || !obj.payload['MeasuredIlluminance']
|| obj.payload['MeasuredIlluminance'].value <= 500
|| !obj.provider || !obj.provider.groupId) {
callback(null);
return;
}
var group = edge.getGroupById(obj.provider.groupId);
group.getDeviceByProductKeyDeviceName('Light Product Key', 'Light Device Name',
function (err, device) {
if (err) {
callback(err);
return;
}
device.set('LightSwitch', 0, (err => {
if (err) {
callback(err);
return;
}
console.log(`Turn off light successfully!`);
callback(null);
}));
});
};
```
```

1. 在[物联网平台控制台](https://iot.console.aliyun.com/)边缘实例页面中，单击**新增实例**，然后创建一个边缘实例。 
2. 在已创建的边缘实例的实例详情页面，选择**函数计算**，然后为该实例分配第一步中创建的函数。

   **说明：** 为边缘实例配置函数时，选择运行模式为**按需运行**。

