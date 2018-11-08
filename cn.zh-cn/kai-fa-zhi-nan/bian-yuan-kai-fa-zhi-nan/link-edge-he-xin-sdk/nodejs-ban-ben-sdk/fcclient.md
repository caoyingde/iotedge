# FCClient

包含函数计算相关API的类。

## invokeFunction\(params, callback\) <a id="section_wxc_xjd_kfb .section"></a>

调用指定函数。

* params：{Object} 参数对象，包含：
  * functionId：{String} \(Required\) 被调用函数的唯一ID。
  * invocationType：{String} 调用类型。同步为`Sync`，异步为`Async`。默认为同步。
  * payload：{String\|Buffer} 参数信息作为函数的输入。
* callback\(err, data\)：回调函数，遵循JS标准实践。
  * err：{Error} 成功则返回null，否则为发生的错误。
  * data：被调函数的返回值。

