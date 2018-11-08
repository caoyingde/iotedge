# 配置联动函数

本章介绍如何创建设备的联动函数。联动函数用于关联您的两个设备，用来实现设备联动的业务逻辑。

## 创建联动函数 <a id="section_nqc_lcn_qfb .section"></a>

1. 下载虚拟设备联动函数。您需要通过光照传感器的数据来控制灯，因此需要下载联动函数。

   [虚拟设备联动函数](http://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightMonitor.zip)

2. 登录函数计算控制台。
3. 为设备联动函数创建一个服务。

   其中，**服务名称**必须填写，此处设置为**DeviceScript**，其余参数可根据您的需求设置。

4. 创建服务成功后，在服务概览页面单击**新建函数**。
5. 选择函数模板，此处选择空白函数模板。
6. 选择触发器类型，此处选择不创建触发器，单击**下一步**。
7. 设置设备联动函数的参数。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/15411283877161_zh-CN.png)

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/15411283876836_zh-CN.png)

   | 参数 | 描述 |
   | :--- | :--- |
   | 所在服务 | 选择已创建的**DeviceScript**服务。 |
   | 函数名称 | 设置为**LightMonitor**。 |
   | 运行环境 | 设置函数的运行环境，此示例中选择**nodejs8**。 |
   | 代码配置 | 选择**代码包上传**，上传已下载的虚拟设备联动函数脚本。 |

   其余参数的值请根据您的需求，参见[函数计算](https://help.aliyun.com/product/50980.html?spm=a2c4g.11186623.2.8.7e6b1617Ezzl6L)设置。

8. 单击**下一步**，进入模板授权管理页面。此处无需设置，单击**下一步**。
9. 确认函数信息后，单击**创建**。
10. 创建函数完成后，在线编辑代码，将代码中的设备相关信息，即Light Product Key和Light Device Name，替换为[管理边缘实例](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/管理边缘实例.md)中创建的客厅灯产品下Light设备的三元组信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/15411283877227_zh-CN.png)

11. 修改参数后单击**保存**。

## 分配联动函数到边缘实例 <a id="section_uvh_z3n_y2b .section"></a>

1. 在[物联网控制台](http://iot.console.aliyun.com/)，选择**边缘计算** &gt; **边缘实例**。
2. 单击myhome实例右侧的**查看**。
3. 在实例详情页面，选择**函数计算**，单击**分配函数**。
4. 在分配函数页面中，将[创建联动函数](pei-zhi-lian-dong-han-shu.md#section_nqc_lcn_qfb)中创建的LightMonitor函数分配到边缘实例中。

| 参数 | 描述 |
| :--- | :--- |
| 地域 | 选择您创建的服务所在的地域。 |
| 服务 | 选择**DeviceScript**服务。 |
| 函数 | 选择**LightMonitor**函数。 |
| 授权 | 选择**AliyunIOTAccessingFCRole**。 |

1. 单击**分配**。
2. 配置函数。

   | 参数 | 描述 |
   | :--- | :--- |
   | 运行模式 | 运行模式有两种。此处选择按需运行模式。 |
   | 内存限制 | 函数运行所需的内存资源，单位为MB。此处设置为50MB。 |
   | 超时限制 | 选择按需运行模式后需设置按需运行函数运行时间，时间到了FC进程将会退出。此处设置300秒。 |

3. 单击**确定**，至此您已将联动函数分配到边缘实例中。

## 分配消息路由到边缘实例 <a id="section_jrn_jdl_j2b .section"></a>

1. 在实例详情页面，选择消息路由，单击**添加路由**。
2. 在添加消息路由页面中，配置参数，此处配置的参数是将设备数据发送至云。
   * **消息来源**：此处选择**设备**，选择**全部产品**。
   * **消息主题过滤**：此处选择**全部**。
   * **消息目标**：此处选择**IoT Hub**。

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15411283876771_zh-CN.png)
3. 在添加消息路由页面中，配置参数，此处配置的参数是将光照传感器数据发送至函数中。
   * **消息来源**：此处选择**设备**，选择**光照传感器** &gt; **LightSensor**。
   * **TopicFilter**：此处选择**全部**。
   * **消息目标**：此处选择**函数计算**和**DeviceScript/LightMoniter**。
4. 单击**确定**，至此您已为实例添加了消息路由。

