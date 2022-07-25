export const Highlight = ({children, color}) => (
  <span
    style={{
      backgroundColor: color,
      borderRadius: '2px',
      color: '#FFFFFF',
      padding: '0.2rem',
    }}>
    {children}
  </span>
);

export const Highlight1 = ({children, color}) => (
  <span
    style={{
      backgroundColor: color,
      borderRadius: '2px',
      color: '#333333',
      padding: '0.2rem',
    }}>
    {children}
  </span>
);

export const Highlight2 = ({children, color}) => (
  <span
    style={{
      backgroundColor: color,
      color: '#FF0000',
    }}>
    {children}
  </span>
);

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/reverse/reason/list</Highlight1>

Get the list of reject reason. Need to be used in all refuse refund actions

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Thailand      | https://api.lazada.co.th/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Singapore     | https://api.lazada.sg/rest |
| Philippines   | https://api.lazada.com.ph/rest |

#### Common Request Parameters
---
| Name          | Type     | Required  | Description  |
| :---          | :---     | :---       | :---          |
| app_key       | String   | <Highlight2>true</Highlight2>      | Unique app ID issued by LAZOP console when you apply for an app category       |
| timestamp     | String   | <Highlight2>true</Highlight2>      | The time stamp of the request e.g. 1517820392000 (which translates to 5 February 2018 08:46:32) with less than 7200s difference from UTC time       |
| access_token  | String   | false                              | API interface call credentials       |
| sign_method   | String   | <Highlight2>true</Highlight2>      | The HMAC hash algorithm you are using to calculate your signature       |
| sign          | String   | <Highlight2>true</Highlight2>      | Part of the authentication process that is used for identifying and verifying who is sending a request (click [here](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10450&docId=108068) for details)       |

### Request Parameters
---

| Name          | Type     | Required  | Demo Value  | Rule     | Description   |
| :---          | :---     | :---      | :---        | :---     | :---          |
| reverse_order_line_id | Number	   | <Highlight2>true</Highlight2>	 | 0 |          | reverse order line id| 


### Common Response Parameters 
---

| Name        | Type        | Description        |
| :---         | :---         | :---                |
| type        | String      | Error type. Optional values ​​are ISP (service provider error), ISV (developer error), SYSTEM (platform system error) |
| code        | String      | Error code. For example: ServiceUnavailable                |
| message     | String      | Description of error details                |
| request_id  | String      | Request a unique identifier               |
| detail      | Object[]    | If the API call is for batch processing, when the call fails (all or part of the request failure), the response contains the error details. See the following example: |
```bash
{ 
    "detail": [
        {
            "field": "Product",
            "seller_sku": "api-create-test-1",
            "message": "SELLER_SKU_INVALID"
        },
        {
            "field": "Product2",
            "message": "SELLER_SKU_INVALID"
        }
    ]
} 
```

### Response Parameters
---
| Name                                  | Type       | Demo Value                               | Description     |
| :---                                  | :---       | :---                                     | :---            |
| data                                  | Object[]   | []                                       | data |
| -reason_id                            | Number	 | 1000017                                  | reason id | 
| -muti_language_text                   | String	 | out of stock                             | multi-language reason |
| -text                                 | String	 | out of stock                             | english reason|

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/reverse/reason/list");
request.setHttpMethod("GET");
request.addApiParameter("reverse_order_line_id", "0");
LazopResponse response = client.execute(request);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/reverse/reason/list','GET');
$request->addApiParam('reverse_order_line_id','0');
var_dump($c->execute($request));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/reverse/reason/list");
request.SetHttpMethod("GET");
request.AddApiParameter("reverse_order_line_id", "0");
LazopResponse response = client.Execute(request);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/reverse/reason/list','GET')
request.add_api_parameter("reverse_order_line_id", "0")
response = client.execute(request)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/reverse/reason/list','GET')
request.add_api_param('reverse_order_line_id', '0')
response = client.execute(request)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/order/reverse/reason/list?timestamp=1656131590585&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&reverse_order_line_id=0'
```

### Response Example
---
```
{
  "code": "0",
  "data": [
    {
      "muti_language_text": "out of stock",
      "text": "out of stock",
      "reason_id": "1000017"
    },
    {
      "muti_language_text": "out of stock",
      "text": "out of stock",
      "reason_id": "1000017"
    }
  ],
  "request_id": "0ba2887315178178017221014"
}
```

### Error Example
---
```
{
  "code": "MISSING_PARAMETER",
  "type": "ISV",
  "message": "missing required parameter: access_token",
  "request_id": "0ba2887315172940728551014"
}
```

### Error Codes
---
| Error Code            | 	Error Message               | Description        |
| :---                  | :---                          | :---               |
| 103	                | E0103: reverse order line id is empty when query reject reason | E0103: reverse order line id is empty when query reject reason | 
| 106	                | E0106: ROC internal error	    | E0106: ROC internal error | 
| 116	                | E0116: no seller id           | E0116: no seller id | 
| 117	                | E0117: no user id	            | E0117: no user id | 
| 118	                | E0118: no user email          | E0118: no user email | 
| 119	                | E0119: cannot find any cancel reasons for these orders | E0119: cannot find any cancel reasons for these orders|  

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)