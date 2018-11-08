# 控制台创建网关

边缘计算节点，即承载计算能力的边缘网关。配置边缘计算节点包含控制台创建网关和搭建边缘环境两部分内容，本节介绍在控制台创建边缘网关与设备的步骤。

1. 登录物联网平台控制台。 
2. 选择**设备管理** &gt; **产品**、单击**创建产品**。在弹出页面，按如下参数设置说明设置参数后，单击**确认**，创建网关产品。 产品是一批具有相同功能的设备的集合，您可以创建产品，用于批量管理设备。比如，同一产品型号的设备，功能都相同。您可以为该型号创建产品，以此来批量管理设备。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15096/15410573306543_zh-CN.png)

   参数设置说明：

   * 版本选择：选择**高级版**。
   * 产品名称：在此处为产品命名，产品名称需保持账号内唯一。
   * 节点类型：在此处选择产品类型。此例中，选择**网关**。
   * 设备类型：在此处选择**边缘网关**。
   * 数据格式：在此处选择该产品的数据传输格式。边缘网关请选择**Alink JSON**。
   * 使用ID²认证：ID²是物联网平台提供的一种安全认证方式，边缘计算中并不涉及这种认证。此处，请选择**否**。
   * 产品描述：使用文字描述该产品，可为空。

3. 单击设备管理、**添加设备**。按如下参数设置说明设置参数后，单击**确认**，创建一个网关设备。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15096/15410573306544_zh-CN.png)

   参数设置说明：

   * 产品：选择上一步中创建的产品。
   * DeviceName：为该网关设备命名。DeviceName需保持产品内唯一。如不填写，系统将自动生成。

     **说明：** DeviceName支持大写字母\[A-Z\]、小写字母\[a-z\]、数字\[0-9\]和下划线（\_）。且不能以下划线开头或结尾。

4. 网关设备创建完成后，系统会弹出设备证书，即设备三元组（包括ProductKey、DeviceName和DeviceSecret）。您可以**一键复制**并保存这些信息，用于后续设备开发使用。
