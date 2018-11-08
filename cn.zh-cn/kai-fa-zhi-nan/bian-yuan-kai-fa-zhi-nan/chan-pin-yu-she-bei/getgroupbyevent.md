# getGroupByEvent

## 功能介绍 <a id="section_vr4_rbf_h2b .section"></a>

获取部署至网关的分组对象。您可以通过该分组对象获取设备对象。

## 请求参数 <a id="section_cfk_ghp_32b .section"></a>

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| event | Buffer | handler函数返回的Buffer类型的event值。 |

## 返回参数 <a id="section_eyv_jhp_32b .section"></a>

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| group | Group | 返回的Group对象，您可以从该对象中获取在云中定义的边缘分组中的设备信息。 |

## 使用示例 <a id="section_uvg_mhp_32b .section"></a>

```text
module.exports.handler = function(event, context, callback) {
    const linkedge = require("linkedge");
    var group = linkedge.getGroupByEvent(event);
};
```

