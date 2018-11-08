# 流数据分析

[流数据分析](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/数据分析服务/流数据分析/任务管理.md)是一种用流的方法快速实时处理数据的计算方式，边缘计算中的流数据分析，继承于物联网平台数据分析产品的流数据分析的能力，可以无缝对接数据分析产品，在数据分析产品中创建流数据分析任务，并将该任务下发到边缘端，通过边缘设备实时运行。运行结果可以存储在边缘端也可以直接传输至云端。

边缘部分流数据分析主要特点如下：

* 运行在边缘端，不依赖网络，低时延。
* 对数据进行采集、清洗、加工、聚合之后再上云，大大减少数据传输成本。

## 操作步骤 <a id="section_f2n_qxg_qfb .section"></a>

1. 登录[物联网平台控制台](http://iot.console.aliyun.com)。
2. 参考[流数据分析](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/数据分析服务/流数据分析/任务管理.md)，创建、设置并发布数据分析任务。

   其中，执行任务需选择**边缘端**。

   **说明：** 图片以组件编排任务为例。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40709/154098238821255_zh-CN.jpg)

3. 单击左侧导航栏中**边缘计算** &gt; **边缘实例**。

   找到要分配流数据分析任务的实例，单击对应操作栏中的**查看**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15328/154098238913914_zh-CN.png)

4. 在实例详情页面，选择**流数据分析**，然后单击**分配任务**或**分配流数据分析任务**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40709/154098238921201_zh-CN.png)

5. 在弹出的分配任务页面中，选择要分配给实例的任务，单击**分配**。

   本例中，流数据分析任务名称为test\_local\_db。

   分配成功后，单击**完成**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40709/154098239121202_zh-CN.png)

   完成规则添加后，便可在该实例的实例详情页面上，查看该实例的流数据分析任务信息。

6. 部署实例。为实例分配任务后，单击页面右上角**部署**，并在弹出对话框中，单击**确认**。

   您可以在本页面中查看部署状态和部署详情。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40709/154098239121203_zh-CN.png)

