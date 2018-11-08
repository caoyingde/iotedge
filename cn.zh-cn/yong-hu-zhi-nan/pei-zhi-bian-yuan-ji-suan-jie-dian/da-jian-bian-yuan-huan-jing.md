# 搭建边缘环境

本节介绍如何使用Docker镜像搭建边缘环境，配置边缘计算节点。

目前支持在以下系统中搭建边缘环境：

* Windows x86\_64
* MAC x86\_64
* Ubuntu 18.04 x86\_64
* Ubuntu 16.04 x86\_64
* 安装Docker环境。
  1. 下载Docker软件，具体请参考[Docker官网](https://www.docker.com/)。 
  2. 安装Docker，具体安装方法请参考[Docker官方文档](https://docs.docker.com/)。 

     **说明：** 若您的系统为Linux版，请至Docker Store下载安装适配您Linux发行版的Docker客户端。
* 下载边缘计算节点启动脚本。
  * Windows或Mac版：curl -O [http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/link-iot-edge.sh](http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/link-iot-edge.sh)
  * Linux版：wget [http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/link-iot-edge.sh](http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/link-iot-edge.sh)
* 启动边缘计算节点，使设备上线。 `./link-iot-edge.sh {version} {productkey} {devicename} {devicesecret}`

  **说明：**

  * 请将{version}替换为需要的[Docker镜像版本号](../../chan-pin-jian-jie/fa-bu-li-shi.md)，建议您使用最新的版本号。
  * 请将{productkey} {devicename} {devicesecret}替换为实际的网关设备三元组信息。
  * 执行此命令，会删除已存在的Docker容器，创建新的Docker容器，并保存网关三元组信息。

* 边缘计算节点成功启动后，您可以在设备管理界面，对应网关设备详情页上，看到设备状态变为**在线**。

  ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15096/15398408216546_zh-CN.png)

* （可选）停止边缘计算节点。 ./link-iot-edge.sh --stop

  **说明：** 执行此命令会终止边缘计算节点的运行，但不会删除Docker容器。若您需要删除Docker容器可以使用docker rm命令。

* （可选）重启边缘计算节点。 ./link-iot-edge.sh --restart {version}

  **说明：**

  * 请将{version}替换为您的Docker镜像版本号。
  * 如果已执行[3](da-jian-bian-yuan-huan-jing.md#step3start)中的命令，启动过边缘计算节点，使用此命令可以实现快速重启，并且不再需要配置网关设备三元组信息。
  * 如果边缘计算节点已被删除，使用此命令会重新拉取指定版本的Docker镜像，并启动新的Docker容器。

