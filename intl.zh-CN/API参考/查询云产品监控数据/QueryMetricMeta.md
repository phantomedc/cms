# QueryMetricMeta {#concept_lyv_rgs_zfb .concept}

查询云监控开放的时序类监控项的监控项描述，通常配合查询监控项接口QueryMetricMeta和查询监控数据接口QueryProjectMeta/QueryMetricLast 一起使用。

## 请求类型 {#section_pfl_zgs_zfb .section}

POST|GET

## 请求参数 { .section}

|**名称**|**类型**|必填|**描述**|
|------|------|--|------|
|Action|String|是|系统规定参数，取值：QueryMetricMeta|
|Project|String|否|指标所属的Project，按等于匹配|
|Metric|String|否|指标名，按等于匹配|
|Labels|String|否| 根据标签过滤，格式\[\{"name":"标签名","value":"标签值"\},\{"name":"标签名","value":"标签值"\}\]

 已有的标签name说明：

 MetricCategory：监控项分类的描述

 alertEnable：是否需要报警

 alertUnit：建议的报警单位

 unitFactor：单位转换系数

 minAlertPeriod：最小报警周期

 productCategory：产品类型分类

 |
|PageNumber|int|否|分页参数，默认1|
|PageSize|int|否|每页最大数量，默认30|

## 返回参数 { .section}

|**名称**|**类型**|**描述**|
|------|------|------|
|RequestId|String|用于跟踪|
|Success|Boolean|用于标识本次调用是否成功|
|ErrorCode|String|错误码200成功|
|ErrorMessage|String|错误码消息|
|Resources|Array|返回的metric meta列表|

## Metric meta各字段的含义解释 { .section}

|名称|类型|描述|
|--|--|--|
|Project|String|监控项的Project名称，用于查询监控数据|
|Metric|String|监控项名称|
|Unit|String|监控项的单位|
|Statistics|String|统计方法，多个用英文逗号分隔，例如：Maximum,Minimum,Average|
|Dimensions|String|监控项的Dimensions，多级用英文逗号分隔，例如：userId,instanceId|
|Periods|String|监控项的所有统计周期，多个用英文逗号分隔：15,60,900|
|Labels|String| 监控项的标签，是一个json的string\[\{"name":"标签名","value":"标签的值"\}\]，可以是多个，name可以重复

 已有的标签name说明：

 metricCategory：指标分类

 alertEnable：是否可以报警

 alertUnit：报警单位

 unitFactor：单位转换系数

 minAlertPeriod：最小报警周期

 productCategory：产品

 |
|Description|String|监控项的描述|

## 错误编码 { .section}

|HTTPStateCode|ErrorCode|ErrorMessage|
|-------------|---------|------------|
|403|AccessForbidden|User not authorized to operate on the specified resource.|
|400|ParameterInvalid|Illegal parameters.|
|404|ResourceNotFound|The specified resource is not found.|
|500|InternalError|The request processing has failed due to some unknown error.|

## 请求示例 { .section}

```

import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.cms.model.v20180308.QueryMetricMetaRequest;
import com.aliyuncs.cms.model.v20180308.QueryMetricMetaResponse;
import com.aliyuncs.profile.DefaultProfile;


class Test {
public static void main(String[] args) {


// 初始化
DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "", "");
IAcsClient client = new DefaultAcsClient(profile);

//设置参数
QueryMetricMetaRequest request = new ListMetricMetaRequest();
request.setAcceptFormat(FormatType.JSON); 
request.setProject("acs_ecs_dashboard");

// 发起请求
try {
QueryMetricMetaResponse response = client.getAcsResponse(request);
System.out.println("Success:" + response.getSuccess());
System.out.println("ErrorCode:" + response.getErrorCode());
System.out.println("ErrorMessage:" + response.getErrorMessage());
System.out.println("RequestId:" + response.getRequestId());
} catch (Exception e) {
e.printStackTrace();
}
}
}
```

## 返回示例 { .section}

```


{
"RequestId": "60498C25-B5AE-48CD-B03D-207011F21E8A",
"ErrorCode": 200,
"Success": true,
"Resources": {
"Resource": [
{
"Description": "",
"Statistics": "Average",
"Labels": "[{\"name\":\"minAlertPeriod\",\"value\":\"60\"},{\"name\":\"metricCategory\",\"value\":\"role\"},{\"name\":\"is_alarm\",\"value\":\"true\"}]",
"Metric": "ActiveApplications",
"Dimensions": "clusterId,role",
"Project": "acs_hbase",
"Periods": "30,300"
},
{
"Description": "",
"Statistics": "Average",
"Labels": "[{\"name\":\"minAlertPeriod\",\"value\":\"60\"},{\"name\":\"metricCategory\",\"value\":\"role\"},{\"name\":\"is_alarm\",\"value\":\"true\"}]",
"Metric": "ActiveApplications",
"Dimensions": "clusterId,role",
"Project": "acs_emr",
"Periods": "30,300,3600"
},
{
"Description": "端口当前活跃连接数",
"Statistics": "Average,Minimum,Maximum",
"Labels": "[{\"name\":\"alertUnit\",\"value\":\"Count\"},{\"name\":\"minAlertPeriod\",\"value\":\"60\"},{\"name\":\"metricCategory\",\"value\":\"port\"},{\"name\":\"is_alarm\",\"value\":\"true\"}]",
"Metric": "ActiveConnection",
"Dimensions": "instanceId,port,protocol",
"Project": "acs_slb_dashboard",
"Periods": "60,300",
"Unit": "Count"
},
{
"Description": "高防IP活跃并发连接",
"Statistics": "Maximum",
"Labels": "[{\"name\":\"alertUnit\",\"value\":\"count\"},{\"name\":\"minAlertPeriod\",\"value\":\"60\"}]",
"Metric": "ActiveConnection",
"Dimensions": "instanceId,ip",
"Project": "acs_ddos",
"Periods": "30,60,300",
"Unit": "count"
},
{
"Description": "活跃消息数",
"Statistics": "Average,Minimum,Maximum",
"Labels": "[{\"name\":\"alertUnit\",\"value\":\"Count\"},{\"name\":\"minAlertPeriod\",\"value\":\"300\"},{\"name\":\"metricCategory\",\"value\":\"queue\"},{\"name\":\"is_alarm\",\"value\":\"true\"}]",
"Metric": "ActiveMessages",
"Dimensions": "region,queue",
"Project": "acs_mns_new",
"Periods": "300",
"Unit": "Count"
}
]
}
}
```

