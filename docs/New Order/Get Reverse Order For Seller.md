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

<Highlight color="#00A854">GET/POST</Highlight>  <Highlight1 color="#EEEEEE">/reverse/getreverseordersforseller</Highlight1>

Use this API to get the list of items for a range of reverse orders.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Malaysia      | https://api.lazada.com.my/rest |
| Singapore     | https://api.lazada.sg/rest |
| Philippines   | https://api.lazada.com.ph/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Thailand      | https://api.lazada.co.th/rest |

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
| ofc_status_list       | String[]	   | false	| ["RETURN_CANCELED"] |     |Limit the ofc status
| reverse_order_id      | Number	   | false	| 0 |   |Specify trade order id
| trade_order_id        | Number	   | false	| 0 |   |Specify reverse order id
| page_size             | Number	   | <Highlight2>true</Highlight2>	| 10 | Default Value: 10 | Page size, default 10 |
| reverse_status_list   | String[]     | false	| ["REQUEST_INITIATE"] |    |Limit the reverse status. |
| page_no               | Number	   | <Highlight2>true</Highlight2>	| 1 | Default Value: 1 | Page no | 
| return_to_type        | String       | false | RTM |  |Return Type. Enum Values：[RTM, RTW] | 
| dispute_in_progress   | Boolean	   | false	| true |      |Is dispute in progress |


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
| result                                | Object     | {}                                       | Response body |
| -total                                | Number	 | 50                                       | The total number of data | 
| -items                                | Object[]	 | {}                                       | Data list |
| --reverse_order_id                    | Number	 | 0                                        | Reverse order id |
| --trade_order_id                      | Number	 | 0                                        | Trade order id |
| --request_type                        | String	 | CANCEL                                   | Reverse request type |
| --is_rtm                              | Boolean	 | true                                     | rtm:true, rtw:false |
| --shipping_type                       | String	 | DEFAULT                                  | Shipping type | 
| --reverse_order_lines                 | Object[]	 | [{}]                                     | Reverse order lines list|
| --reverse_order_line_id               | Number	 | 0                                        | Reverse order line id |
| ---trade_order_line_id                | Number	 | 0                                        | Trade order line id |
| ---reverse_status                     | String	 | REQUEST_INITIATE                         | Reverse order status |
| ---is_need_refund                     | String	 | true                                     | Is need refund |
| ---ofc_status                         | String	 | RETURN_CANCELED                          | Ofc status |
| ---product                            | Object	 | {}                                       | Product Object|
| ----product_id                        | Number	 | 0                                        | Product id |
| ----product_sku                       | String	 | 0                                        | Product sku |
| ---product                            | Object	 | {}                                       | Product Object|
| ---buyer                              | Object	 | {}                                       | Buyer Object|
| ----buyer_id                          | Number	 | 0                                        | Buyer id |
| ---trade_order_gmt_create             | Number	 | 0                                        | trade order create time |
| ---refund_amount                      | Number	 | 0                                        | refund amount, currency in cent, except VN (for example for SG, 100 equals SGD $1; for VN, 10000 equals VND 10000) |
| ---reason_text                        | String	 | Out of stock                             | reverse reason |
| ---reason_code                        | Number	 | 123                                      | reverse reason code |
| ---refund_payment_method              | String	 | Alipay                                   | payment method |
| ---whqc_decision                      | String	 | scrap                                    | warehouse decision |
| ---return_order_line_gmt_create       | Number	 | 0                                        | reverse order line create time |
| ---return_order_line_gmt_modified     | Number	 | 0                                        | reverse order line modified time |
| ---is_dispute                         | Boolean	 | true                                     | is in dispute or not |
| ---seller_sku_id                      | String	 | th-1000                                  | seller sku id |
| ---item_unit_price                    | Number	 | 0                                        | price, currency in cent, except VN (for example for SG, 100 equals SGD $1; for VN, 10000 equals VND 10000) |
| ---platform_sku_id                    | String	 | th-1001                                  | platform sku id |
| -page_no                              | Number	 | 1                                        | Page no |
| -success                              | Boolean	 | true                                     | Result |
| -page_size                            | Number	 | 10                                       | Page size |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/reverse/getreverseordersforseller");
request.addApiParameter("ofc_status_list", "[\"RETURN_CANCELED\"]");
request.addApiParameter("reverse_order_id", "0");
request.addApiParameter("trade_order_id", "0");
request.addApiParameter("page_size", "10");
request.addApiParameter("reverse_status_list", "[\"REQUEST_INITIATE\"]");
request.addApiParameter("page_no", "1");
request.addApiParameter("return_to_type", "RTM");
request.addApiParameter("dispute_in_progress", "true");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/reverse/getreverseordersforseller');
$request->addApiParam('ofc_status_list','[\"RETURN_CANCELED\"]');
$request->addApiParam('reverse_order_id','0');
$request->addApiParam('trade_order_id','0');
$request->addApiParam('page_size','10');
$request->addApiParam('reverse_status_list','[\"REQUEST_INITIATE\"]');
$request->addApiParam('page_no','1');
$request->addApiParam('return_to_type','RTM');
$request->addApiParam('dispute_in_progress','true');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/reverse/getreverseordersforseller");
request.AddApiParameter("ofc_status_list", "[\"RETURN_CANCELED\"]");
request.AddApiParameter("reverse_order_id", "0");
request.AddApiParameter("trade_order_id", "0");
request.AddApiParameter("page_size", "10");
request.AddApiParameter("reverse_status_list", "[\"REQUEST_INITIATE\"]");
request.AddApiParameter("page_no", "1");
request.AddApiParameter("return_to_type", "RTM");
request.AddApiParameter("dispute_in_progress", "true");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/reverse/getreverseordersforseller')
request.add_api_parameter("ofc_status_list", "[\"RETURN_CANCELED\"]")
request.add_api_parameter("reverse_order_id", "0")
request.add_api_parameter("trade_order_id", "0")
request.add_api_parameter("page_size", "10")
request.add_api_parameter("reverse_status_list", "[\"REQUEST_INITIATE\"]")
request.add_api_parameter("page_no", "1")
request.add_api_parameter("return_to_type", "RTM")
request.add_api_parameter("dispute_in_progress", "true")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/reverse/getreverseordersforseller')
request.add_api_param('ofc_status_list', '[\"RETURN_CANCELED\"]')
request.add_api_param('reverse_order_id', '0')
request.add_api_param('trade_order_id', '0')
request.add_api_param('page_size', '10')
request.add_api_param('reverse_status_list', '[\"REQUEST_INITIATE\"]')
request.add_api_param('page_no', '1')
request.add_api_param('return_to_type', 'RTM')
request.add_api_param('dispute_in_progress', 'true')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X POST url + '/reverse/getreverseordersforseller' \
-H 'Content-Type:application/x-www-form-urlencoded;charset=utf-8' \
-d 'app_key=12345678' \
-d 'timestamp=1656134472458' \
-d 'access_token=37c66819338b4562e17675b8c5c4dbd0' \
-d 'sign_method=sha256' \
-d 'sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC' \
-d 'ofc_status_list=%5B%22RETURN_CANCELED%22%5D' \
-d 'reverse_order_id=0' \
-d 'trade_order_id=0' \
-d 'page_size=10' \
-d 'reverse_status_list=%5B%22REQUEST_INITIATE%22%5D' \
-d 'page_no=1' \
-d 'return_to_type=RTM' \
-d 'dispute_in_progress=true' \
```

### Response Example
---
```
{
  "result": {
    "total": "50",
    "success": "true",
    "page_no": "1",
    "items": [
      {
        "reverse_order_lines": [
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          },
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          }
        ],
        "reverse_order_id": "0",
        "request_type": "CANCEL",
        "is_rtm": "true",
        "shipping_type": "DEFAULT",
        "trade_order_id": "0"
      },
      {
        "reverse_order_lines": [
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          },
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          }
        ],
        "reverse_order_id": "0",
        "request_type": "CANCEL",
        "is_rtm": "true",
        "shipping_type": "DEFAULT",
        "trade_order_id": "0"
      }
    ],
    "page_size": "10"
  },
  "code": "0",
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
| 	| Query result is empty. 	      | |  

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)