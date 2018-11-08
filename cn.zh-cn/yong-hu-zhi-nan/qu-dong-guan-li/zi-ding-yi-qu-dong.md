# 自定义驱动

自定义驱动是您利用Link IoT Edge开发包开发并上传到驱动管理中的驱动程序，可以使用Link IoT Edge的边缘分组部署功能部署到边缘网关中，您需要确保该驱动程序可执行且功能符合您的要求。

1. 登录[物联网平台控制台](https://iot.console.aliyun.com/)。 
2. 在左侧导航栏中，单击**边缘管理** &gt; **驱动管理**。 
3. 在驱动管理页面，单击右侧**创建驱动**。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18781/153933088210611_zh-CN.png) 
4. 设置驱动参数。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18781/153933088210612_zh-CN.png)

   参数说明如下：

   * 语言类型：驱动的语言类型，支持Node.js8和Python3类型。
   * 驱动名称：为您的驱动设置名称，同一个账号内驱动名称必须为唯一。
   * 驱动描述：描述您创建的驱动，不可以为空。
   * 驱动文件：单击**上传文件**，上传您的驱动文件。推荐您按照Link IoT Edge[开发指南](../../bian-yuan-kai-fa-zhi-nan/she-bei-jie-ru-sdk-zong-he-shi-li.md)中的方式开发您的驱动文件。

5. 单击**确认**，完成自定义驱动的创建。 可在驱动管理列表中查看创建的驱动。
6. 自定义驱动创建完成后关联边缘网关与使用该驱动的设备。 
   1. 创建子设备通道，具体方法请参见[子设备通道管理](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/网关与子设备/子设备通道管理.md)。 
   2. 添加子设备，具体方法请参见[子设备管理](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/产品与设备/网关与子设备/子设备管理.md)。 
7. 驱动创建完成之后，需要分配到边缘分组中，详细操作内容请见[边缘分组](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/驱动管理/cn.zh-CN/用户指南/边缘分组.md)中分配设备驱动的步骤。 
8. （可选）单击驱动名称右侧的**编辑**，可以修改已创建的驱动名称、驱动描述或重新上传驱动文件。 
9. （可选）单击驱动名称右侧的**删除**，可以删除已创建的自定义驱动。 

