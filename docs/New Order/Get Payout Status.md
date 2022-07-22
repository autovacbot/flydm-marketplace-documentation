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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/finance/payout/status/get</Highlight1>

Get your transaction statements created after the provided date

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Philippines   | https://api.lazada.com.ph/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Singapore     | https://api.lazada.sg/rest |
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
| - created_after  | String   | <Highlight2>true</Highlight2>      | 2018-01-01     |  | Filter statements created after the provided date. Mandatory.       |

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
| data                                  | Object[]   | data                                     | Response body    |
| -closing_balance                      | String     | 3962.41                                  | Closing balance          |
| -guarantee_deposit                    | String     | 0                                        | Guarantee deposit  |
| -payout                               | String     | 3962.41 EUR                              | Amount to be paid out to seller for statement          |
| -paid                                 | String     | 0                                        | Payout status of statement. 1 is paid, and 0 is not paid          |
| -statement_number                     | String     | EG100RT-20141228                         | When the statement was created   |
| -created_at                           | String     | 2018-01-04 00:23:04                      | Country          |
| -updated_at                           | String     | 2018-01-04 00:23:04                      | When the statement was last updated          |
| -opening_balance                      | String     | 0.00                                     | The opening balance          |
| -item_revenue                         | String     | 0                                        | The revenue generated by the item          |
| -shipment_fee                         | String     | 51.20                                    | Costs of shipping      |
| -shipment_fee_credit                  | String     | 51.20                                    | Shipping fee credit, if any       |
| -other_revenue_total                  | String     | 0                                        | Other total revenue          |
| -fees_total                           | String     | 51.20                                    | Sum of payment fee and return to seller fee          |
| -subtotal1                            | String     | 51.20                                    | Sum of item revenue and other revenue          |
| -refunds                              | String     | 0                                        | Sum of all refunds, if any          |
| -fees_on_refunds_total                | String     | 3432                                     | Accumulated fees on refunds issued          |
| -subtotal2                            | String     | 51.20                                    | (Sum of Subtotal1) - Refunds          |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/finance/payout/status/get");
request.setHttpMethod("GET");
request.addApiParameter("created_after", "2018-01-01");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/finance/payout/status/get','GET');
$request->addApiParam('created_after','2018-01-01');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/finance/payout/status/get");
request.SetHttpMethod("GET");
request.AddApiParameter("created_after", "2018-01-01");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/finance/payout/status/get','GET')
request.add_api_parameter("created_after", "2018-01-01")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/finance/payout/status/get','GET')
request.add_api_param('created_after', '2018-01-01')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/finance/payout/status/get?timestamp=1655700039133&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&created_after=2018-01-01'
```

### Response Example
---
```
{
  "code": "0",
  "data": [
    {
      "subtotal2": "51.20",
      "subtotal1": "51.20",
      "shipment_fee_credit": "51.20",
      "payout": "3962.41 EUR",
      "item_revenue": "0",
      "created_at": "2018-01-04 00:23:04",
      "other_revenue_total": "0",
      "fees_total": "51.20",
      "refunds": "0",
      "guarantee_deposit": "0",
      "updated_at": "2018-01-04 00:23:04",
      "fees_on_refunds_total": "0",
      "closing_balance": "3962.41",
      "paid": "0",
      "opening_balance": "0.00",
      "statement_number": "EG100RT-20141228",
      "shipment_fee": "51.20"
    },
    {
      "subtotal2": "51.20",
      "subtotal1": "51.20",
      "shipment_fee_credit": "51.20",
      "payout": "3962.41 EUR",
      "item_revenue": "0",
      "created_at": "2018-01-04 00:23:04",
      "other_revenue_total": "0",
      "fees_total": "51.20",
      "refunds": "0",
      "guarantee_deposit": "0",
      "updated_at": "2018-01-04 00:23:04",
      "fees_on_refunds_total": "0",
      "closing_balance": "3962.41",
      "paid": "0",
      "opening_balance": "0.00",
      "statement_number": "EG100RT-20141228",
      "shipment_fee": "51.20"
    }
  ],
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