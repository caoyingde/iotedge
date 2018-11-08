# 边缘实例规则计算

使用边缘实例规则计算需为边缘实例添加和部署规则。部署至边缘实例的规则能够快速响应本地的消息，并且可在断网环境下正常运行。

## 为实例配置规则计算 <a id="section_x4d_1fy_32b .section"></a>

为边缘实例部署规则之前，需先创建规则和边缘实例。规则的创建方法，请参见[云端管理规则计算](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/规则计算/cn.zh-CN/用户指南/规则计算/云端管理规则计算.md)。

规则计算部署步骤：

1. 登录[物联网平台控制台](http://iot.console.aliyun.com)。
2. 单击左侧导航栏中**边缘计算** &gt; **边缘实例**。
3. 找到要添加规则的实例，单击对应操作栏中的**查看**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154106341513914_zh-CN.png)

4. 在实例详情页面，选择**规则计算**，然后单击**分配规则**或**分配规则计算**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154106341513915_zh-CN.png)

5. 在弹出的分配规则页面中，选择要分配给实例的规则，单击**分配**。分配成功后，单击**完成**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154106341513916_zh-CN.png)

   完成规则添加后，便可在该实例的实例详情页面上，查看该实例的规则计算信息。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154106341513931_zh-CN.png)

   **说明：** 您可以单击规则右侧的**日志**，快速查询该规则的相关日志。

6. 部署实例。为实例分配规则后，单击页面右上角**部署**，并在弹出对话框中，单击**确认**。

   您可以在本页面中查看部署状态和部署详情。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154106341513936_zh-CN.png)

## 查看实例规则计算日志 <a id="section_k1r_5vw_32b .section"></a>

在物联网平台控制台，查看已同步至云端的日志。

**说明：** 若某条规则既在云端运行又在边缘端运行，那么在物联网平台控制台规则计算中，查看到的日志为云端运行日志和边缘端运行日志。

1. 登录[物联网平台控制台](http://iot.console.aliyun.com)。
2. 单击左侧导航栏中**边缘计算** &gt; **边缘实例**。
3. 找到要查看日志的实例，单击对应操作栏中的**查看**按钮。
4. 在实例详情页面，选择**规则计算**。
5. 单击规则名称对应操作栏中**日志**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154106341513951_zh-CN.png)

6. 在运行日志页面，单击**详情**查看日志详情。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15098/15410634156575_zh-CN.png)

