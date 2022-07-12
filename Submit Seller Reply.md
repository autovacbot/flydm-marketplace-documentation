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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/review/seller/reply/add</Highlight1>

submit seller reply for customers review

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Philippines   | https://api.lazada.com.ph/rest |
| Singapore     | https://api.lazada.sg/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Vietnam       | https://api.lazada.vn/rest |
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
| - id          | Number   | <Highlight2>true</Highlight2>	| 11111111111  |        | review id that user wants to reply to. Can be obtain from GetProductReviewList |
| - content     | String   | <Highlight2>true</Highlight2>	| thank you for your reply |        | reply content in text, only support reply in text.max length = 500 |

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
| data                                  | Boolean    | true                                     | reply success or fail   |
| success                               | Boolean    | true                                     | reply success or fail |
| error_code                            | String	 | error                                    | error code |
| error_msg                             | String	 | error                                    | error msg|



### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/review/seller/reply/add");
request.setHttpMethod("GET");
request.addApiParameter("id", "11111111111");
request.addApiParameter("content", "thank you for your reply");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/review/seller/reply/add','GET');
$request->addApiParam('id','11111111111');
$request->addApiParam('content','thank you for your reply');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/review/seller/reply/add");
request.SetHttpMethod("GET");
request.AddApiParameter("id", "11111111111");
request.AddApiParameter("content", "thank you for your reply");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/review/seller/reply/add','GET')
request.add_api_parameter("id", "11111111111")
request.add_api_parameter("content", "thank you for your reply")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/review/seller/reply/add','GET')
request.add_api_param('id', '11111111111')
request.add_api_param('content', 'thank you for your reply')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/review/seller/reply/add?timestamp=1655954545607&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&id=11111111111&content=thank+you+for+your+reply'
```

### Response Example
---
```
{
  "error_msg": "error",
  "code": "0",
  "data": "true",
  "success": "true",
  "error_code": "error",
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
| Error Code            | 	Error Message         | Description        |
| :---                  | :---                    | :---               |
| PARAMS_VALIDATE_ERROR	| NULL_SELLERID 	      | Cannot recognize sellerid| 
| PARAMS_VALIDATE_ERROR	| NULL_ID	              | Cannot recognize id| 
| PARAMS_VALIDATE_ERROR	| NULL_CONTENT	          | Empty content| 
| PARAMS_VALIDATE_ERROR	| REPLY_ALREADY	          | Already replied. All reply needs go through quality control process.| 
| PARAMS_VALIDATE_ERROR	| NO_SUCH_REVIEW	      | No such review| 
| PARAMS_VALIDATE_ERROR	| REVIEW_STATUS_CANNOT_REPLY	| Review status cannot be replied to, review's status may be changed because of being edited or reported| 
| PARAMS_VALIDATE_ERROR	| REVIEW_TYPE_DONOT_SUPPORT_REPLY	| Review type cannot be replied to, only reply to PRODUCT_REVIEW| 
| PARAMS_VALIDATE_ERROR	| REVIEW_INFO_DONOT_SUPPORT_REPLY	| Review info cannot be replied to, review must have text content or images or video| 
| PARAMS_VALIDATE_ERROR	| REVIEW_REPORTED_CANNOT_REPLY	    | Review been reported cannot be repied to| 
| PARAMS_VALIDATE_ERROR	| REPLY_CONTENT_TOO_LONG	        | Reply too long| 
| PARAMS_VALIDATE_ERROR	| BEYOND_REPLY_PERIOD	            | Reply over due| 
| TRAFFIC_CONTROL	    | TRAFFIC_CONTROL	                | Traffic control| 
### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)