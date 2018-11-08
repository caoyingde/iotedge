# 官方驱动

官方驱动是由阿里云提供的通信协议驱动，包括Modbus、OPC UA官方驱动和Light、LightSensor官方示例驱动。

## Modbus驱动介绍 <a id="section_wsy_ncp_y2b .section"></a>

Modbus是常用的应用层数据通信协议，阿里云官方Modbus驱动（以下简称Modbus驱动）支持Modbus-RTU和Modbus-TCP两种交互。

Modbus驱动支持的功能有读取输入状态和输入寄存器，读/写线圈状态和保持寄存器。

Modbus驱动支持从控制台下载，您可以对下载后的驱动代码进行更改，可作为您的自定义代码使用。

Modbus驱动使用步骤如下：

1. 创建高级版产品，并选择接入网关协议为Modbus，具体创建产品步骤请参见\[创建产品\(高级版\)\]\(../../../../cn.zh-CN/用户指南/产品与设备/创建产品\(高级版\).md\#\)。
2. 为产品添加设备，具体添加设备步骤请参见[单个创建设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/创建设备/单个创建设备.md)和[批量创建设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/创建设备/批量创建设备.md)。
3. 为产品定义物模型，具体定义方法请参见[新增物模型](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/物模型/新增物模型.md)。
4. 完成上述设备配置后，需要配置设备与网关的交互方式。
   1. 创建子设备通道，具体方法请参见[子设备通道管理](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/网关与子设备/子设备通道管理.md)。
   2. 添加子设备，具体方法请参见[子设备管理](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/网关与子设备/子设备管理.md)。
5. 到边缘实例中分配相关设备和网关，选择Modbus驱动进行部署。

## OPC UA驱动介绍 <a id="section_dbw_f2p_y2b .section"></a>

Link IoT Edge产品中提供用于接入OPC UA设备的驱动，下面简称OPC UA驱动。

OPC UA驱动支持从控制台下载，您可以对下载后的驱动代码进行更改，可作为您的自定义代码使用。

OPC UA驱动包含三部分功能：

* 负责接入OPC UA设备。
* 对接入设备数据进行转换，符合阿里云物模型规范。
* 设备数据上行和下行控制。

OPC UA驱动使用步骤如下：

1. 创建高级版产品，并选择设备协议为OPC UA，具体创建产品步骤请参见\[创建产品\(高级版\)\]\(../../../../cn.zh-CN/用户指南/产品与设备/创建产品\(高级版\).md\#\)。
2. 为产品添加设备，具体添加设备步骤请参见[单个创建设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/创建设备/单个创建设备.md)和[批量创建设备](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/创建设备/批量创建设备.md)。
3. 为产品定义物模型，具体定义方法请参见[新增物模型](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/物模型/新增物模型.md)。
4. 完成上述设备配置后，需要配置设备与网关的交互方式，目前仅支持OPC UA交互。 1. 创建子设备通道，具体方法请参见[子设备通道管理](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/网关与子设备/子设备通道管理.md)。

   ```text
   其中，对参数进行如下设置：

   |参数|参数设置|
   |:-|:---|
   |通道名称|设置OPC UA Server通道名称|
   |连接地址|OPC UA Server监听地址|
   |用户名|登录OPC UA Server用户名|
   |密码|登录OPC UA Server密码|
   |安全模式|访问OPC UA Server安全数据交互加密策略|
   |安全策略|访问OPC UA Server数据交互加密算法|
   |方法调用超时|OPC UA驱动调用OPC UA Server方法调用超时时间|
   |数字证书|访问OPC UA Server鉴权认证证书|
   |私钥证书|访问OPC UA Server数据加密密钥|
   ```

   1. 添加子设备，具体方法请参见[子设备管理](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/网关与子设备/子设备管理.md)。

      其中，对参数进行如下设置：

      | 参数 | 参数设置 |
      | :--- | :--- |
      | 产品 | 使用OPC UA驱动的产品 |
      | 设备名 | 使用OPC UA驱动的设备 |
      | 关联通道 | 已创建的OPC UA Server通道 |
      | 节点路径 | 设备在OPC UA服务器下的节点路径 |

5. 到边缘实例中分配相关设备和网关，选择OPC UA驱动进行部署。

## Light驱动介绍 <a id="section_d1y_qcm_4fb .section"></a>

Light驱动是Link IoT Edge提供的一款智能灯泡的模拟驱动，是用于说明驱动开发方式的示例驱动。Light驱动支持智能灯泡的开关操作，可以用于模拟快速入门中的灯设备。

Light驱动的使用示例请参见[快速入门](../../kuai-su-ru-men/da-jian-bian-yuan-huan-jing.md)。

## LightSensor驱动介绍 <a id="section_dz1_tcm_4fb .section"></a>

LightSensor驱动是Link IoT Edge提供的一款光照传感器的模拟驱动，是用于说明驱动开发方式的示例驱动，光照强度数据按照一定周期重复，可以用于模拟快速入门中的光照传感器设备。

LightSensor驱动的使用示例请参见[快速入门](../../kuai-su-ru-men/da-jian-bian-yuan-huan-jing.md)。

