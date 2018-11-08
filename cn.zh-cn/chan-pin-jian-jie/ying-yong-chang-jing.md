# 应用场景

物联网边缘计算平台的典型应用场景有：未来酒店、工业生产、风力发电效率提升等。

## 未来酒店 <a id="section_yhw_m2f_h2b .section"></a>

通过边缘网关快速集成本地设备后，边缘网关作为本地节点快速响应本地事件，实现本地M2M的智能联动，实现室内室外一体化的语音智能。

特点：

* 设备联动：入楼闸机、房间门、空调、照明、水电等智能联动。
* 边缘计算：人脸信息、房间号、保洁日历、时间段等全部由边缘网关计算处理。
* 语音智能：入住后，天猫精灵成为私人管家，接收住户指令，管理多端设备。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14809/15356322626616_zh-CN.png)

整个场景的运转流程是：

1. 住户自助办理入住，入住机将信息等规则推送给边缘网关。
2. 住户在入楼闸机处刷脸，闸机与边缘网关核对身份信息。
3. 信息核对成功后，闸机打开，住户被允许进入大楼。
4. 住户来到房间门口，刷脸。房间门与边缘网关核对身份信息。
5. 信息核对成功后，房间门打开，住户被允许进入房间。
6. 房间门打开的同时，房间水电、空调、照明、电视等根据环境设置自动开启，天猫精灵开始工作。
7. 住户入住后有其他需求，可以语音将指令需求告知天猫精灵，实现进一步智能联动。

## 风力发电 <a id="section_zm4_x2g_h2b .section"></a>

在风力发电机组本地网络中，部署边缘计算网关，实时采集机组数据。在本地处理采集的数据后，先将数据上传至阿里云MaxCompute，再使用大数据训练模型后，对发电参数，如风向灵敏度、启动延时参数等做优化。将模型转化为算法或者规则导入本地边缘节点，自动调整风电机组参数，提高机组发电性能。

特点：

* 数据实时采集：多机组多数据点同时采集。
* 大数据处理：数据上传至阿里云后，使用大数据训练模型。
* 即时反馈：算法或规则导入本地边缘节点后，实时自动调整机组参数，实现最优化生产。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14809/15356322626617_zh-CN.png)
