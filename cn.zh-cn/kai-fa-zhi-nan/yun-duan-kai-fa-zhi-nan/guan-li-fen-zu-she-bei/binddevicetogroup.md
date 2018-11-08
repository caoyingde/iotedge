# BindDeviceToGroup

绑定设备到指定分组。

## 请求参数 <a id="section_cdz_tcf_h2b .section"></a>

| 参数 | 类型 | 是否必需 | 描述 |
| :--- | :--- | :--- | :--- |
| Action | String | 是 | 要执行的操作。取值：BindDeviceToGroup。 |
| GroupId | Long​ | 是 | ​分组ID。 |
| ProductKey | String | 是 | 产品Key。 |
| DeviceName | String | 是 | 设备名称。 |
| DeviceType | String | 是 | 设备类型。取值：gateway：网关，device：设备。 |

## 返回参数 <a id="section_n1m_4df_h2b .section"></a>

| 参数 | 类型 | 描述 |
| :--- | :--- | :--- |
| RequestId | String | 阿里云为该请求生成的唯一标识符。 |
| Success | Boolean | 表示是否调用成功。true表示调用成功，false表示调用失败。 |
| ErrorMessage | String | 调用失败时，返回的出错信息。 |
| Code | String | 接口返回码。200表示成功，其他返回码表示错误。 |

## 示例 <a id="section_qwb_tdf_h2b .section"></a>

**请求示例**

```text
https://iot.cn-shanghai.aliyuncs.com/?Action=BindDeviceToGroup
&GroupId=134429
&ProductKey=a1XXXXXXXXX
&DeviceName=uHrognqkk7ZJpmNXXXXX
&DeviceType=device
&公共请求参数
```

**返回示例**

```text
{
  "RequestId": "D832E764-A75C-474E-B9C3-AA75E9D579E6",
  "Success": true,
  "Code": "200"
}
```

