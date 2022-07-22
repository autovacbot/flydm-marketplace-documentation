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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/rts</Highlight1>

Use this API to mark an order item as being ready to ship.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Malaysia      | https://api.lazada.com.my/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Singapore     | https://api.lazada.sg/rest |
| Philippines   | https://api.lazada.com.ph/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Indonesia     | https://api.lazada.co.id/rest |



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
| - delivery_type  | String   | <Highlight2>true</Highlight2>   | dropship | | One of the following delivery types: 'dropship' - the seller will send out the package on his own. Now only "dropship" is supported.    |
| - order_item_ids | String   | <Highlight2>true</Highlight2> | [1832590,1832592] |  | List of oder items to be marked ready to ship. Comma separated list in square brackets. Mandatory.   |
| - shipment_provider | String   | <Highlight2>true</Highlight2> | Aramax |  | Valid shipment provider as looked up via GetShipmentProviders. Mandatory for drop-shipping.   |
| - tracking_number | String   | <Highlight2>true</Highlight2> | 12345678 |  | Package tracking number. Mandatory in the case of drop-shipping.   |

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
| :---                                  | :---       | :---                                     | :---             |
| data                                  | Object     | {}                                       | Response body    |
| -order_items                          | Object[]   | []                                       | order items array          |
| --order_item_id                       | Number     | 123456                                   | order item id  |
| --purchase_order_id                   | Number     | 456789                                   | Seller Center identification.  Optional, please ignore it if your business scenario does not cover it.          |
| --purchase_order_number               | String     | ABC-123456                               | Order number in the Seller Center.  Optional, please ignore it if your business scenario does not cover it.  |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/rts");
request.addApiParameter("delivery_type", "dropship");
request.addApiParameter("order_item_ids", "[1832590,1832592]");
request.addApiParameter("shipment_provider", "Aramax");
request.addApiParameter("tracking_number", "12345678");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/rts');
$request->addApiParam('delivery_type','dropship');
$request->addApiParam('order_item_ids','[1832590,1832592]');
$request->addApiParam('shipment_provider','Aramax');
$request->addApiParam('tracking_number','12345678');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/rts");
request.AddApiParameter("delivery_type", "dropship");
request.AddApiParameter("order_item_ids", "[1832590,1832592]");
request.AddApiParameter("shipment_provider", "Aramax");
request.AddApiParameter("tracking_number", "12345678");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);

```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/rts')
request.add_api_parameter("delivery_type", "dropship")
request.add_api_parameter("order_item_ids", "[1832590,1832592]")
request.add_api_parameter("shipment_provider", "Aramax")
request.add_api_parameter("tracking_number", "12345678")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/rts')
request.add_api_param('delivery_type', 'dropship')
request.add_api_param('order_item_ids', '[1832590,1832592]')
request.add_api_param('shipment_provider', 'Aramax')
request.add_api_param('tracking_number', '12345678')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X POST url + '/order/rts' \
-H 'Content-Type:application/x-www-form-urlencoded;charset=utf-8' \
-d 'app_key=12345678' \
-d 'timestamp=1655791287484' \
-d 'access_token=37c66819338b4562e17675b8c5c4dbd0' \
-d 'sign_method=sha256' \
-d 'sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC' \
-d 'delivery_type=dropship' \
-d 'order_item_ids=%5B1832590%2C1832592%5D' \
-d 'shipment_provider=Aramax' \
-d 'tracking_number=12345678' \
```

### Response Example
---
```
{
  "code": "0",
  "data": {
    "order_items": [
      {
        "order_item_id": "123456",
        "purchase_order_id": "456789",
        "purchase_order_number": "ABC-123456"
      },
      {
        "order_item_id": "123456",
        "purchase_order_id": "456789",
        "purchase_order_number": "ABC-123456"
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
| Error Code        | 	Error Message                   | Description        |
| :---              | :---                              | :---               |
| 20                | E020: "%s" Invalid Order Item ID  | The specified order item ID is not valid. |
| 21                | E021: OMS Api Error Occurred      | Internal system error. |
| 23                | E023: "%s" Invalid Order Item IDs      | The specified order item IDs are not valid. |
| 24                | E024: "%s" Invalid Delivery Type      | The specified delivery type is not valid. |
| 25                | E025: "%s" Invalid Shipping Provider      | The specified shipping provider is not valid. |
| 26	            | E026: "%s" Invalid Tracking Number	|The specified tracking number is not valid.|
| 29	            | E029: Order items must be from the same order	|The specified order items must be from the same order.
| 31	            | E031: Tracking ID incorrect. Example tracking ID: "%s"	|The specified tracking ID is not correct.
| 63	            | E063: The tracking code %s has already been used	|The specified tracking code has been used.
| 73	            | E073: All order items must have status Pending or Ready To Ship. (%s)	|The status of order items is not valid.
| 82	            | E082: All order items must have status Pending.	|The status of order items is not valid.
| 91	            | E091: You are not allowed to set the shipment provider and tracking number and the delivery type is wrong. Please use sent_to_warehous	|Error occurred due to permission issue.|
| 94	            | E094: Serial numbers specified incorrectly	|Serial numbers were not specified according to one of the accepted formats for the SerialNumber parameter.|
| 95	            | E095: Invalid serial number format (%s)	|Serial numbers must be 1 to 26 characters; only latin letters and digits are allowed.|
| 96	            | E096: Duplicate serial number among order items (%s)	|Two or more items in the order would share a serial number.|



### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)