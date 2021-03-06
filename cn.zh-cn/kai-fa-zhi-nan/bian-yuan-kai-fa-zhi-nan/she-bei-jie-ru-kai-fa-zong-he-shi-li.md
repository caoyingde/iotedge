# 设备接入开发综合示例

本文展示一段使用设备接入SDK，开发驱动的代码片段。设备使用thing标识，拥有一个temperature的只读属性，在连接到边缘计算节点后，每隔2秒向平台上报属性和高温事件。

## 综合示例 <a id="section_wlk_g52_h2b .section"></a>

```text
/*
 * Copyright (c) 2018 Alibaba Group Holding Ltd.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
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
    config,
    thing: {
      temperature: 41,
    },
    callbacks: {
      setProperties: function (properties) {
        // Usually, in this callback we should set properties to the physical thing and
        // return the result. Here we just return a failed result since the properties
        // are read-only.
        console.log('Set properties %s to thing %s-%s', JSON.stringify(properties),
          config.productKey, config.deviceName);
        // Return an object representing the result in the following form or the promise
        // wrapper of the object.
        return {
          code: RESULT_FAILURE,
          message: 'failure',
        };
      },
      getProperties: function (keys) {
        // Usually, in this callback we should get properties from the physical thing and
        // return the result. Here we return the simulated properties.
        console.log('Get properties %s from thing %s-%s', JSON.stringify(keys),
          config.productKey, config.deviceName);
        // Return an object representing the result in the following form or the promise
        // wrapper of the object.
        if (keys.includes('temperature')) {
          return {
            code: RESULT_SUCCESS,
            message: 'success',
            params: {
              temperature: self.thing.temperature,
            }
          };
        }
        return {
          code: RESULT_FAILURE,
          message: 'The requested properties does not exist.',
        }
      },
      callService: function (name, args) {
        // Usually, in this callback we should call services on the physical thing and
        // return the result. Here we just return a failed result since no service
        // provided by the thing.
        console.log('Call service %s with %s on thing %s-%s', JSON.stringify(name),
          JSON.stringify(args), config.productKey, config.deviceName);
        // Return an object representing the result in the following form or the promise
        // wrapper of the object
        return new Promise((resolve) => {
          resolve({
            code: RESULT_FAILURE,
            message: 'The requested service does not exist.',
          })
        });
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
          client.reportEvent('high_temperature', {temperature: 41});
          client.reportProperties({'temperature': item.thing.temperature});
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

