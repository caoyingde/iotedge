# 配置边缘计算节点

边缘计算节点，即承载计算能力的边缘网关。配置边缘计算节点包含两部分内容：在控制台创建边缘网关与设备，使用Docker镜像配置边缘计算节点。

## 控制台创建网关 <a id="task_swz_vph_h2b"></a>

1. 登录物联网平台控制台。 
2. 单击产品管理、**创建产品**。在弹出页面，单击选择**高级版**，设置参数，单击**确认**，创建网关产品。 产品是一批具有相同功能的设备的集合，您可以创建产品，用于批量管理设备。比如，同一产品型号的设备，功能都相同。您可以为该型号创建产品，以此来批量管理设备。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15096/15342303006543_zh-CN.png)

   您需要设置如下参数：

   * 版本选择：选择**高级版**。
   * 产品名称：在此处为产品命名，产品名称需保持账号内唯一。此例中，填写**gateway\_linkedge**。
   * 节点类型：在此处选择产品类型。此例中，选择**网关**。
   * 设备类型：在此处选择**边缘网关**。
   * 数据格式：在此处选择该产品的数据传输格式。边缘网关请选择**Alink JSON**。
   * 使用ID²认证：ID²是物联网平台提供的一种安全认证方式，边缘计算中并不涉及这种认证。此处，请选择**否**。
   * 产品描述：使用文字描述该产品，可为空。

3. 单击设备管理、**添加设备**。设置参数后，单击**确认**，创建一个网关设备。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15096/15342303006544_zh-CN.png)

   此处参数设置如下：

   * 产品：选择上一步中创建的产品，此处选择**gateway\_linkedge**。
   * DeviceName：为该网关设备命名。DeviceName需保持产品内唯一。如不填写，系统将自动生成。

     **说明：** DeviceName支持大写字母\[A-Z\]、小写字母\[a-z\]、数字\[0-9\]和下划线（\_）。且不能以下划线开头或结尾。

4. 网关设备创建完成后，系统会弹出设备证书，即设备三元组（包括ProductKey、DeviceName和DeviceSecret）。您可以**一键复制**并保存这些信息，用于后续设备开发使用。

## 配置边缘计算节点 <a id="task_d4m_wph_h2b"></a>

1. 目前支持在以下系统中配置边缘计算节点：
   * Windows x86\_64
   * MAC x86\_64
   * Ubuntu 18.04 x86\_64
   * Ubuntu 16.04 x86\_64
2. 安装Docker环境。
   1. 下载Docker软件，具体请参考[Docker官网](https://www.docker.com/)。 
   2. 安装Docker，具体安装方法请参考[Docker官方文档](https://docs.docker.com/)。 

      **说明：** 若您的系统为Linux版，请至Docker Store下载安装适配您Linux发行版的Docker客户端。
3. 下载边缘计算节点启动脚本。
   * Windows或Mac版：curl -O [http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/linkedge\_start.sh](http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/linkedge_start.sh)
   * Linux版：wget [http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/linkedge\_start.sh](http://aliyun-iotedge.oss-cn-hangzhou.aliyuncs.com/linkedge_start.sh)
4. 启动边缘计算节点，使设备上线。 `./linkedge_start.sh {version} {productkey} {devicename} {devicesecret}`

   **说明：**

   * 请将{version}替换为需要的[Docker镜像版本号](../chan-pin-jian-jie/fa-bu-li-shi.md)。
   * 请将{productkey} {devicename} {devicesecret}替换为实际的网关设备三元组信息。

5. 边缘计算节点成功启动后，您可以在设备管理界面，对应网关设备详情页上，看到设备状态变为**在线**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15096/15342303006546_zh-CN.png)

6. （可选）停止边缘计算节点。 ./linkedge\_start.sh --stop

   **说明：** 执行此命令会终止边缘计算节点的运行，但不会删除Docker容器。若您需要删除Docker容器可以使用docker rm命令。

7. （可选）重启边缘计算节点。 ./linkedge\_start.sh --restart {version}

   **说明：**

   * 请将{version}替换为您的Docker镜像版本号。
   * 如果已执行[3](pei-zhi-bian-yuan-ji-suan-jie-dian-1.md#step3start)中的命令，启动过边缘计算节点，使用此命令可以实现快速重启，并且不再需要配置网关设备三元组信息。
   * 如果边缘计算节点已被删除，使用此命令会重新拉取指定版本的Docker镜像，并启动新的Docker容器。

