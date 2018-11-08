# 管理边缘分组

本章主要介绍创建边缘分组，为边缘分组分配网关、驱动、设备、函数计算、消息路由的步骤。

## 一、创建边缘分组 <a id="section_i4z_1lf_j2b .section"></a>

1. 在[物联网控制台](http://iot.console.aliyun.com/)，选择**边缘管理** &gt; **边缘分组**。
2. 单击**新增分组**。系统显示创建分组页面。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15381278646752_zh-CN.png)

   设置**分组名称**。

3. 单击**确认**，完成边缘分组的创建。

## 二、添加网关到边缘分组 <a id="section_l11_s4f_j2b .section"></a>

1. 在边缘分组页面，选择已创建的分组，单击右侧的**查看**，进入分组详情页面。
2. 选择网关，单击**分配网关**。
3. 在分配网关页面中，选择网关，即[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/添加设备.md)中创建的网关（边缘计算节点设备）。
4. 单击网关右侧的**分配**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15381278646756_zh-CN.png)

5. 单击右下角**完成**，至此您已为边缘分组分配了网关。

## 三、分配驱动到边缘分组 <a id="section_pxc_5h2_z2b .section"></a>

1. 选择设备驱动，单击**分配驱动**。
2. 分配在[创建驱动与联动函数](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/创建驱动与联动函数.md)中创建的**light\_protocol**驱动和**sensor\_protocol**驱动到边缘分组中。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/153812786410402_zh-CN.png)

3. 在驱动配置弹窗中设置**内存限制**为100MB，单击**确认**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/153812786410403_zh-CN.png)

4. 单击右下角**完成**，至此您已为边缘分组分配了驱动。

## 四、添加设备到边缘分组 <a id="section_dtl_tqf_j2b .section"></a>

1. 选择设备，单击**分配设备**。
2. 在分配设备页面中，分别选择[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/添加设备.md)中创建的光照传感器设备和灯设备，单击设备右侧的**分配**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15381278646757_zh-CN.png)

3. 为设备选择驱动，客厅灯设备选择**light\_protocol**驱动，光照传感器设备选择**sensor\_protocol**驱动，单击**确定**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/153812786410405_zh-CN.png)

4. 单击右下角**完成**，至此您已为边缘分组分配了设备。
5. 在**设备管理**页面，单击**边缘计算节点**设备后的**查看**。
6. 在设备详情页面，选择**子设备通道管理** &gt; **自定义**，单击添加自定义通道，为与设备关联的light\_protocol驱动和sensor\_protocol驱动创建通道。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/153812786511583_zh-CN.png)

   其中，

   * **通道名称**：为自定义通道命名，sensor\_protocol驱动的通道命名为For-LightSensor，light\_protocol驱动的通道命名为For-Light。
   * **自定义配置**：此处请配置为`{}`。

7. 在设备详情页面，选择**子设备管理**，单击**添加子设备**，关联网关与设备。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/153812786511964_zh-CN.png)

   其中，

   * **产品**：分别选择**光照传感器**产品和**客厅灯**产品。
   * **设备名**：分别选择**LightSensor**设备和**Light**设备。
   * **关联通道**：LightSensor设备关联**For-LightSensor**通道，Light设备关联**For-Light**通道。
   * **自定义配置**：此处请配置为`{}`。

8. 完成参数配置后，单击**确定**。

## 五、添加函数到边缘分组 <a id="section_uvh_z3n_y2b .section"></a>

1. 选择**函数计算**，单击**分配函数**。
2. 在分配函数页面中，将[创建驱动与联动函数](https://help.aliyun.com/document_detail/85424.html#concept_mwf_clq_32b)中创建的设备联动函数分配到边缘分组中。
3. **地域**：选择您创建的服务所在的地域。
4. **服务**：选择**DeviceScript**服务。
5. **函数**：选择**LightMonitor**函数。
6. **授权**：选择**AliyunIOTAccessingFCRole**。
7. 单击**分配**。
8. 配置函数。
   * **运行模式**：运行模式有两种。此处选择按需运行模式。
   * **内存限制**：函数运行所需的内存资源，单位为MB。此处设置为50MB。
   * **超时限制**：选择按需运行模式后需设置按需运行函数运行时间，时间到了FC进程将会退出。此处设置300秒。
9. 单击**确定**，至此您已添加设备的联动函数至边缘分组。

## 六、添加消息路由到边缘分组 <a id="section_jrn_jdl_j2b .section"></a>

1. 选择消息路由，单击**添加路由**。
2. 在添加消息路由页面中，配置参数，此处配置的参数是将设备数据发送至云。
   * **消息来源**：此处选择**设备**，选择**全部产品**。
   * **TopicFilter**：此处选择**全部**。
   * **消息目标**：此处选择**IoT Hub**。

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15381278656771_zh-CN.png)
3. 在添加消息路由页面中，配置参数，此处配置的参数是将光照传感器数据发送至函数中。
   * **消息来源**：此处选择**设备**，选择**光照传感器** &gt; **LightSensor**。
   * **TopicFilter**：此处选择**全部**。
   * **消息目标**：此处选择**函数计算**和**DeviceScript/LightMoniter**。
4. 单击**确定**，至此您已为分组添加了消息路由。

