# 创建驱动函数及联动函数

本章介绍如何创建连接设备的函数，并将设备的驱动函数和联动函数上传至[函数计算控制台](https://fc.console.aliyun.com/overview/cn-shanghai)。关于边缘部分函数计算的说明请参见[边缘部分函数计算](../yong-hu-zhi-nan/han-shu-ji-suan/bian-yuan-bu-fen-han-shu-ji-suan.md)。这里，我们将为您提供两个虚拟设备，请将两个设备的驱动函数和联动函数上传至函数计算控制台。

## 创建设备驱动函数 <a id="section_idj_mfn_m2b .section"></a>

设备的驱动函数有两个，分别为光照传感器设备驱动函数和灯设备驱动函数。您需要将两个驱动函数全部上传到函数计算控制台。

**光照传感器设备驱动函数**

1. 下载光照传感器设备驱动函数，该驱动函数用于您在函数计算平台中管理光照传感器设备。

   [光照传感器设备驱动函数](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightSensor.zip)

2. 登录函数计算控制台。
3. 为光照传感器设备的函数创建一个服务。

   其中，服务名称必须填写，此处设置为DeviceScript，其余参数可根据您的需求设置。

4. 创建服务成功后，在服务概览页面单击**新建函数**。
5. 选择函数模板，此处选择空白函数模板。
6. 选择触发器类型，此处选择不创建触发器，单击**下一步**。
7. 设置设备驱动函数的参数。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/6835_zh-CN.png)

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/6836_zh-CN.png)

   其中，

   所在服务：选择[3](chuang-jian-qu-dong-han-shu-ji-lian-dong-han-shu.md#step1-3)中创建的服务。

   函数名称：设置您的函数名称，此处设置为LightSensor。

   运行环境：设置函数运行的环境，此示例中选择nodejs8。

   代码配置：选择代码包上传，上传[1](chuang-jian-qu-dong-han-shu-ji-lian-dong-han-shu.md#step1-1)中下载的光照传感器设备驱动函数脚本。

   其余参数的值请根据您的需求，参见[函数计算](https://help.aliyun.com/product/50980.html?spm=a2c4g.11186623.3.1.lo2iWt)设置。

8. 单击**下一步**，进入模板授权管理页面。此处无需设置，单击**下一步**。
9. 确认函数信息，单击**创建**。
10. 创建函数完成后，在线编辑代码，将代码中的设备相关信息，即productKey和deviceName参数的值替换为[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/添加设备.md)中创建的光照传感器设备三元组信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/7222_zh-CN.png)

11. 修改参数后单击**保存**。

**灯设备驱动函数**

1. 下载灯设备驱动函数，该驱动函数用于您在函数计算平台中管理灯设备。

   [灯设备驱动函数](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/Light.zip)

2. 登录函数计算控制台。
3. 单击DeviceScript服务，进入服务概览页面。
4. 在服务概览页面单击**新建函数**。
5. 选择函数模板，此处选择空白函数模板。
6. 选择触发器类型，此处选择不创建触发器，单击**下一步**。
7. 设置设备驱动函数的参数。

   其中，

   * 函数名称：设置为Light。
   * 代码配置：选择代码包上传，上传已下载的灯设备驱动函数脚本。
   * 其余参数请与[7](chuang-jian-qu-dong-han-shu-ji-lian-dong-han-shu.md#step1_7)参数设置保持一致。

8. 单击**下一步**，进入模板授权管理页面。此处无需设置，单击**下一步**。
9. 确认函数信息，单击**创建**。
10. 创建函数完成后，在线编辑代码，将代码中的设备相关信息，即productKey和deviceName参数的值替换为[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/添加设备.md)中创建的灯设备三元组信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/7224_zh-CN.png)

11. 修改参数后单击**保存**。

## 创建设备联动函数 <a id="section_isq_p4m_j2b .section"></a>

1. 下载虚拟设备联动函数。您需要通过光照传感器的数据来控制灯，因此需要下载联动函数。
   * [虚拟设备联动函数](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightMonitor.zip)
2. 登录函数计算控制台。
3. 单击DeviceScript服务，进入服务概览页面。
4. 在服务概览页面单击**新建函数**。
5. 选择函数模板，此处选择空白函数模板。
6. 设置设备联动函数的参数。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/7161_zh-CN.png)

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/6836_zh-CN.png)

   其中，

   * 函数名称：设置为LightMonitor。
   * 代码配置：选择代码包上传，上传已下载的虚拟设备联动函数脚本。
   * 其余参数请与[7](chuang-jian-qu-dong-han-shu-ji-lian-dong-han-shu.md#step1_7)参数设置保持一致。

7. 单击**下一步**，进入模板授权管理页面。此处无需设置，单击**下一步**。
8. 确认函数信息，单击**创建**。
9. 创建函数完成后，在线编辑代码，将代码中的设备相关信息，即Light Product Key和Light Device Name，替换为[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/cn.zh-CN/快速入门/添加设备.md)中创建的灯设备三元组信息。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/7227_zh-CN.png)

10. 修改参数后单击**保存**。

