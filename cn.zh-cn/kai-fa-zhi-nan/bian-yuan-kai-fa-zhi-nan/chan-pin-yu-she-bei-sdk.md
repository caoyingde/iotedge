# 产品与设备SDK

产品与设备SDK是Link Edge的核心SDK，方便您编写的驱动与边缘计算节点的交互。

## 产品与设备SDK使用说明 <a id="section_fw1_c3s_n2b .section"></a>

使用格式如下：

```text
var linkedge = require('linkedge');
```

## getGroupByEvent <a id="section_vr4_rbf_h2b .section"></a>

**功能介绍**

获取部署至网关的分组对象。您可以通过该分组对象获取设备对象。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| event | Buffer | handler函数返回的Buffer类型的event值。 |

**返回参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| group | Group | 返回的Group对象，您可以从该对象中获取在云中定义的边缘分组中的设备信息。 |

**使用示例**

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
};
```

## publish <a id="section_zr2_fmm_n2b .section"></a>

**功能介绍**

发布消息。您可以通过消息路由，配置该消息流转的目的地。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| topic | String | 消息的主题。-   如果您发送的数据需在边缘流转，则topic命名规则为：支持英文大小写、数字、斜线、下划线和短划线，长度不超过256个字符。 |

* 如果您发送的数据需要上云端，则topic命名规则请参考\[数据格式\(高级版\)\]\(../../../../cn.zh-CN/用户指南/规则引擎/数据格式\(高级版\).md\#\)。

\| \|payload\|String\|发布的消息体，数据内容由您自行决定。\| \|callback\|Function\|[回调函数](chan-pin-yu-she-bei-sdk.md#callback1)。\|

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| status | Boolean | 发布消息的结果。true表示发送成功，false表示发送失败。 |

**返回参数**

无。

**使用示例**

```text
//发送消息
linkedge.publish("/xxx/topic", "{\"payload\" : \" xxx_test\"}",
function(err, status) {
    if (!err && status) {
        log.LOGI(TAG, "sendSignal xxx_topic ok");
    }
});
```

## Group.getDeviceByProductKeyDeviceName <a id="section_rh2_klm_n2b .section"></a>

**功能介绍**

通过设备的ProductKey和DeviceName获取设备对象。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| productKey | String | 设备对应的产品唯一标识符。 |
| deviceName | String | 设备对应的设备名称。 |
| callback | Function | [回调函数](chan-pin-yu-she-bei-sdk.md#callback2)。 |

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| device | Device | 设备对象。 |

**使用示例**

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
    group.getDeviceByProductKeyDeviceName("a1lDXTP1NPK", "myDeviceName", function(err, device) {
        if(err){
        // 发生错误的逻辑            
        }else{
        // 未发生错误的逻辑            
        }
    });
};
```

## Group.getDevicesByProductKey <a id="section_mcx_wlm_n2b .section"></a>

**功能介绍**

通过设备的ProductCode获取设备列表。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| productKey | String | 设备对应的产品唯一标识符。 |
| callback | Function | [回调函数](chan-pin-yu-she-bei-sdk.md#callback3)。 |

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| deviceList | Map | 设备列表。 |

**使用示例**

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
    group.getDevicesByProductKey("a1lDXTP1NPK", function(err, device) {
        if(err){
        // 发生错误的逻辑            
        }else{
        // 未发生错误的逻辑            
        }
    });
};
```

## Device.get <a id="section_uv2_dmm_n2b .section"></a>

**功能介绍**

通过属性名称获取设备属性内容。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| key | String | 属性名称。 |
| callback | Function | [回调函数](chan-pin-yu-she-bei-sdk.md#callback4)。 |

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| value | Object | 根据您定义的产品属性值类型返回。 |

**使用示例**

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
    group.getDeviceByProductKeyDeviceName("a1lDXTP1NPK", "myDeviceName", function(err, device) {
        if(err){
        // 发生错误的逻辑            
        }else{
        // 未发生错误的逻辑  
        device.get("temperature",function(err, value){ 
            var value = value});          
        }
    });};
```

## Device.set <a id="section_uqz_2mm_n2b .section"></a>

**功能介绍**

设置设备属性。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| key | String | 属性名称。 |
| value | Object | 根据您定义的产品属性值类型确定Object具体类型。 |
| callback | Function | [回调函数](chan-pin-yu-she-bei-sdk.md#callback5)。 |

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| status | Boolean | 设置属性结果。true表示设置成功，false表示设置失败。 |

**使用示例**

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
    group.getDeviceByProductKeyDeviceName("a1lDXTP1NPK", "myDeviceName", function(err, device) {
        if(err){
        // 发生错误的逻辑            
        }else{
            // 未发生错误的逻辑  
            device.set("temperature",12,function(err, status){ 
                // 如果需要获取结果可以通过status进行判断}
                );          
        }
    });};
```

## Device.${method} <a id="section_bzc_fmm_n2b .section"></a>

**功能介绍**

调用设备服务。

**请求参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| intputParam1 | Object | 根据您定义的产品的服务入参类型决定 |
| intputParam2 | Object | 根据您定义的产品的服务入参类型决定 |
| …… | Object | 请求参数个数由您的定义决定。 |
| callback | Function | [回调函数](chan-pin-yu-she-bei-sdk.md#callback6)。 |

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| value | Object | 服务返回参数。 |

**使用示例**

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
    group.getDeviceByProductKeyDeviceName("a1lDXTP1NPK", "myDeviceName", function(err, device) {
        if(err){
        // 发生错误的逻辑            
        }else{
            // 未发生错误的逻辑  
            // 假设您定义的函数名称为open，无参数
            device.open(function(err, value){ 
              var outputParam = value
            });  
        }
    });};
```

