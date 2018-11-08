# 产品架构

物联网边缘计算平台主要涉及设备端、边缘计算端和云端三个部分。

物联网边缘计算平台的架构如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14807/15408883776611_zh-CN.png)

物联网应用可广泛应用于：智能生活、智能工业、智能楼宇、环境保护、农业水利、能源监控等环境。计算平台主要涉及：

* 设备端

  开发者使用设备接入SDK，将非标设备转换成标准物模型，就近接入边缘计算节点，从而实现设备的管理和控制。

* 边缘计算端

  设备连接到边缘计算节点后，边缘计算节点可以实现设备数据的采集、流转、存储、分析和上报设备数据至云端，同时边缘计算节点提供规则引擎、函数计算引擎，方便场景编排和业务扩展。

* 云端

  设备数据上传云端后，可以结合阿里云功能，如大数据、AI学习等，通过标准API接口，实现更多功能和应用。
