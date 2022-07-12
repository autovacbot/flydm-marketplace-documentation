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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/cancel</Highlight1>

Use this API to cancel a single order item.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Philippines   | https://api.lazada.com.ph/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Singapore     | https://api.lazada.sg/rest |
| Malaysia      | https://api.lazada.com.my/rest |

#### Common Request Parameters
---
| Name          | Type     | Required  | Description  |
| :---          | :---     | :---       | :---          |
| app_key       | String   | <Highlight2>true</Highlight2>     | Unique app ID issued by LAZOP console when you apply for an app category       |
| timestamp     | String   | <Highlight2>true</Highlight2>      | The time stamp of the request e.g. 1517820392000 (which translates to 5 February 2018 08:46:32) with less than 7200s difference from UTC time       |
| access_token  | String   | <Highlight2>true</Highlight2>      | API interface call credentials       |
| sign_method   | String   | <Highlight2>true</Highlight2>      | The HMAC hash algorithm you are using to calculate your signature       |
| sign          | String   | <Highlight2>true</Highlight2>      | Part of the authentication process that is used for identifying and verifying who is sending a request (click [here](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10450&docId=108068) for details)       |

### Request Parameters
---

| Name          | Type     | Required  | Demo Value  | Rule     | Description   |
| :---          | :---     | :---      | :---        | :---     | :---          |
| - reason_detail | String   | false   | Out of stock | | Reason detail. Optional |
| - reason_id | Number   | <Highlight2>true</Highlight2> | 15 |  | ID of the cancel reason.   |
| - order_item_id | Number   | <Highlight2>true</Highlight2> | 140168 |  | Order item ID. Mandatory   |

### Common Response Parameters 
---

| Name        | Type        | Description        |
| :---         | :---         | :---                |
| type        | String      | Error type. Optional values ​​are ISP (service provider error), ISV (developer error), SYSTEM (platform system error)               |
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
| success                               | Boolean    | true                                     | Success    |


### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/cancel");
request.addApiParameter("reason_detail", "Out of stock");
request.addApiParameter("reason_id", "15");
request.addApiParameter("order_item_id", "140168");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/cancel');
$request->addApiParam('reason_detail','Out of stock');
$request->addApiParam('reason_id','15');
$request->addApiParam('order_item_id','140168');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/cancel");
request.AddApiParameter("reason_detail", "Out of stock");
request.AddApiParameter("reason_id", "15");
request.AddApiParameter("order_item_id", "140168");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);

```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/cancel')
request.add_api_parameter("reason_detail", "Out of stock")
request.add_api_parameter("reason_id", "15")
request.add_api_parameter("order_item_id", "140168")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/cancel')
request.add_api_param('reason_detail', 'Out of stock')
request.add_api_param('reason_id', '15')
request.add_api_param('order_item_id', '140168')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X POST url + '/order/cancel' \
-H 'Content-Type:application/x-www-form-urlencoded;charset=utf-8' \
-d 'app_key=12345678' \
-d 'timestamp=1655791793961' \
-d 'access_token=37c66819338b4562e17675b8c5c4dbd0' \
-d 'sign_method=sha256' \
-d 'sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC' \
-d 'reason_detail=Out+of+stock' \
-d 'reason_id=15' \
-d 'order_item_id=140168' \
```

### Response Example
---
```
{
  "code": "0",
  "success": "true",
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
| Error Code        | 	Error Message                   | Description        |
| :---              | :---                              | :---               |
| 20                | E020: "%s" Invalid Order Item ID  | The specified order item ID is not valid. |
| 21                | E021: OMS Api Error Occurred      | Internal system error. |
| 22                | E022: "%s" Invalid Reason         | The specified cancel reason is not valid. |
| 28                | E028: It is not possible to set the order to the status "%s"  | Failed to change the order status. |


### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)