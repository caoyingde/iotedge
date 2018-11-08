# 消息路由设置示例

一个边缘实例可以设置一个或多个消息路由路径。本节将以示例来展示Link IoT Edge支持的五种消息路由路径的设置方法和消息查看方法。

## 消息路由路径：从设备路由到 IoT Hub <a id="section_cv5_sp4_f2b .section"></a>

将设备的属性或全部消息（属性和事件）上报至云端（IoT Hub）。

下图示例表示 device03 设备的属性及事件信息会上报到云端，并且在断网后设备数据无法上报到云端时，Link IoT Edge会将这些数据存储到本地，在恢复网络后把本地数据重新传到云端。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15106/15408908686548_zh-CN.png)

**查看消息**：通过消息主题过滤后的设备数据发送到云端后，您便可以在物联网平台控制台，该子设备所属产品的日志服务页面查看设备上报的数据。

## 消息路由路径：从设备路由到函数计算 <a id="section_mz1_5p4_f2b .section"></a>

将设备的属性或全部消息（属性和事件）发送至边缘函数计算中。

下图中的示例表示：将device03设备的属性信息发送到指定的olin\_service\_test/fc\_driver函数中。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15106/15408908686549_zh-CN.png)

**查看消息**：目前，由于路由到函数计算的消息未上报云端，所以只能在网关本地日志中查看。用 tail命令查看网关本地日志。命令格式：`tail -f /linkedge/run/logger/{module name}/log.INFO`。其中，变量{module name}需填写您实际的模块名称。示例：`tail -f /linkedge/run/logger/function-compute/log.INFO`，`function-compute`为函数计算的模块名。

## 消息路由路径：从函数计算路由到 IoT Hub <a id="section_j5r_5p4_f2b .section"></a>

将函数计算中的数据发送到云端。

下图中的示例表示：olin\_service\_test/fc\_driver函数过滤出符合 `/productkey/devicename/user/#`的 消息主题，并将该消息主题中的消息发送给云端，当网络故障后，Link IoT Edge将olin\_service\_test/fc\_driver函数无法上报的消息存储到本地，并在网络恢复后将本地数据重新上报到云端。

**说明：** `/productkey/devicename/user/#`是您自定义的一个发送消息到云端（IoT Hub）的 消息主题。具体设置方法请参考[自定义Topic](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/Topic/自定义Topic.md)。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15106/15408908686550_zh-CN.png)

**查看消息**：函数计算的数据上报到云端后，您可以在物联网平台控制台中，实例网关设备所属产品的日志服务页面查看上报的数据。

## 消息路由路径：从函数A路由到函数B <a id="section_h34_13d_n2b .section"></a>

将函数A的数据发送到函数B中。

下图中的示例表示：函数A过滤出符合 `/xxxx` 的 消息主题 ，并将该消息主题中的消息发送给函数B。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15303/15408908697268_zh-CN.png)

**查看消息**：路由到函数计算的数据只能在网关设备本地日志中查看。具体方法，请参见本文档消息路由路径：从设备路由到函数计算章节中，查看消息日志的方法。

## 消息路由路径：从IoT Hub路由到函数计算 <a id="section_rwx_ypk_x2b .section"></a>

云端发送消息至函数计算中。

下图中的示例表示：IoT Hub滤条出符合 `/productkey/devicename/user/#`的消息主题，并将此消息主题中的消息发送给函数计算。

**说明：** 云端发送给边缘端的消息，使用的消息主题是以`/${ProductKey}/${DeviceName}/user`为前缀 的。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15303/154089086910113_zh-CN.png)

**查看消息**：路由到函数计算的数据只能在网关设备本地日志中查看。具体方法，请参见本文档消息路由路径：从设备路由到函数计算章节中，查看消息日志的方法。

