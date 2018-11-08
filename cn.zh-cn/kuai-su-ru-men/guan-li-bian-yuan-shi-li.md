# 管理边缘实例

本章主要介绍创建边缘实例，为边缘实例分配网关、驱动、设备、函数计算、消息路由的步骤。

## 一、创建边缘实例 <a id="section_i4z_1lf_j2b .section"></a>

1. 在[物联网控制台](http://iot.console.aliyun.com/)，选择**边缘计算** &gt; **边缘实例**。
2. 单击**新增实例**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15414070066752_zh-CN.png)

   * 设置**实例名称**为myhome。
   * 关联**网关产品**和**网关设备**，选择[搭建边缘环境](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/搭建边缘环境.md)中创建的边缘计算节点产品和mygw设备。

3. 单击**确认**，完成边缘实例的创建。

## 二、添加子设备到边缘实例 <a id="section_dtl_tqf_j2b .section"></a>

1. 在边缘实例页面，选择已创建的myhome实例，单击右侧的**查看**。
2. 在实例详情页面，选择子设备，单击**分配子设备**。 1. 在分配子设备页面中，单击**新建子设备**。

   ```text
   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15414070066756_zh-CN.png)
   ```

   1. 在新建子设备页面，单击**新建产品**，创建光照传感器产品。

      ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15414070066838_zh-CN.png)

   2. 在创建产品页面设置参数后，单击**确认**。

      ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/154140700610348_zh-CN.png)

      | 参数 | 描述 |
      | :--- | :--- |
      | 产品名称 | 此处设置为**光照传感器**。 |
      | 设备类型 | 此处选择**光照度传感器**。 |
      | 接入网关协议 | 此处选择**自定义**。 |

   3. 在新建子设备页面，**产品**自动分配已创建的光照传感器产品，**设备名称**输入LightSensor后单击**确认**，为光照传感器添加设备。
   4. 参考创建光照传感器产品及设备的步骤，创建客厅灯产品和设备。

      其中，客厅灯产品参数设置如下：

      | 参数 | 描述 |
      | :--- | :--- |
      | 产品名称 | 设置为**客厅灯**。 |
      | 设备类型 | 此处选择**灯**。 |

      产品设备名称设置为Light。

3. 在分配子设备页面，分别分配光照传感器产品下的LightSensor设备和客厅灯产品下的Light设备到实例中。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/15414070076757_zh-CN.png)

4. 单击**完成**，至此您已为实例分配了两个子设备。
5. 为光照传感器产品和客厅灯产品开启动态注册。

   **说明：** 两个产品都需要开启动态注册。

   1. 选择**设备管理** &gt; **产品**，搜索光照传感器和客厅灯产品。
   2. 单击产品名称后的**查看**。

      ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/154140700710403_zh-CN.png)

   3. 在产品详情页面，单击**动态注册**后的开关，获取验证码，开启产品的动态注册。

      ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/154140700711964_zh-CN.png)

## 三、为子设备分配驱动 <a id="section_bm5_yvm_qfb .section"></a>

LightSensor设备需要关联LightSensor官方示例驱动，Light设备需要关联Light官方示例驱动。

1. 选择**边缘计算** &gt; **边缘实例**，单击已创建的myhome实例右侧的**查看**。
2. 分配官方示例驱动到子设备前，在实例详情页面，选择**子设备通信通道** &gt; **自定义**，单击**添加自定义通道**，为设备和驱动的交互创建通道。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/154140700711583_zh-CN.png)

   | 参数 | 描述 |
   | :--- | :--- |
   | 通道名称 | 为自定义通道命名，LightSensor示例驱动的通道命名为For\_LightSensor，Light示例驱动的通道命名为For\_Light。 |
   | 自定义配置 | 此处请配置为`{}`。 |

3. 选择子设备，单击已分配的子设备右侧的**驱动配置**，为设备分配LightSensor官方示例驱动和Light官方示例驱动。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15291/154140700710402_zh-CN.png)

   | 参数 | 描述 |
   | :--- | :--- |
   | 选择驱动 | 客厅灯设备选择**light\_protocol**驱动，光照传感器设备选择**sensor\_protocol**驱动。 |
   | 选择通道 | LightSensor设备关联**For-LightSensor**通道，Light设备关联**For-Light**通道。 |
   | 内存限制 | 设置为100MB。 |

4. 单击**确定**，您已成功为设备配置了驱动。

