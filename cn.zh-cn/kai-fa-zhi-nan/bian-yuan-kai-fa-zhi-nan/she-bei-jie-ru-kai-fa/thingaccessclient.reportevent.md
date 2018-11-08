# ThingAccessClient.reportEvent

## 功能介绍 <a id="section_wgj_wv2_h2b .section"></a>

主动上报设备事件。

## 请求参数 <a id="section_fvn_vfp_32b .section"></a>

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| eventName | String | 事件对应的名称，与您在产品定义中创建事件的名称一致。 |
| args | Object | 事件中包含的属性key与value，取值格式为：\`\`\` |

{ "key1": "value1", "key2": "value2" }

\`\`\`

\|

