# 设备上线及函数执行

## 部署分组 <a id="section_vsn_23m_j2b .section"></a>

1. 在[物联网边缘计算控制台](http://iot.console.aliyun.com/)，选择**边缘管理** &gt; **边缘分组**。系统显示边缘分组页面。
2. 在已创建的分组名右侧，单击**查看**，进入分组详情页面。
3. 单击**部署分组**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/6778_zh-CN.png)

4. 单击**确认**。

   您可通过单击**部署详情**来查看部署进度及结果。

## 查看设备上线情况 <a id="section_lx5_pnm_j2b .section"></a>

部署分组后，您将在分组的设备列表中可以看到对应设备已经上线。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/6779_zh-CN.png)

## 查看设备状态 <a id="section_rql_14m_j2b .section"></a>

您可查看具体设备详情，看到设备数据已经发送至云端。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/6781_zh-CN.png)

## 查看函数运行日志 { .section}

您可边缘计算节点的日志中查看函数运行的情况。

`grep ${函数ID} /linkedge/run/logger/iot-gravity/log.INFO`

其中，将${函数ID}替换为实际的函数ID。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/6840_zh-CN.png)

