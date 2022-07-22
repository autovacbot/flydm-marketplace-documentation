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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/reverse/return/update</Highlight1>

Seller can use this API to action on return and refund related.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Malaysia      | https://api.lazada.com.my/rest |
| Singapore     | https://api.lazada.sg/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Philippines   | https://api.lazada.com.ph/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Indonesia     | https://api.lazada.co.id/rest |


#### Common Request Parameters
---
| Name          | Type     | Required  | Description  |
| :---          | :---     | :---       | :---          |
| app_key       | String   | <Highlight2>true</Highlight2>     | Unique app ID issued by LAZOP console when you apply for an app category       |
| timestamp     | String   | <Highlight2>true</Highlight2>      | The time stamp of the request e.g. 1517820392000 (which translates to 5 February 2018 08:46:32) with less than 7200s difference from UTC time       |
| access_token  | String   | false   | API interface call credentials       |
| sign_method   | String   | <Highlight2>true</Highlight2>      | The HMAC hash algorithm you are using to calculate your signature       |
| sign          | String   | <Highlight2>true</Highlight2>      | Part of the authentication process that is used for identifying and verifying who is sending a request (click [here](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10450&docId=108068) for details)       |

### Request Parameters
---

| Name          | Type     | Required  | Demo Value  | Rule     | Description   |
| :---          | :---     | :---      | :---        | :---     | :---          |
| action        | String   | <Highlight2>true</Highlight2>  | instantRefund | instantRefund;agreeReturn;refuseReturn;agreeRefund;refuseRefund;confirmDelivery |
| reverse_order_id | Number | <Highlight2>true</Highlight2> | 0 | reverse order id | 
| reverse_order_item_ids | Number[] | <Highlight2>true</Highlight2> | [] | reverse order item id list |
| reason_id     | Number   | false | 0 | reason id | 
| comment       | String   | false | comment | comment | 
| image_info    | Object[] | false | [] | image_info |
| -name         | String   | false | name | image name
| -url          | String   | false | url | image url

### Common Response Parameters 
---

| Name        | Type        | Description        |
| :---        | :---        | :---                |
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
| data                                  | Object     | {}                                       | data |
| -reverse_order_line                   | Object[]   | []                                       | reverse order line |
| --reverse_order_line_id               | Number     | 0                                        | reverse order line id |
| --reason_source                       | String     | reason_source                            | reason source |
| --reason_type                         | String     | reason_type                              | reason type |
| --reason_id                           | Number     | 0                                        | reason id |
| --reason_name                         | String     | out of stock                             | reason name |
| --reason_desc                         | String     | stock is 0                               | reason desc |
| --refund_amount                       | Number     | 0                                        | refund amount |
| --is_cancel                           | Boolean	 | true                                     | cancel or not|
| --order_id                            | Number     | 0                                        | order id |
| --seller_sku                          | String     | 0                                        | seller sku |
| --paid_price                          | Number     | 0                                        | paid price |
| --apply_reason                        | String     | out of stock                             | apply reason |
| --order_line_id                       | Number     | 0                                        | order line id |
| -reverse_order_id                     | Number     | 0                                        | reverse orde id |
| -reason_info                          | Object[]   | []                                       | reason info |
| --reason_id                           | Number     | 0                                        | reason id |
| --reason_name                         | String     | out of stock                             | reason name |
| -total_refund                         | String     | 0                                        | total refund amount |


### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/reverse/return/update");
request.setHttpMethod("GET");
request.addApiParameter("action", "instantRefund");
request.addApiParameter("reverse_order_id", "0");
request.addApiParameter("reverse_order_item_ids", "[]");
request.addApiParameter("reason_id", "0");
request.addApiParameter("comment", "comment");
request.addApiParameter("image_info", "[{\"name\":\"name\",\"url\":\"url\"}]");
LazopResponse response = client.execute(request);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/reverse/return/update','GET');
$request->addApiParam('action','instantRefund');
$request->addApiParam('reverse_order_id','0');
$request->addApiParam('reverse_order_item_ids','[]');
$request->addApiParam('reason_id','0');
$request->addApiParam('comment','comment');
$request->addApiParam('image_info','[{\"name\":\"name\",\"url\":\"url\"}]');
var_dump($c->execute($request));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/reverse/return/update");
request.SetHttpMethod("GET");
request.AddApiParameter("action", "instantRefund");
request.AddApiParameter("reverse_order_id", "0");
request.AddApiParameter("reverse_order_item_ids", "[]");
request.AddApiParameter("reason_id", "0");
request.AddApiParameter("comment", "comment");
request.AddApiParameter("image_info", "[{\"name\":\"name\",\"url\":\"url\"}]");
LazopResponse response = client.Execute(request);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/reverse/return/update','GET')
request.add_api_parameter("action", "instantRefund")
request.add_api_parameter("reverse_order_id", "0")
request.add_api_parameter("reverse_order_item_ids", "[]")
request.add_api_parameter("reason_id", "0")
request.add_api_parameter("comment", "comment")
request.add_api_parameter("image_info", "[{\"name\":\"name\",\"url\":\"url\"}]")
response = client.execute(request)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/reverse/return/update','GET')
request.add_api_param('action', 'instantRefund')
request.add_api_param('reverse_order_id', '0')
request.add_api_param('reverse_order_item_ids', '[]')
request.add_api_param('reason_id', '0')
request.add_api_param('comment', 'comment')
request.add_api_param('image_info', '[{\"name\":\"name\",\"url\":\"url\"}]')
response = client.execute(request)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/order/reverse/return/update?timestamp=1656146349396&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&action=instantRefund&reverse_order_id=0&reverse_order_item_ids=%5B%5D&reason_id=0&comment=comment&image_info=%5B%7B%22name%22%3A%22name%22%2C%22url%22%3A%22url%22%7D%5D'
```

### Response Example
---
```
{
  "code": "0",
  "data": {
    "reason_info": [
      {
        "reason_name": "out of stock",
        "reason_id": "0"
      },
      {
        "reason_name": "out of stock",
        "reason_id": "0"
      }
    ],
    "reverse_order_id": "0",
    "total_refund": "0",
    "reverse_order_line": [
      {
        "paid_price": "0",
        "is_cancel": "true",
        "reason_id": "0",
        "reason_source": "reason_source",
        "reason_desc": "stock is 0",
        "apply_reason": "out of stock",
        "reason_type": "reason_type",
        "seller_sku": "0",
        "refund_amount": "0",
        "order_line_id": "0",
        "reason_name": "out of stock",
        "order_id": "0",
        "reverse_order_line_id": "0"
      },
      {
        "paid_price": "0",
        "is_cancel": "true",
        "reason_id": "0",
        "reason_source": "reason_source",
        "reason_desc": "stock is 0",
        "apply_reason": "out of stock",
        "reason_type": "reason_type",
        "seller_sku": "0",
        "refund_amount": "0",
        "order_line_id": "0",
        "reason_name": "out of stock",
        "order_id": "0",
        "reverse_order_line_id": "0"
      }
    ]
  },
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
| Error Code            | 	Error Message                               | Description        |
| :---                  | :---                                          | :---               |
| 100	                | E0100: reverse order list is empty	        | E0100: reverse order list is empty |
| 106	                | E0106: ROC internal error	                    | E0106: ROC internal error |
| 107	                | E0107: invalid action	                        | E0107: invalid action |
| 108	                | E0108: reason can't be empty if you want to refuse return or refund	| E0108: reason can't be empty if you want to refuse return or refund |
| 109	                | E0109: comment can't be empty if you want to refuse return or refund	| E0109: comment can't be empty if you want to refuse return or refund |
| 110	                | E0110: image can't be empty if you want to refuse refund	| E0110: image can't be empty if you want to refuse refund |
| 111	                | E0111: do not support massive reverse order line operation if you want to refuse return or refund	| E0111: do not support massive reverse order line operation if you want to refuse return or refund |
| 112	                | E0112: no reverse order found	                | E0112: no reverse order found |
| 113	                | E0113: reverse order line have unknown status	| E0113: reverse order line have unknown status |
| 114	                | E0114: this reverse does not support this action	| E0114: this reverse does not support this action |
| 116	                | E0116: no seller id	                        | E0116: no seller id |
| 117	                | E0117: no user id	                            | E0117: no user id |
| 118	                | E0118: no user email	                        | E0118: no user email |
| 125	                | E0125: invalid reverse id	                    | E0125: invalid reverse id |
| 126	                | E0126: invalid reverse order lines	        | E0126: invalid reverse order lines |
| 127	                | E0127: invalid seller id for this reverse order line	| E0127: invalid seller id for this reverse order line |  

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)