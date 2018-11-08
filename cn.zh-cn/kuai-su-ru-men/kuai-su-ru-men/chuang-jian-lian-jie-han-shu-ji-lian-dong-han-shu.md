# 创建连接函数及联动函数

本章介绍如何创建连接设备的函数，并将光照传感器设备的驱动函数和灯设备的驱动函数上传至[函数计算控制台](https://fc.console.aliyun.com/overview/cn-shanghai)。关于边缘部分函数计算的说明请参见[边缘部分函数计算](../../yong-hu-zhi-nan/han-shu-ji-suan/bian-yuan-bu-fen-han-shu-ji-suan.md)。

## 配置设备驱动函数 <a id="section_jnz_p4m_j2b .section"></a>

这里，我们将为您提供两个虚拟设备，请将两个设备驱动函数和联动函数上传至函数计算控制台。

1. 下载虚拟设备驱动函数，两个驱动函数用于您在函数计算平台中管理灯设备和光照传感器设备。
   * [光照传感器设备驱动函数](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightSensor.zip)
   * [灯设备驱动函数](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/Light.zip)
2. 将两个虚拟设备驱动函数的index.js文件中相关设备的信息，即productKey和deviceName参数的值替换为[添加设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/快速入门/快速入门/cn.zh-CN/快速入门/快速入门/添加设备.md)中创建的光照传感器设备三元组信息和灯设备三元组信息。

   示例如下：

   \`\`\`

   var configs = \[ {productKey: 'Your Product Key',deviceName: 'Your Device Name'}, \];

```text
3.  下载虚拟设备联动函数。您需要通过光照传感器的数据来控制灯，因此需要下载联动函数。

    -   [虚拟设备联动函数](https://iotedge-web.oss-cn-shanghai.aliyuncs.com/public/driverSample/LightMonitor.zip)
4.  将虚拟设备联动函数的index.js文件中相关设备的信息，即Light Product Key和Light Device Name，替换为[添加设备](cn.zh-CN/快速入门/快速入门/添加设备.md#)中创建的灯设备三元组信息。
```

```text
group.getDeviceByProductKeyDeviceName('Light Product Key', 'Light Device Name',.........

```
```

## 上传设备驱动函数至函数计算 <a id="section_isq_p4m_j2b .section"></a>

1. 登录函数计算控制台。
2. 为光照传感器设备和灯设备的函数创建一个服务。

   其中，服务名称必须填写，此处设置为DeviceScript，其与参数请根据您的需求设置。

3. 创建服务成功后，在服务概览页面单击**新建函数**。
4. 选择函数模板，此处选择空白函数模板。
5. 设置光照传感器设备驱动函数的参数。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/6835_zh-CN.png)![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/6837_zh-CN.png)![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15289/6836_zh-CN.png)

   其中，

   所在服务：选择[2](chuang-jian-lian-jie-han-shu-ji-lian-dong-han-shu.md#step2)中创建的服务。

   函数名称：设置您的函数名称，此处设置为LightSensor。

   运行环境：设置函数运行的环境，此示例中选择nodejs8。

   代码配置：复制已下载的光照传感器设备驱动函数的index.js文件内容到在线编辑器中。

   其余参数的值请根据您的需求，参见[函数计算](https://help.aliyun.com/product/50980.html?spm=a2c4g.11186623.3.1.lo2iWt)设置。

6. 单击**下一步**，进入模板授权管理页面，为函数授权。此处选择授权AliyunIOTAccessingFCRole角色，单击**下一步**。
7. 重复[3](chuang-jian-lian-jie-han-shu-ji-lian-dong-han-shu.md#step3)到[6](chuang-jian-lian-jie-han-shu-ji-lian-dong-han-shu.md#step6)的操作，为服务添加灯设备驱动函数和虚拟设备联动函数。

   添加灯设备驱动函数时：

   * 函数名称：设置为Light。
   * 代码配置：复制已下载的灯设备驱动函数的index.js文件内容到在线编辑器中。
   * 其余参数请与[5](chuang-jian-lian-jie-han-shu-ji-lian-dong-han-shu.md#step5)参数设置保持一致。 添加虚拟设备联动函数时：
   * 函数名称：设置为Scene。
   * 代码配置：复制已下载的虚拟设备联动函数的index.js文件内容到在线编辑器中。
   * 其余参数请与[5](chuang-jian-lian-jie-han-shu-ji-lian-dong-han-shu.md#step5)参数设置保持一致。

8. 函数执行验证。

   函数成功创建后，可以直接在函数计算的控制台执行，以验证函数执行情况。函数计算会直接将函数的输出和请求的相关信息打印在控制台上。

