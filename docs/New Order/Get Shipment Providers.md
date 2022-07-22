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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/shipment/providers/get</Highlight1>

Use this API to get the list of all active shipping providers, which is needed when working with the SetStatusToPackedByMarketplace API.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Thailand      | https://api.lazada.co.th/rest |
| Philippines   | https://api.lazada.com.ph/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Singapore     | https://api.lazada.sg/rest |






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
| -shipment_providers                   | Object[]   | []                                       | shipment providers          |
| --is_default                          | Number     | 1                                        | This shipment provider will be the standard selection for order processing.  |
| --tracking_code_example               | String     | 1200234789012                            | The example of tracking code.          |
| --enabled_delivery_options            | String     | []                                       | Shipment provider's speed eligibility, which could be multiple values. Possible values are economy, standard, and express.          |
| --name                                | String     | NinjaVan API                             | Name of the shipment provider. This is the string that is needed for SetStatusToPackedByMarketplace.   |
| --cod                                 | Number     | 1                                        | The shipment provider will be available for cash on delivery orders.          |
| --tracking_code_validation_regex      | String     | /^[0-9]{12}[-]{0,1}[0-9]{0,2}$/i         | The regular expression for validation of tracking code. Example: /^[a-z0-9]{10}$/i Please check using http://regex101.com/#pcre.         |
| --tracking_url                        | String     | https://sofp.lazada.sg                   | Shipment provider's tracking URL. Placeholder {{{TRACKING_NR}}} can be used for tracking code. Otherwise tracking code should be appended to the end of tracking URL.  |
| --api_integration                     | Number     | 1                                        | Value will be 1 if this shipment provider has an API.          |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/shipment/providers/get");
request.setHttpMethod("GET");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/shipment/providers/get','GET');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/shipment/providers/get");
request.SetHttpMethod("GET");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/shipment/providers/get','GET')
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/shipment/providers/get','GET')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/shipment/providers/get?timestamp=1655710799589&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0'
```

### Response Example
---
```
{
  "code": "0",
  "data": {
    "shipment_providers": [
      {
        "tracking_code_example": "1200234789012",
        "enabled_delivery_options": "[]",
        "name": "NinjaVan API",
        "cod": "1",
        "tracking_code_validation_regex": "/^[0-9]{12}[-]{0,1}[0-9]{0,2}$/i",
        "is_default": "1",
        "tracking_url": "https://sofp.lazada.sg",
        "api_integration": "1"
      },
      {
        "tracking_code_example": "1200234789012",
        "enabled_delivery_options": "[]",
        "name": "NinjaVan API",
        "cod": "1",
        "tracking_code_validation_regex": "/^[0-9]{12}[-]{0,1}[0-9]{0,2}$/i",
        "is_default": "1",
        "tracking_url": "https://sofp.lazada.sg",
        "api_integration": "1"
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
| Error Code        | 	Error Message               | Description        |
| :---              | :---                          | :---               |
||Query result is empty.||


### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)