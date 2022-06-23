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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/document/get</Highlight1>

Use this API to retrieve order-related documents, including invoices and shipping labels.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Singapore     | https://api.lazada.sg/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Vietnam       | https://api.lazada.vn/rest |
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
| - doc_type    | String   | <Highlight2>true</Highlight2>      | shippingLabel | | Document types, including 'invoice', 'shippingLabel', or 'carrierManifest'. Mandatory.    |
| - order_item_ids    | String   | <Highlight2>true</Highlight2>      | [279709, 279709] | Max List Size: 100 | Identifier of the order item for which the caller wants to get a document. Mandatory.   |

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
| data                                  | Object     | {}                                       | response data    |
| -document                             | Object     | {}                                       | document          |
| --file                                [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)| String     | PHN0eWxlPnRlRrU3VRbUNDJyAvPjwvcD4K       | To reconstruct the file, the data from the  node needs to be base64 decoded, and interpreted according to the mime_type.  |
| --mime_type                           | String     | text/html                                | To reconstruct the file, the data from the  node needs to be base64 decoded, and interpreted according to the mime_type.          |
| --document_type                       | String     | shippingLabel                            | Document types, including 'invoice', 'shippingLabel', or 'carrierManifest'.  |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/document/get");
request.setHttpMethod("GET");
request.addApiParameter("doc_type", "shippingLabel");
request.addApiParameter("order_item_ids", "[279709, 279709]");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/document/get','GET');
$request->addApiParam('doc_type','shippingLabel');
$request->addApiParam('order_item_ids','[279709, 279709]');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/document/get");
request.SetHttpMethod("GET");
request.AddApiParameter("doc_type", "shippingLabel");
request.AddApiParameter("order_item_ids", "[279709, 279709]");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);

```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/document/get','GET')
request.add_api_parameter("doc_type", "shippingLabel")
request.add_api_parameter("order_item_ids", "[279709, 279709]")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/document/get','GET')
request.add_api_param('doc_type', 'shippingLabel')
request.add_api_param('order_item_ids', '[279709, 279709]')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/order/document/get?timestamp=1655717905153&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&doc_type=shippingLabel&order_item_ids=%5B279709%2C+279709%5D'
```

### Response Example
---
```
{
  "code": "0",
  "data": {
    "document": {
      "file": "PHN0eWxlPnRlRrU3VRbUNDJyAvPjwvcD4K",
      "mime_type": "text/html",
      "document_type": "shippingLabel"
    }
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
| 20                | E020: "%s" Invalid Order Item IDs | The specified order item ID is not valid. |
| 21                | E021: OMS Api Error Occurred      | Internal system error. |
| 32                | E032: Document type "%s" is not valid | The specified document type is not valid. |
| 34                | E034: Order Item must be packed. Please call SetStatusToReadyToShip before | The current status of the order item is not valid. |
| 35                | E035: "%s" was not found | The specified order item is not found. |



### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)