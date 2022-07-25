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

<Highlight color="#00A854">POST</Highlight>  <Highlight1 color="#EEEEEE">/promotion/voucher/create</Highlight1>

create a new seller voucher promotion

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Malaysia      | https://api.lazada.com.my/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Singapore     | https://api.lazada.sg/rest |
| Philippines   | https://api.lazada.com.ph/rest |
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
| criteria_over_money      | String    | <Highlight2>true</Highlight2>  | 100   |          | Discount details, if order value reaches set value, will money discount or percentage discount|
| voucher_type             | String   | <Highlight2>true</Highlight2>	| COLLECTIBLE_VOUCHER |      |  Voucher type, just set COLLECTIBLE_VOUCHER|
| apply                    | String    | <Highlight2>true</Highlight2>  | SPECIFIC_PRODUCTS   |          | apply scope: ENTIRE_SHOP \ SPECIFIC_PRODUCTS|
| collect_start            | Number   | false  | 1625649720000   |          | The time that customers can collect the voucher|
| display_area             | String    | <Highlight2>true</Highlight2>  | REGULAR_CHANNEL   |          | The area that customers can see the voucher. REGULAR_CHANNEL\STORE_FOLLOWER\OFFLINE\LIVE_STREAM\SHARE_VOUCHER\CEM_SELLER|
| period_end_time          | Number    | <Highlight2>true</Highlight2>  | 1630339199000   |          | The period end time that customers can use the voucher|
| voucher_name             | String    | <Highlight2>true</Highlight2>  | test voucher   |          | Voucher name|
| voucher_discount_type    | String    | <Highlight2>true</Highlight2>  | MONEY_VALUE_OFF   |          | Discount type, MONEY_VALUE_OFF | PERCENTAGE_DISCOUNT_OFF |
| offering_money_value_off | String    | false  | 1   |          | Discount details, if order value reaches criteria_over_money value, will discount money value|
| period_start_time       | Number    | <Highlight2>true</Highlight2>  | 1626969600000   |          | The period start time that customers can use the voucher|
| limit      | Number     | <Highlight2>true</Highlight2>  | 1   |          | 	
Voucher limit per customer|
| issued      | Number    | <Highlight2>true</Highlight2>  | 5   |          | Revision should be greater than the current setting|
| max_discount_offering_money_value      | String    | false  | 50   |          | Discount details, if order value reaches criteria_over_money value, allow maximum discount per order, just support percentage discount off type|
| offering_percentage_discount_off       | Number    | false  | 1   |          | Discount details, if order value reaches criteria_over_money value, will percentage discount off value|

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
| data                                  | Number	 | 9616200353530                            | promotion ID|
| success                               | Boolean	 | true                                     | true \ false| 
| error_code                            | Number	 | null                                     | error code
| error_msg                             | String	 | null                                     | error message| 

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/promotion/voucher/create");
request.addApiParameter("criteria_over_money", "100");
request.addApiParameter("voucher_type", "COLLECTIBLE_VOUCHER");
request.addApiParameter("apply", "SPECIFIC_PRODUCTS");
request.addApiParameter("collect_start", "1625649720000");
request.addApiParameter("display_area", "REGULAR_CHANNEL");
request.addApiParameter("period_end_time", "1630339199000");
request.addApiParameter("voucher_name", "test voucher");
request.addApiParameter("voucher_discount_type", "MONEY_VALUE_OFF");
request.addApiParameter("offering_money_value_off", "1");
request.addApiParameter("period_start_time", "1626969600000");
request.addApiParameter("limit", "1");
request.addApiParameter("issued", "5");
request.addApiParameter("max_discount_offering_money_value", "50");
request.addApiParameter("offering_percentage_discount_off", "1");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/promotion/voucher/create');
$request->addApiParam('criteria_over_money','100');
$request->addApiParam('voucher_type','COLLECTIBLE_VOUCHER');
$request->addApiParam('apply','SPECIFIC_PRODUCTS');
$request->addApiParam('collect_start','1625649720000');
$request->addApiParam('display_area','REGULAR_CHANNEL');
$request->addApiParam('period_end_time','1630339199000');
$request->addApiParam('voucher_name','test voucher');
$request->addApiParam('voucher_discount_type','MONEY_VALUE_OFF');
$request->addApiParam('offering_money_value_off','1');
$request->addApiParam('period_start_time','1626969600000');
$request->addApiParam('limit','1');
$request->addApiParam('issued','5');
$request->addApiParam('max_discount_offering_money_value','50');
$request->addApiParam('offering_percentage_discount_off','1');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/promotion/voucher/create");
request.AddApiParameter("criteria_over_money", "100");
request.AddApiParameter("voucher_type", "COLLECTIBLE_VOUCHER");
request.AddApiParameter("apply", "SPECIFIC_PRODUCTS");
request.AddApiParameter("collect_start", "1625649720000");
request.AddApiParameter("display_area", "REGULAR_CHANNEL");
request.AddApiParameter("period_end_time", "1630339199000");
request.AddApiParameter("voucher_name", "test voucher");
request.AddApiParameter("voucher_discount_type", "MONEY_VALUE_OFF");
request.AddApiParameter("offering_money_value_off", "1");
request.AddApiParameter("period_start_time", "1626969600000");
request.AddApiParameter("limit", "1");
request.AddApiParameter("issued", "5");
request.AddApiParameter("max_discount_offering_money_value", "50");
request.AddApiParameter("offering_percentage_discount_off", "1");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/promotion/voucher/create')
request.add_api_parameter("criteria_over_money", "100")
request.add_api_parameter("voucher_type", "COLLECTIBLE_VOUCHER")
request.add_api_parameter("apply", "SPECIFIC_PRODUCTS")
request.add_api_parameter("collect_start", "1625649720000")
request.add_api_parameter("display_area", "REGULAR_CHANNEL")
request.add_api_parameter("period_end_time", "1630339199000")
request.add_api_parameter("voucher_name", "test voucher")
request.add_api_parameter("voucher_discount_type", "MONEY_VALUE_OFF")
request.add_api_parameter("offering_money_value_off", "1")
request.add_api_parameter("period_start_time", "1626969600000")
request.add_api_parameter("limit", "1")
request.add_api_parameter("issued", "5")
request.add_api_parameter("max_discount_offering_money_value", "50")
request.add_api_parameter("offering_percentage_discount_off", "1")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/promotion/voucher/create')
request.add_api_param('criteria_over_money', '100')
request.add_api_param('voucher_type', 'COLLECTIBLE_VOUCHER')
request.add_api_param('apply', 'SPECIFIC_PRODUCTS')
request.add_api_param('collect_start', '1625649720000')
request.add_api_param('display_area', 'REGULAR_CHANNEL')
request.add_api_param('period_end_time', '1630339199000')
request.add_api_param('voucher_name', 'test voucher')
request.add_api_param('voucher_discount_type', 'MONEY_VALUE_OFF')
request.add_api_param('offering_money_value_off', '1')
request.add_api_param('period_start_time', '1626969600000')
request.add_api_param('limit', '1')
request.add_api_param('issued', '5')
request.add_api_param('max_discount_offering_money_value', '50')
request.add_api_param('offering_percentage_discount_off', '1')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X POST url + '/promotion/voucher/create' \
-H 'Content-Type:application/x-www-form-urlencoded;charset=utf-8' \
-d 'app_key=12345678' \
-d 'timestamp=1655964758029' \
-d 'access_token=37c66819338b4562e17675b8c5c4dbd0' \
-d 'sign_method=sha256' \
-d 'sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC' \
-d 'criteria_over_money=100' \
-d 'voucher_type=COLLECTIBLE_VOUCHER' \
-d 'apply=SPECIFIC_PRODUCTS' \
-d 'collect_start=1625649720000' \
-d 'display_area=REGULAR_CHANNEL' \
-d 'period_end_time=1630339199000' \
-d 'voucher_name=test+voucher' \
-d 'voucher_discount_type=MONEY_VALUE_OFF' \
-d 'offering_money_value_off=1' \
-d 'period_start_time=1626969600000' \
-d 'limit=1' \
-d 'issued=5' \
-d 'max_discount_offering_money_value=50' \
-d 'offering_percentage_discount_off=1' \
```

### Response Example
---
```
{
  "error_msg": "null",
  "code": "0",
  "data": "9616200353530",
  "success": "true",
  "error_code": "null",
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
| 23	                | E023: xxxx	                | business validation error| 
| 21	                | E023: Internal System Error	| Internal System Error| 
| 24	                | E024: Parameter illegal	    | Parameter illegal| 
| 25	                | E025: UMP Exception	        | UMP Exception| 
| 26	                | E026: Seller Unauthorized	    | Seller Unauthorized| 

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)