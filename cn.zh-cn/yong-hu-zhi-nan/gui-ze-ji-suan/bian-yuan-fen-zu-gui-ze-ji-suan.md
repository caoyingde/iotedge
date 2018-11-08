# 边缘分组规则计算

使用边缘分组规则计算需为边缘分组添加和部署规则。部署至边缘分组的规则能够快速响应本地的消息，并且可在断网环境下正常运行。

## 为分组配置规则计算 <a id="section_x4d_1fy_32b .section"></a>

为边缘分组部署规则之前，需先创建规则和边缘分组。规则的创建方法，请参见[云端管理规则计算](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/规则计算/cn.zh-CN/用户指南/规则计算/云端管理规则计算.md)。

规则计算部署步骤：

1. 登录[物联网平台控制台](http://iot.console.aliyun.com)。
2. 单击左侧导航栏中**边缘管理** &gt; **边缘分组**。
3. 找到要添加规则的分组，单击对应操作栏中的**查看**按钮。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15099/15343004446576_zh-CN.png)

4. 在分组详情页面，选择**规则计算**，然后单击**分配规则**或**分配规则计算**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15099/15343004446704_zh-CN.jpg)

5. 在弹出的分配规则页面中，选择要分配给分组的规则，单击**分配**。分配成功后，单击**完成**。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15099/15343004456705_zh-CN.jpg)

   完成规则添加后，便可在该分组的分组详情页面上，查看该分组的规则计算信息。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15099/15343004456707_zh-CN.jpg)

   **说明：** 您可以通过规则 ID，在边缘计算节点中快速查询该规则的相关日志。

6. 部署分组。为分组分配规则后，单击页面右上角**部署分组**，然后在弹出对话框中，单击**确认**。

   您可以在本页面中查看部署状态和部署详情。

   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15099/15343004456708_zh-CN.jpg)

## 查看分组规则计算日志 <a id="section_k1r_5vw_32b .section"></a>

查看分组规则计算日志的两种方法：

* 使用grep命令，查看本地日志。

  边缘计算所在的 Docker 容器安装在 Linux 系统中，所以可使用grep命令，查看边缘分组规则计算的部署和运行的本地日志。

  * 通过grep命令查看边缘分组规则计算部署日志。

    查看部署日志的命令示例：

    ```text
    grep 7dd4db24a05f47c881bb0bbc4c05c9a7 /linkedge/run/logger/userlog/log.INFO | grep IFTTT_Deploy_Result
    ```

    以上示例中， `7dd4db24a05f47c881bb0bbc4c05c9a7` 为要查询的规则 ID。

    返回日志示例：

    ```text
    2018-06-25 22:18:11.869859 [MILESTONE] [iot-gravity(pid=21565) (ifttt.js:153)]: [IFTTT_Deploy_Result][Succeeded] [7dd4db24a05f47c881bb0bbc4c05c9a7] result =  deploy success for jobId: 58432
    ```

  * 通过grep命令查看边缘分组规则计算运行日志。

    查看运行日志的命令示例：

    ```text
    grep 7dd4db24a05f47c881bb0bbc4c05c9a7 /linkedge/run/logger/userlog/log.INFO | grep IFTTT_Running_Result
    ```

    以上示例中， `7dd4db24a05f47c881bb0bbc4c05c9a7` 为要查询的规则 ID。

    返回日志示例：

    \`\`\` 2018-06-25 22:23:22.775260 \[MILESTONE\] \[iot-gravity\(pid=15843\) \(ifttt.js:66\)\]: \[IFTTT\_Running\_Result\]\[Succeeded\] \[7dd4db24a05f47c881bb0bbc4c05c9a7\] jobid 57445 running status : 2 result : \[2018-6-25 22:23:22\];tenantId:66118FD98C3448B79D818FB364985CA3;bizCode:SUMMARY;traceId:6617c55e-5934-4947-b58b-62ac0a443903;sceneId:7dd4db24a05f47c881bb0bbc4c05c9a7;useTime:333;result:true;timestamp:1529936602774

```text
    ```
```

* 在物联网平台控制台，查看已同步至云端的日志。

  **说明：** 若某条规则既在云端运行又在边缘端运行，那么在物联网平台控制台规则计算中，查看到的日志为云端运行日志和边缘端运行日志。

  1. 登录[物联网平台控制台](http://iot.console.aliyun.com)。
  2. 单击左侧导航栏中**边缘管理** &gt; **边缘分组**。
  3. 找到要查看日志的分组，单击对应操作栏中的**查看**按钮。
  4. 在分组详情页面，选择**规则计算**。
  5. 单击规则 ID 对应操作栏中**日志**按钮，即可查看日志。

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15099/15343004456578_zh-CN.png)

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15098/15343004456575_zh-CN.png)

**说明：** 通过grep命令本地查看到的是边缘分组规则计算的全部日志，包括断网场景下的日志；而在物联网平台控制台，只能查看到已同步至云端的日志。

