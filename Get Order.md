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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/get</Highlight1>

Use this API to get the list of items for a single order.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Vietnam       | https://api.lazada.vn/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Singapore     | https://api.lazada.sg/rest |
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
| - order_id    | Number   | <Highlight2>true</Highlight2>      | 16090         |  | The identifier that was assigned to the order by the Seller Center           |

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
| data                                  | Object     | {}                                       | Responsebody body    |
|-address_shipping                      | Object     | 1                                        | Node that contains additional nodes, which makes up the shipping address: FirstName, LastName, Phone, Phone2, Address1, Address2, City, PostCode, and Country.          |
| --address5                            | String     | 1******2                                 | Third-level address  |
| --postcode                            | String     | 247979                                   | Post code; Note: This value will not be used in Lazada ID          |
| --address4                            | String     | address4                                 | City name          |
| --last_name                           | String     | Last Name                                | Customer last name          |
| --country                             | String     | Singapore                                | Country          |
| --address3                            | String     | address3                                 | State name          |
| --address2                            | String     | address2                                 | Not used for now          |
| --city                                | String     | Singapore-Central                        | City name          |
| --address1                            | String     | 318 tanglin road, phoenix park, #01-59   | Detailed address      |
| --phone2                              | String     | 1******2                                 | Backup phone number          |
| --first_name                          | String     | First Name                               | Customer first name          |
| --phone                               | String     | 94236248                                 | Phone number          |
| -customer_last_name                   | String     | last_name                                | Customer last name          |
| -gift_option                          | Boolean    | 0                                        | 1 if item is a gift, and 0 if it is not.          |
| -voucher_code                         | String     | 3432                                     | Voucher code          |
| -updated_at                           | String     | 2014-10-15 18:36:05 +0800                | Date and time of the last change to the order.          |
| -delivery_info                        | String     | 1                                        | Order delivery information.          |
| -gift_message                         | String     | Gift                                     | Gift message as specified by the customer         |
| -branch_number                        | String     | 2222                                     | (For Thailand only) The tax branch code for corporate customers, provided by the customer when placing the order.         |
| -tax_code                             | String     | 1234                                     | (For Thailand and Vietnam only) The customer's VAT tax code, provided by the customer when placing the order.         |
| -extra_attributes                     | String     | {"TaxInvoiceRequested":"true"}           | Extra attributes which were passed to the Seller Center on getMarketPlaceOrders call.          |
| -shipping_fee                         | String     | 0.00                                     | Shipping fee          |
| -customer_first_name                  | String     | First Name                               | Customer first name.         |
| -payment_method                       | String     | COD                                      | The method of payment.           |
| -statuses                             | String[]   | delivered                                | Unique status of the items in the order          |
| -remarks                              | String     | remarks                                  | OA human-readable remark          |
| -order_number                         | Number     | 300034416                                | The order number          |
| -order_id                             | Number     | 16090                                    | Identifier of this order as assigned by the Seller Center          |
| -voucher                              | String     | 0.00                                     | Voucher amount          |
| -national_registration_numberC        | String     | 1123                                     | Required in some countries          |
| -promised_shipping_times              | String     | 2017-03-24 16:09:22                      | Promised shipping time     |
| -items_count                          | Number     | 1                                        | Number of items in the order       |
| -created_at                           | String     | 2014-10-15 18:36:05 +0800                | Date and time when the order was placed    |
| -price                                | String     | 99.00                                    | Total amount for this order          |
| -address_billing                      | Object     | {}                                       | 	Node that contains additional nodes, which makes up the shipping address: FirstName, LastName, Phone, Phone2, Address1, Address2, City, PostCode, and Country          |
| --address3                            | String     | address3                                 | State name          |
| --address2                            | String     | address2                                 | Not used for now          |
| --city                                | String     | Singapore-Central                        | City name          |
| --address1                            | String     | 22 leonie hill road, #13-01              | Detailed address          |
| --phone2                              | String     | 24***22                                  | Backup phone number          |
| --first_name                          | String     | First Name                               | Customer first name          |
| --phone                               | String     | 81***8                                   | Phone number          |
| --address5                            | String     | address5                                 | Third-level address          |
| --post_code                           | String     | 239195                                   | Post code; Note: This value will not be used in Lazada ID          |
| --address4                            | String     | address4                                 | City name          |
| --last_name                           | String     | Last Name                                | Customer last name          |
| --country                             | String     | Singapore                                | Country          |
| -warehouse_code                       | String     | dropshipping                             | Warehouse Code of multi-wh sellers          |
| -shipping_fee_original                | String     | 0.00                                     | shipping fee original          |
| -shipping_fee_discount_seller         | String     | 0.00                                     | shipping fee discount from seller          |
| -shipping_fee_discount_platform       | String     | 0.00                                     | shipping fee discount from platform          |

### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/order/get");
request.setHttpMethod("GET");
request.addApiParameter("order_id", "16090");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/order/get','GET');
$request->addApiParam('order_id','16090');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/order/get");
request.SetHttpMethod("GET");
request.AddApiParameter("order_id", "16090");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);
```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/order/get','GET')
request.add_api_parameter("order_id", "16090")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/order/get','GET')
request.add_api_param('order_id', '16090')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/order/get?timestamp=1655532205138&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&order_id=16090'
```

### Response Example
---
```
{
  "code": "0",
  "data": {
    "voucher": "0.00",
    "warehouse_code": "dropshipping",
    "order_number": "300034416",
    "created_at": "2014-10-15 18:36:05 +0800",
    "voucher_code": "3432",
    "gift_option": "0",
    "shipping_fee_discount_platform": "0.00",
    "customer_last_name": "last_name",
    "updated_at": "2014-10-15 18:36:05 +0800",
    "promised_shipping_times": "2017-03-24 16:09:22",
    "price": "99.00",
    "national_registration_number": "1123",
    "shipping_fee_original": "0.00",
    "payment_method": "COD",
    "customer_first_name": "First Name",
    "shipping_fee_discount_seller": "0.00",
    "shipping_fee": "0.00",
    "branch_number": "2222",
    "tax_code": "1234",
    "items_count": "1",
    "delivery_info": "1",
    "statuses": [
      "delivered",
      "delivered"
    ],
    "address_billing": {
      "country": "Singapore",
      "address3": "address3",
      "address2": "address2",
      "city": "Singapore-Central",
      "phone": "81***8",
      "address1": "22 leonie hill road, #13-01",
      "post_code": "239195",
      "phone2": "24***22",
      "last_name": "Last Name",
      "address5": "address5",
      "address4": "address4",
      "first_name": "First Name"
    },
    "extra_attributes": "{\"TaxInvoiceRequested\":\"true\"}",
    "order_id": "16090",
    "gift_message": "Gift",
    "remarks": "remarks",
    "address_shipping": {
      "country": "Singapore",
      "address3": "address3",
      "address2": "address2",
      "city": "Singapore-Central",
      "phone": "94236248",
      "address1": "318 tanglin road, phoenix park, #01-59",
      "post_code": "247979",
      "phone2": "1******2",
      "last_name": "Last Name",
      "address5": "1******2",
      "address4": "address4",
      "first_name": "First Name"
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
| Error Code        | 	Error Message               | Description        |
| :---              | :---                          | :---               |
| 16                | E016: "%s" Invalid Order ID   | The specified order ID is not valid.    |
| 6                 | E006: System Error            | System Error    |

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)