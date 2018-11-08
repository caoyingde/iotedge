# 部署边缘计算节点

本章介绍部署边缘计算节点的方法，边缘计算节点是作为网关设备，用于将设备连接到物联网边缘计算中。

## 安装Docker <a id="section_ojq_gry_32b .section"></a>

1. 下载Docker客户端。
   * MAC版下载：[https://docs.docker.com/docker-for-mac/install/\#download-docker-for-mac](https://docs.docker.com/docker-for-mac/install/#download-docker-for-mac)
   * Windows版下载：[https://docs.docker.com/docker-for-windows/install/\#download-docker-for-windows](https://docs.docker.com/docker-for-windows/install/#download-docker-for-windows)
2. 安装Docker客户端。
   * MAC版安装：[https://docs.docker.com/docker-for-mac/install/\#install-and-run-docker-for-mac](https://docs.docker.com/docker-for-mac/install/#install-and-run-docker-for-mac)
   * Windows版安装：[https://docs.docker.com/docker-for-windows/install/\#install-docker-for-windows-desktop-app](https://docs.docker.com/docker-for-windows/install/#install-docker-for-windows-desktop-app)

## 安装并启动边缘计算节点 <a id="section_ixl_bff_j2b .section"></a>

1. 启动边缘计算节点。

   ```text
   sudo docker run -d --restart=unless-stopped --privileged=true -v linkedge_vol1:/usr/.security -v linkedge_vol2:/etc/.sec/ -v linkedge_vol3:/linkedge/gateway/build/.sst -v linkedge_vol4:/tmp/var/run/ -v linkedge_vol5:/linkedge/run -v linkedge_vol6:/linkedge/gateway/build/config --name=linkedge registry.cn-hangzhou.aliyuncs.com/iotedge/edge_x86_centos:{version} {productkey} {devicename} {devicesecret}
   ```

   **说明：**

   * Windows版Docker环境下执行Docker命令，无需加`sudo`命令。
   * 请将{version}替换为需要的Docker镜像版本号，此处替换为v1.3。
   * 请将{productkey} {devicename} {devicesecret}替换为实际的边缘计算节点设备的三元组信息。

2. 在[物联网边缘计算控制台](http://iot.console.aliyun.com/)，选择**设备管理**，选择已创建好的边缘计算节点产品，查看网关状态。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15286/6743_zh-CN.png)

