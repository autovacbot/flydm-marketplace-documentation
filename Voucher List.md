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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/promotion/vouchers/get</Highlight1>

query seller voucher promotion list

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Philippines   | https://api.lazada.com.ph/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Vietnam       | https://api.lazada.vn/rest |
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
| cur_page      | Number   | false     | 1           |          | current page|
| voucher_type  | String   | <Highlight2>true</Highlight2>	| COLLECTIBLE_VOUCHER  |          | voucher type COLLECTIBLE_VOUCHER | CODE_VOUCHER|
| name          | String   | false	   | null        |          | promotion name|
| page_size     | Number   | false	   | 10          |          | page size|
| status        | String   | false	   | null        |          | NOT_START \ ONGOING \ SUSPEND \ FINISH|


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
| data                                  | Object     | response body                            | response body   |
| -total                                | Number	 | 234                                      | total |
| -current                              | Number	 | 1                                        | current page |
| -data_list                            | Object[]	 | data list                                | data list |
| --criteria_over_money                 | String     | 100                                      | Discount details, if order value reaches set value, will money discount or percentage discount|
| --apply                               | String	 | SPECIFIC_PRODUCTS                        | apply scope: ENTIRE_SHOP | SPECIFIC_PRODUCTS|
| --voucher_type                        | String	 | COLLECTIBLE_VOUCHER                      | Voucher type, COLLECTIBLE_VOUCHER | CODE_VOUCHER|
| --collect_start                       | Number	 | 1626969600000                            | The time that customers can collect the voucher|
| --display_area                        | String	 | REGULAR_CHANNEL                          | The area that customers can see the voucher REGULAR_CHANNEL\STORE_FOLLOWER\OFFLINE\LIVE_STREAM\SHARE_VOUCHER\CEM_SELLER|
| --period_end_time                     | Number	 | 1630339199000                            | The period end time that customers can use the voucher|
| --voucher_name                        | String 	 | test voucher                             | Voucher name|
| --voucher_discount_type               | String	 | MONEY_VALUE_OFF                          | Discount type|
| --offering_money_value_off            | String     | 1                                        | Discount details, if order value reaches criteria_over_money value, will discount money value|
| --period_start_time                   | Number	 | 1626969600000                            | The period start time that customers can use the voucher|
| --limit                               | Number	 | 1                                        | Voucher limit per customer|
| --order_used_budget                   | Number	 | 0                                        | Already used total|
| --currency                            | String	 | SGD                                      | Currency|
| --id                                  | Number	 | 91471121126083                           | Promotion ID |
| --issued                              | Number	 | 5                                        | Revision should be greater than the current setting|
| max_discount_offering_money_value     | String	 | null                                     | Discount details, if order value reaches criteria_over_money value, allow maximum discount per order, just support percentage discount off type |
| --voucher_code                        | String	 | null                                     | Voucher code |
| --offering_percentage_discount_off    | String	 | null                                     | Discount details, if order value reaches criteria_over_money value, will percentage discount off value|
| --status                              | String	 | SUSPEND                                  | Promotin status, NOT_START \ ONGOING \ SUSPEND \ FINISH|
| -page_size                            | Number	 | 10                                       | current page size|
| success                               | Boolean    | true                                     | success / fail |
| error_code                            | String	 | null                                     | error code |
| error_msg                             | String	 | null                                     | error message|

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/promotion/vouchers/get");
request.setHttpMethod("GET");
request.addApiParameter("cur_page", "1");
request.addApiParameter("voucher_type", "COLLECTIBLE_VOUCHER");
request.addApiParameter("name", "null");
request.addApiParameter("page_size", "10");
request.addApiParameter("status", "null");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/promotion/vouchers/get','GET');
$request->addApiParam('cur_page','1');
$request->addApiParam('voucher_type','COLLECTIBLE_VOUCHER');
$request->addApiParam('name','null');
$request->addApiParam('page_size','10');
$request->addApiParam('status','null');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/promotion/vouchers/get");
request.SetHttpMethod("GET");
request.AddApiParameter("cur_page", "1");
request.AddApiParameter("voucher_type", "COLLECTIBLE_VOUCHER");
request.AddApiParameter("name", "null");
request.AddApiParameter("page_size", "10");
request.AddApiParameter("status", "null");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/promotion/vouchers/get','GET')
request.add_api_parameter("cur_page", "1")
request.add_api_parameter("voucher_type", "COLLECTIBLE_VOUCHER")
request.add_api_parameter("name", "null")
request.add_api_parameter("page_size", "10")
request.add_api_parameter("status", "null")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/promotion/vouchers/get','GET')
request.add_api_param('cur_page', '1')
request.add_api_param('voucher_type', 'COLLECTIBLE_VOUCHER')
request.add_api_param('name', 'null')
request.add_api_param('page_size', '10')
request.add_api_param('status', 'null')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/promotion/vouchers/get?timestamp=1655971198572&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&cur_page=1&voucher_type=COLLECTIBLE_VOUCHER&name=null&page_size=10&status=null'
```

### Response Example
---
```
{
  "error_msg": "null",
  "code": "0",
  "data": {
    "data_list": [
      {
        "period_end_time": "1630339199000",
        "max_discount_offering_money_value": "null",
        "criteria_over_money": "100",
        "apply": "SPECIFIC_PRODUCTS",
        "voucher_name": "test voucher",
        "voucher_code": "null",
        "offering_money_value_off": "1",
        "order_used_budget": "0",
        "offering_percentage_discount_off": "null",
        "period_start_time": "1626969600000",
        "display_area": "REGULAR_CHANNEL",
        "voucher_type": "COLLECTIBLE_VOUCHER",
        "limit": "1",
        "collect_start": "1626969600000",
        "voucher_discount_type": "MONEY_VALUE_OFF",
        "currency": "SGD",
        "id": "91471121126083",
        "issued": "5",
        "status": "SUSPEND"
      },
      {
        "period_end_time": "1630339199000",
        "max_discount_offering_money_value": "null",
        "criteria_over_money": "100",
        "apply": "SPECIFIC_PRODUCTS",
        "voucher_name": "test voucher",
        "voucher_code": "null",
        "offering_money_value_off": "1",
        "order_used_budget": "0",
        "offering_percentage_discount_off": "null",
        "period_start_time": "1626969600000",
        "display_area": "REGULAR_CHANNEL",
        "voucher_type": "COLLECTIBLE_VOUCHER",
        "limit": "1",
        "collect_start": "1626969600000",
        "voucher_discount_type": "MONEY_VALUE_OFF",
        "currency": "SGD",
        "id": "91471121126083",
        "issued": "5",
        "status": "SUSPEND"
      }
    ],
    "total": "243",
    "current": "1",
    "page_size": "10"
  },
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
| 	| Query result is empty. 	      | |  

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)