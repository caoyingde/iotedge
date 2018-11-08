# Device.get

## 功能介绍 <a id="section_w2b_wdf_h2b .section"></a>

通过属性名称获取设备属性内容。

## 请求参数 <a id="section_rmt_mjp_32b .section"></a>

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| key | String | 属性名称。 |
| callback | Function | [回调函数](device.get.md#callback4)。 |

**回调参数**

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| err | Error | 错误对象，当有错误时Error非空。 |
| value | Object | 根据您定义的产品属性值类型返回。 |

## 使用示例 <a id="section_ujk_pjp_32b .section"></a>

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

