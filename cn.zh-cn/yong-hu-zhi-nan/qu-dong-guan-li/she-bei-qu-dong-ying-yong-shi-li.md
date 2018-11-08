# 设备驱动应用示例

本节为您介绍本地设备连接方法，通过设备驱动可实现设备连接网关。设备连接网关的API，请参见[设备接入开发](../../bian-yuan-kai-fa-zhi-nan/she-bei-jie-ru-sdk-zong-he-shi-li.md)。

您需要准备一个驱动文件。建议您按照[开发指南](../../bian-yuan-kai-fa-zhi-nan/she-bei-jie-ru-sdk-zong-he-shi-li.md)中的方式开发驱动文件，并确保该驱动文件的正确性和可用性。

以定义光照传感器数据发送至云端为例。

1. 在物联网平台控制台，选择**边缘计算** &gt; **驱动管理** 
2. 在驱动管理页面，单击**新建驱动**，创建驱动。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15398/154103555813066_zh-CN.png)

   | 参数 | 描述 |
   | :--- | :--- |
   | 语言类型 | 选择驱动的语言类型，可以选择**nodejs8**。 |
   | 驱动名称 | 可填写为**Light\_Sensor**。 |
   | 驱动描述 | 描述将要创建的驱动，可以为空。 |
   | 驱动文件 | 上传提前准备的驱动文件。 |

3. 在边缘实例页面创建一个边缘实例，关联[控制台创建网关](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/驱动管理/cn.zh-CN/用户指南/配置边缘计算节点/控制台创建网关.md)中创建的网关，并配置实例内容。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15398/15410355586955_zh-CN.png)

   1. 在**实例详情** &gt; **子设备**页面，单击**分配子设备**。 
   2. 在分配子设备页面，单击**新建子设备**。

      ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15398/154103555821102_zh-CN.png)

   3. 单击**新建产品**，创建名称为光照传感器的高级版产品。
   4. 设置产品参数后单击确认。 
   5. 在新建子设备页面，设置设备名称，单击**确认**完成子设备的创建。 
   6. 分配上一步创建的子设备到边缘实例中。 
   7. 为子设备配置步骤2中创建的Light\_Sensor驱动。

      ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15398/15410355586954_zh-CN.png)

4. 单击实例详情页面右上角**部署**，将已分配到实例的资源部署至网关中。

部署成功后，设备上报的属性和事件将会每隔2秒被同步到云端，您可以在IoT控制台设备运行状态页面查看具体信息。

