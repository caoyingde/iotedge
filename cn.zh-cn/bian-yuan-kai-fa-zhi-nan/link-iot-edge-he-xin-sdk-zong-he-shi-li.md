# Link IoT Edge核心SDK综合示例

本文展示使用Link IoT Edge核心SDK控制灯设备的操作代码。示例中，当光照传感器上报的光照度超过500时关闭灯，光照度不足100时打开灯。

## Node.js版本综合示例 <a id="section_fvm_xdf_h2b .section"></a>

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

/*
 * The example demonstrates closing a light when it monitor the illuminance
 * reported by a light sensor is greater than 500.
 */

'use strict';

const leSdk = require('linkedge-core-sdk');

const iotData = new leSdk.IoTData();

const productKey = 'Light Product Key';
const deviceName = 'Light Device Name';

module.exports.handler = function (event, context, callback) {

  console.log(`LightMonitor is invoking with ${event.toString()}.`);

  var illuminance;
  try {
    var obj = JSON.parse(event.toString());
    if (!obj.payload) {
      callback(new Error(`Can't find "payload" in event.`));
      return;
    }
    var payload = JSON.parse(obj.payload);
    if (!payload['MeasuredIlluminance']) {
      callback(new Error(`Can't find "MeasuredIlluminance" in event.`));
      return;
    }
    illuminance = payload['MeasuredIlluminance'].value || 0;
  } catch (err) {
    err = new Error(`Parse event failed due to ${err}.`);
    callback(err);
    return;
  }

  if (illuminance > 500) {
    turnOff(callback);
  } else if (illuminance <= 100) {
    turnOn(callback);
  } else {
    console.log(`Illuminance value is ${illuminance}, ignore.`);
    callback(null);
  }
};

function turnOff(callback) {
  // Turn off the light according to product key and device name.
  iotData.setThingProperties({
    productKey,
    deviceName,
    payload: {'LightSwitch': 0},
  }, function (err) {
    if (err) {
      console.log(`Failed to turn off the light due to ${err}.`);
      callback(err);
    } else {
      console.log(`Turns off light successfully.`);
      callback(null);
    }
  });
}

function turnOn(callback) {
  // Turn on the light according to product key and device name.
  iotData.setThingProperties({
    productKey,
    deviceName,
    payload: {'LightSwitch': 1},
  }, function (err) {
    if (err) {
      console.log(`Failed to turn on the light due to ${err}.`);
      callback(err);
    } else {
      console.log(`Turns on light successfully.`);
      callback(null);
    }
  });
}
```

## Python版本综合示例 <a id="section_khp_3hd_lfb .section"></a>

```text
# -*- coding: utf-8 -*-
import lecoresdk
import json


ON = 1
OFF = 0

def light_turn(status):
  it = lecoresdk.IoTData()
  set_params = {"productKey": "Light Product Key",
                           "deviceName": "Light Device Name",
                           "payload": {"LightSwitch":status}}
  res = it.setThingProperties(set_params)

def handler(event, context):
  event_json = json.loads(event.decode("utf-8"))
  if "payload" in event_json:
    payload_json = json.loads(event_json["payload"])
    if "illuminance" in payload_json and "value" in payload_json["illuminance"]:
       illuminance = payload_json["illuminance"]["value"]
       if illuminance > 500:
          light_turn(OFF)
       elif illuminance <= 100:
          light_turn(ON)
  return 'hello world'
```

