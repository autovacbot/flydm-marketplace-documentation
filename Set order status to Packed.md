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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/pack</Highlight1>

Use this API to mark an order item as being packed.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Singapore     | https://api.lazada.sg/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Philippines   | https://api.lazada.com.ph/rest |


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
| - shipping_provider    | String   | <Highlight2>true</Highlight2>      | Aramax | | Valid shipment provider as looked up via GetShipmentProviders. Mandatory for the "dropship" delivery type.    |
| - delivery_type        | String   | <Highlight2>true</Highlight2>      | dropship |  | only support dropship   |
| - order_item_ids       | String   | <Highlight2>true</Highlight2>      | [1530553,1830236] |  | List of oder items to be marked ready to ship. Comma separated list in square brackets. Mandatory.   |

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
| -order_items                          | Object[]   | []                                       | order items          |
| --order_item_id                       | Number     | 123456                                   | Seller Center order item ID  |
| --purchase_order_id                   | Number     | 567890                                   | OMS order ID          |
| --purchase_order_number               | String     | ABC-123456                               | OMS order number  |
| --package_id                          | String     | MPDS-200131783-9800                      | Shipping package ID  |
| --shipment_provider                   | String     | 5                                        | shipment provider  |
| --tracking_number                     | String     | TRACK-1126935-4306                       | Package tracking number |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/pack");
request.addApiParameter("shipping_provider", "Aramax");
request.addApiParameter("delivery_type", "dropship");
request.addApiParameter("order_item_ids", "[1530553,1830236]");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/pack');
$request->addApiParam('shipping_provider','Aramax');
$request->addApiParam('delivery_type','dropship');
$request->addApiParam('order_item_ids','[1530553,1830236]');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/pack");
request.AddApiParameter("shipping_provider", "Aramax");
request.AddApiParameter("delivery_type", "dropship");
request.AddApiParameter("order_item_ids", "[1530553,1830236]");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);

```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/pack')
request.add_api_parameter("shipping_provider", "Aramax")
request.add_api_parameter("delivery_type", "dropship")
request.add_api_parameter("order_item_ids", "[1530553,1830236]")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/pack')
request.add_api_param('shipping_provider', 'Aramax')
request.add_api_param('delivery_type', 'dropship')
request.add_api_param('order_item_ids', '[1530553,1830236]')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X POST url + '/order/pack' \
-H 'Content-Type:application/x-www-form-urlencoded;charset=utf-8' \
-d 'app_key=12345678' \
-d 'timestamp=1655779038053' \
-d 'access_token=37c66819338b4562e17675b8c5c4dbd0' \
-d 'sign_method=sha256' \
-d 'sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC' \
-d 'shipping_provider=Aramax' \
-d 'delivery_type=dropship' \
-d 'order_item_ids=%5B1530553%2C1830236%5D' \
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
        "purchase_order_id": "567890",
        "purchase_order_number": "ABC-123456",
        "tracking_number": "TRACK-1126935-4306",
        "shipment_provider": "5",
        "package_id": "MPDS-200131783-9800"
      },
      {
        "order_item_id": "123456",
        "purchase_order_id": "567890",
        "purchase_order_number": "ABC-123456",
        "tracking_number": "TRACK-1126935-4306",
        "shipment_provider": "5",
        "package_id": "MPDS-200131783-9800"
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
| 20                | E020: "%s" Invalid Order Item ID | The specified order item ID is not valid. |
| 21                | E021: OMS Api Error Occurred      | Internal system error. |
| 23                | E023: "%s" Invalid Order Item IDs      | The specified order item IDs are not valid. |
| 24                | E024: "%s" Invalid Delivery Type      | The specified delivery type is not valid. |
| 25                | E025: "%s" Invalid Shipping Provider      | The specified shipping provider is not valid. |
| 29                | E029: Order items must be from the same order | The specified order items must be from the same order. |
| 73                | E073: All order items must have status Pending or Ready To Ship. (%s) | The status of order items is not valid. |
| 91                | E091: You are not allowed to set the shipment provider and tracking number and the delivery type is wrong. Please use sent_to_warehouse.  | Error occurred due to permission issue. |



### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)