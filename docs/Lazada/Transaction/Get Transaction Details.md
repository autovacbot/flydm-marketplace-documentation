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

<Highlight color="#00A854">POST</Highlight>  <Highlight1 color="#EEEEEE">/finance/transaction/accountTransactions/query</Highlight1>

Query Account Transactions

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Singapore     | https://api.lazada.sg/rest |
| Philippines   | https://api.lazada.com.ph/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Thailand      | https://api.lazada.co.th/rest |
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
| - transaction_type | String | false | Deposit | Enum Values: Deposit,Withdrawal,Payment,null | transaction type,Enumeration values for(Deposit,Withdrawal,Payment,null)       |
| - sub_transaction_type  | String   | false   | Deposit  |  | sub transaction type,Enumeration values for(Settlement,Failed Payment,Returned Payment,Auto Withdrawal,Manual Withdrawal,Sponsored Solutions Top-up,null)   
| - transaction_number | String | false | 1001   |  | transaction number   |
| - page_size  | Number   | <Highlight2>true</Highlight2>   | 10   | Default Value: 10 Regular Expression: ^\+?[1-9][0-9]*$ | page size | 
| - start_time | String | <Highlight2>true</Highlight2> | 20220601 | Regular Expression: ^\d{4}\d{1,2}\d{1,2} | start time,format:yyyyMMdd |
| - end_time  | String   | <Highlight2>true</Highlight2>   | 20220602   | Regular Expression: ^\d{4}\d{1,2}\d{1,2} | start time,format:yyyyMMdd   |
| - page_num  | Number   | <Highlight2>true</Highlight2>   | 1 | Default Value: 1 Regular Expression: ^\+?[1-9][0-9]*$ | page number   |

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
| msg                                   | String     | null                                     | error message | 
| data                                  | Object     | {""}                                     | result | 
| -page_info                            | Object     | {""}                                     | page Info |
| -page_num                             | Number     | 1                                        | pageNum | 
| --page_size                           | Number     | 10                                       | pageSize | 
| --total_page                          | Number     | 100                                      | totalPage |
| --total_count                         | Number     | 1000                                     | totalCount  |
| -transactions                         | Object[]   | []                                       | transactions  |
| --transaction_number                  | String     | 10000001                                 | trading serial number | 
| --transaction_time                    | String     | 2022-01-01 00:00:00                      | trading occurred time | 
| --type                                | String     | Penarikan Dana                           | trading type |
| --sub_type                            | String     | Penarikan Dana Otomatis                  | trading sub type |
| --payee_account                       | Object     | {""}                                     | payee Account |
| ---account                            | String     | 1001                                     | payee Account |
| ---description                        | String     | description                              | description |
| --amount                              | String     | ±0.01                                    | amount |
| --currency                            | String     | IDR                                      | currency |
| --remarks                             | String     | remarks                                  | remarks |
| --tracking_list                       | Object[]   | []                                       | tracking list |
| ---name                               | String     | WITHDRAWAL_INITIATED                     | The name of the state |
| ---status                             | String     | Penarikan Dana Dibuat                    | Configuration of multilingual copywriting | 
| ---update_time                        | String     | 2022-01-01 00:00:00                      | Update time | 
| ---remark                             | String     | remark                                   | remark |
| success                               | Boolean	 | true                                     | success:true,fail:false |
| error_code                            | String     | error_code                               | error code |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/finance/transaction/accountTransactions/query");
request.addApiParameter("transaction_type", "Deposit");
request.addApiParameter("sub_transaction_type", " Deposit");
request.addApiParameter("transaction_number", " 1001");
request.addApiParameter("page_size", "10");
request.addApiParameter("start_time", "20220601");
request.addApiParameter("end_time", "20220602");
request.addApiParameter("page_num", "1");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/finance/transaction/accountTransactions/query');
$request->addApiParam('transaction_type','Deposit');
$request->addApiParam('sub_transaction_type',' Deposit');
$request->addApiParam('transaction_number',' 1001');
$request->addApiParam('page_size','10');
$request->addApiParam('start_time','20220601');
$request->addApiParam('end_time','20220602');
$request->addApiParam('page_num','1');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/finance/transaction/accountTransactions/query");
request.AddApiParameter("transaction_type", "Deposit");
request.AddApiParameter("sub_transaction_type", " Deposit");
request.AddApiParameter("transaction_number", " 1001");
request.AddApiParameter("page_size", "10");
request.AddApiParameter("start_time", "20220601");
request.AddApiParameter("end_time", "20220602");
request.AddApiParameter("page_num", "1");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/finance/transaction/accountTransactions/query')
request.add_api_parameter("transaction_type", "Deposit")
request.add_api_parameter("sub_transaction_type", " Deposit")
request.add_api_parameter("transaction_number", " 1001")
request.add_api_parameter("page_size", "10")
request.add_api_parameter("start_time", "20220601")
request.add_api_parameter("end_time", "20220602")
request.add_api_parameter("page_num", "1")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/finance/transaction/accountTransactions/query')
request.add_api_param('transaction_type', 'Deposit')
request.add_api_param('sub_transaction_type', ' Deposit')
request.add_api_param('transaction_number', ' 1001')
request.add_api_param('page_size', '10')
request.add_api_param('start_time', '20220601')
request.add_api_param('end_time', '20220602')
request.add_api_param('page_num', '1')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X POST url + '/finance/transaction/accountTransactions/query' \
-H 'Content-Type:application/x-www-form-urlencoded;charset=utf-8' \
-d 'app_key=12345678' \
-d 'timestamp=1656312263813' \
-d 'access_token=37c66819338b4562e17675b8c5c4dbd0' \
-d 'sign_method=sha256' \
-d 'sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC' \
-d 'transaction_type=Deposit' \
-d 'sub_transaction_type=+Deposit' \
-d 'transaction_number=+1001' \
-d 'page_size=10' \
-d 'start_time=20220601' \
-d 'end_time=20220602' \
-d 'page_num=1' \
```

### Response Example
---
```
{
  "msg": "null",
  "code": "0",
  "data": {
    "page_info": {
      "total_count": "1000",
      "total_page": "100",
      "page_num": "1",
      "page_size": "10"
    },
    "transactions": [
      {
        "payee_account": {
          "description": "description",
          "account": "1001"
        },
        "amount": "±0.01",
        "sub_type": "Penarikan Dana Otomatis",
        "transaction_number": "10000001",
        "transaction_time": "2022-01-01 00:00:00",
        "currency": "IDR",
        "tracking_list": [
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          },
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          }
        ],
        "type": "Penarikan Dana",
        "remarks": " remarks"
      },
      {
        "payee_account": {
          "description": "description",
          "account": "1001"
        },
        "amount": "±0.01",
        "sub_type": "Penarikan Dana Otomatis",
        "transaction_number": "10000001",
        "transaction_time": "2022-01-01 00:00:00",
        "currency": "IDR",
        "tracking_list": [
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          },
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          }
        ],
        "type": "Penarikan Dana",
        "remarks": " remarks"
      }
    ]
  },
  "success": "true",
  "error_code": " error_code",
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