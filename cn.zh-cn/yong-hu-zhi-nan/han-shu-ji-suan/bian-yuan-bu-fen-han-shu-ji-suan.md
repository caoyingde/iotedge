# 边缘部分函数计算

本章为您介绍如何将函数计算用于边缘端，从而在无论连网还是断网情况下，都能快速响应本地消息。

本章节共涉及以下4步操作：

1. 创建函数
2. 为边缘实例配置函数
3. 配置消息路由规则
4. 部署实例

## 创建函数 <a id="section_pwh_14m_j2b .section"></a>

登录函数计算控制台，创建一个函数。具体操作请参考[函数计算文档](https://help.aliyun.com/document_detail/73329.html)。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15102/15408905896551_zh-CN.jpg)

**说明：** 编写函数时，可以使用[边缘API](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/边缘开发指南/云端开发指南/管理分组/CreateGroup.md)编写。

* 函数入口index.handler

  格式为\[文件名\].\[函数名\]。例如，创建函数时指定`Handler`为`index.handler`，那么函数计算会去加载index.js中定义的handler函数。

  ```text
  module.exports.handler = function(event, context, callback) { console.log('hello world'); callback(null, 'hello world'); //必须有，否则函数计算执行时间将会以能容忍最长时间运行 callback 第一个参数代表向上抛出的代码运行异常与否状态，没有错误填null,有错可以上传错误信息 };
  ```

* event参数

  event参数是您调用函数时传入的数据，其类型是Buffer。数据结构可由您自行定义，当消息来自设备时，数据结构如下：

  ```text
  { "topic" : ${TOPIC}, "payload" : ${PAYLOAD} "provider" : { "groupId" : xxx } }
  ```

  * TOPIC 为一个字符串类型，首字母必须是"/"，格式：

    ```text
    Trigger 为设备属性时候： "/sys/${PRODUCT}/${DEVICE_NAME}/thing/event/property/post" Trigger 为设备事件时候： "/sys/${PRODUCT}/${DEVICE_NAME}/thing/event/${EVENT}/post"" Trigger 为函数计算的时候： topic 是用户sendMessage 指定的topic，格式由用户自定义。
    ```

  * PAYLOAD 其类型是Object。

    设备属性上报payload格式：

    ```text
    { "Power":{ "value":"on", "time":1524448722000 }, "WF":{ "value": {}, "time":1524448722000 } }
    ```

    设备事件上报payload格式：

    ```text
    {"params":{"value":{"Power":"on","WF":"2"},"time":1524448722000}}
    ```

* context参数

  context参数中包含一些函数的运行时信息，暂未使用，后续留作扩展。

* callback参数

  callback参数用于返回调用函数的结果。

  * 签名是`function(err, data)`。
  * 参数与Nodejs中惯用的callback一样，第一个参数是error，第二个参数是data。
    * 若调用时err不为空，函数将返回`HandledInvocationError`，否则将返回data的内容。
    * 若data是`Buffer`类型，将直接返回数据。

      若data是`object`，数据将被转换成JSON字符串返回。

      若data是其他类型，将被转换成string返回。

## 为边缘实例配置函数 { .section}

函数创建完成后，您可以在IoT控制台，边缘实例中将函数添加至某个实例。此时需要您配置边缘运行规则。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15102/15408905896552_zh-CN.png)

* 运行模式
  * 按需运行（OnDemand）：按照路由消息来触发，每收到一条路由消息，拉起一次进程执行handler。多个事件则启动多个进程并发执行，执行完毕后退出进程。

    特点：handler每次调用都拉起一个的进程执行，所有的输入都从参数获得，是标准的无状态、事件驱动编程模型

  * 持续运行（LongLived）：代码部署成功后会启动一个常驻进程，消息触发的请求会在该进程的请求队列中排队，每个请求到来调用一次handler函数运行，函数运行完毕进程不退出，等待响应下一个消息请求。

    特点：handler的函数每次调用都在同一个进程上下文中，可以在该进程中保存计数器等统计和状态信息，更适合需要保存运行状态的场景。

    典型应用：

    * 设备接入程序（驱动）开发。
    * 记录状态信息。比如开关第一次按下时灯是红色，第二次是黄色，第三次是蓝色。
* 内存限制

  函数运行所需的内存资源，单位为MB。为了维护系统运行的稳定性，防止因恶意代码或内存泄漏榨干系统内存，当运行handler函数进程的内存使用超出限定值时，进程会被杀死。内存限制建议区间为64MB~2GB。

* 超时限制

  超时时间主要限制FC的handler入口函数。

  * 按需运行模式下，如果handler函数执行，且超过时间限制，则FC进程退出。
  * 持续运行模式下，如果handler函数执行，且超过时间限制，当前FC进程不会退出，会抛出异常。

## 配置消息路由规则 <a id="section_mtd_h2n_j2b .section"></a>

如果您创建的函数需要外部消息来触发，则需要在边缘实例的消息路由中配置相应的消息路由规则，将消息的目的地设置为相应函数。具体设置请参考[设置消息路由](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/函数计算/cn.zh-CN/用户指南/消息路由/设置消息路由.md)。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15102/15408905896554_zh-CN.png)

## 部署实例 <a id="section_mdp_m2n_j2b .section"></a>

请参考[边缘实例](https://github.com/caoyingde/iotedge/tree/c697ce413860528d62c9113f91fb2ceb706e7d24/cn.zh-CN/用户指南/函数计算/cn.zh-CN/用户指南/边缘分组.md)来部署实例，实现设备按规则运行。

