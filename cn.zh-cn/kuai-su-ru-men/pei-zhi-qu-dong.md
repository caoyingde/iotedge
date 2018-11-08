# 配置驱动

本章介绍如何创建设备的驱动及联动函数。驱动用于将您的设备连接到边缘网关，实现具体设备通信协议到物模型的转换。联动函数用于关联您的两个设备，用来实现设备联动的业务逻辑。

## 创建设备驱动 <a id="section_inb_mn2_z2b .section"></a>

1. 下载光照传感器设备驱动和灯设备驱动，两个驱动用于您在物联网边缘计算中自定义驱动。
   * [灯设备驱动](http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/Light.zip)
   * [光照传感器设备驱动](http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightSensor.zip)
2. 在[物联网控制台](http://iot.console.aliyun.com/)，选择**边缘管理** &gt; **驱动管理**。
3. 在驱动管理页面，单击**创建驱动**。
4. 创建名称为**sensor\_protocol**的驱动，上传已下载的光照传感器设备驱动文件后单击**确定**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/153931032110348_zh-CN.png)

5. 创建名称为**light\_protocol**的驱动，上传已下载的灯设备驱动文件后单击**确定**。

## 创建设备联动函数 <a id="section_isq_p4m_j2b .section"></a>

1. 下载虚拟设备联动函数。您需要通过光照传感器的数据来控制灯，因此需要下载联动函数。

   [虚拟设备联动函数](http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightMonitor.zip)

2. 登录函数计算控制台。
3. 为设备联动函数创建一个服务。

   其中，**服务名称**必须填写，此处设置为**DeviceScript**，其余参数可根据您的需求设置。

4. 创建服务成功后，在服务概览页面单击**新建函数**。
5. 选择函数模板，此处选择空白函数模板。
6. 选择触发器类型，此处选择不创建触发器，单击**下一步**。
7. 设置设备联动函数的参数。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/15393103217161_zh-CN.png)

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/15393103216836_zh-CN.png)

   其中，

   * **所在服务**：选择已创建的**DeviceScript**服务。
   * **函数名称**：设置为**LightMonitor**。
   * **运行环境**：设置函数的运行环境，此示例中选择**nodejs8**。
   * **代码配置**：选择**代码包上传**，上传已下载的虚拟设备联动函数脚本。
   * 其余参数的值请根据您的需求，参见[函数计算](https://help.aliyun.com/product/50980.html?spm=a2c4g.11186623.2.8.7e6b1617Ezzl6L)设置。

8. 单击**下一步**，进入模板授权管理页面。此处无需设置，单击**下一步**。
9. 确认函数信息，单击**创建**。
10. 创建函数完成后，在线编辑代码，将代码中的设备相关信息，即Light Product Key和Light Device Name，替换为[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/添加设备.md)中创建的灯设备三元组信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/15393103217227_zh-CN.png)

11. 修改参数后单击**保存**。

