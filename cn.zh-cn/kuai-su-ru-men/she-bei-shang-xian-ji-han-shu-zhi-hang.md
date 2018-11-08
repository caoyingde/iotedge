# 设备上线及函数执行

## 部署实例 <a id="section_vsn_23m_j2b .section"></a>

1. 在[物联网控制台](http://iot.console.aliyun.com/)，选择**边缘计算** &gt; **边缘实例**。
2. 在已创建的实例名称右侧，单击**查看**。
3. 在实例详情页面，单击**部署**后在弹出框中单击**确认**，部署边缘实例。

   您可以通过单击**部署详情**来查看部署进度及结果。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/15409894316778_zh-CN.png)

## 查看设备上线情况 <a id="section_lx5_pnm_j2b .section"></a>

部署实例后，您可以在实例的子设备列表中看到对应设备状态已显示在线。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/15409894316779_zh-CN.png)

## 查看设备状态 <a id="section_rql_14m_j2b .section"></a>

您可以查看具体设备详情，看到设备数据已经发送至云端。

光照传感器检测室内光照强度是否大于500 Lux。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/15409894316781_zh-CN.png)

若光照强度大于500 Lux，则光照传感器认为室内不需要开灯，从而去关闭灯。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15292/15409894317245_zh-CN.png)

**说明：** 状态为0表示灯已关闭，状态为1表示灯已开启。

