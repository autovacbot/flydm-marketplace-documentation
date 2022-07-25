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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/products/get</Highlight1>

Use this API to get detailed information of the specified products.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Philippines   | https://api.lazada.com.ph/rest |
| Singapore     | https://api.lazada.sg/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Thailand      | https://api.lazada.co.th/rest |
| Indonesia     | https://api.lazada.co.id/rest |
| Vietnam       | https://api.lazada.vn/rest |

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
| - filter      | String   | false     | live        |          | Returns the products with the status matching this parameter. Possible values are all, live, inactive, deleted, pending, rejected, sold-out. Mandatory. |
| - update_before      | String   | false     | 2018-01-01T00:00:00+0800  |          | Limits the returned product list to those updated before or on a specified date, given in ISO 8601 date format. Optional |
| - create_before      | String   | false     | 2018-01-01T00:00:00+0800        |          | 	
Limits the returned products to those created before or on the specified date, given in ISO 8601 date format. Optional |
| - offset      | String   | false     | 0        |          | Deprecated(The number of Items you want to skip before you start counting),It is recommended to use date for scrolling query.The maximum offset is 10000 |
| - create_after      | String   | false     | 2010-01-01T00:00:00+0800        |          | Limits the returned products to those created after or on the specified date, given in ISO 8601 date format. Optional |
| - update_after | String   | false     | 2010-01-01T00:00:00+0800  |          | Limits the returned products to those updated after or on the specified date, given in ISO 8601 date format. Optional |
| - limit       | String   | false     | 50        |         | The number of Items you would like to fetch from every response,The maximum is 50. |
| - options     | String   | false     | 1        |          | This value can be used to get more stock information. e.g., Options=1 means contain ReservedStock, RtsStock, PendingStock, RealTimeStock, FulfillmentBySellable. |
| - sku_seller_list      | String   | false     | ["39817:01:01", "Apple 6S Black"] |          | Only products that have the Seller SKU in this list will be returned. Input should be a JSON array. For example, ["Apple 6S Gold", "Apple 6S Black"]. It only matches the whole words. A maximum of 100 SKUs can be returned. |

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
| data                                  | Object     | {"data":{"created_time":"1645176573000","updated_time":"1653463851000","images":["https://my-live.slatic.net/p/58a4f48c8e5d526ba0f4ee2150dff8ab.jpg"],"skus":[{"Status":"active","quantity":20,"Images":[],"SellerSku":"12333-poi","ShopSku":"2807246166_MY-13449296008","Url":"https://www.lazada.com.my/-i2807246166-s13449296008.html","multiWarehouseInventories":[{"occupyQuantity":0,"quantity":20,"totalQuantity":20,"withholdQuantity":0,"warehouseCode":"dropshipping","sellableQuantity":20}],"package_width":"10.00","package_height":"10.00","fblWarehouseInventories":[],"special_price":0.0,"price":102.0,"channelInventories":[{"channelName":"4a9198e3-9b40-44d2-a6b6-863696c42f74","startTime":"2022-05-28 00:00:00","endTime":"2022-05-30 23:59:59","sellableQuantity":1},{"channelName":"9e46b6eb-a509-4db1-a22c-7ad266ac4a74","startTime":"2022-02-25 00:00:00","endTime":"2022-02-26 00:00:00","sellableQuantity":7}],"package_length":"10.00","package_weight":"0.3","Available":20,"SkuId":13449296008}],"item_id":2807246166,"variation":{},"trialProduct":false,"primary_category":8707,"marketImages":[],"attributes":{"name":"#TEST TITLE#$2022-02-18 15:21:16&","short_description":"1234","description":" 123321","video":"30000176356","brand":"NAVIFORCE","model":"9095","movement":"Quartz","feature":"Date,Luminous,Chronograph,World Time,Calculator,Calendar,Shock Resistant","movement_country":"Japan","water_resistant":"30m","case_shape":"Round","Dial_Glass":"Hesalite Crystal","watch_dial_size":"Other","strap":"Leather","warranty_type":"No Warranty","name_ms":"# Ujian Tajuk #2022-02-18 15:21:16","source":"asc","delivery_option_sof":"0"},"status":"Active"},"code":"0","request_id":"21017d2816548274295911740"} | Response body   |
| -total_products                       | Number     | 10 | The number of total Items, it's item level.   |
| -products                             | Object[]   | [] | An array contains at least one Product.   |
| --primary_category                    | Number     | 10000211                                   | The ID of the primary category for his product.   |
| --attributes                   | Object     | { "description": " asd \n",           "name": "asd",           "brand": "Asante",          "short_description": " asdasd ",           "warranty_type": "International Manufacturer"}  | Seller Center identification.  Optional, please ignore it if your business scenario does not cover it.  |
| --skus               | Object[]     | [ { "Status":"active", "SkuId": 314525867, "quantity":0, "product_weight":"0.03", "Images":["http://sg-live-01.slatic.net/p/BUYI1-catalog.jpg","","","","","","",""], "SellerSku":"39817:01:01", "ShopSku":"BU565ELAX8AGSGAMZ-1104491", "Url":"https://alice.lazada.sg/asd-1083832.html", "package_width":"10.00", "special_to_time":"2020-02-0300:00", "special_from_time":"2015-07-3100:00", "package_height":"4.00", "special_price":9, "price":32, "package_length":"10.00", "package_weight":"0.04", "Available":0, "special_to_date":"2020-02-03" } ]  | An array contains at least one SKU.    |
| --item_id                   | Number     | 180226526  | The ID of this product  |
| --The ID of this product    | String     | 1611554725000  | create time  |
| --updated_time              | String     | 1611554725000  | update time  |
| --images                    | Object     | [     "https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg",     "https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg" ]  | product images  |
| --marketImages              | String     | [     "https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg",     "https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg" ]  | product market images  |
| --status                    | String     | Active,InActive,Pending QC,Suspended,Deleted  | product status  |
| --subStatus                 | Object     | Lock,Reject,Live Reject,Admin  | product reject status  |
| --suspendedSkus             | Object[]   | "suspendedSkus":[{"rejectReason":"Possible counterfeit. Please provide proof of authenticity in order to reactivate your product. Refer to this link for more info: https://goo.gl/YjeXER:null", "SellerSku":"2142206567-1640869121385-0", "SkuId":12185089556}]  | An array contains at least one Suspended SKU. |
| --trialProduct              | Boolean    | false  | Whether product is trial product  |


### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/products/get");
request.setHttpMethod("GET");
request.addApiParameter("filter", "live");
request.addApiParameter("update_before", "2018-01-01T00:00:00+0800");
request.addApiParameter("create_before", "2018-01-01T00:00:00+0800");
request.addApiParameter("offset", "0");
request.addApiParameter("create_after", "2010-01-01T00:00:00+0800");
request.addApiParameter("update_after", "2010-01-01T00:00:00+0800");
request.addApiParameter("limit", "10");
request.addApiParameter("options", "1");
request.addApiParameter("sku_seller_list", " [\"39817:01:01\", \"Apple 6S Black\"]");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/products/get','GET');
$request->addApiParam('filter','live');
$request->addApiParam('update_before','2018-01-01T00:00:00+0800');
$request->addApiParam('create_before','2018-01-01T00:00:00+0800');
$request->addApiParam('offset','0');
$request->addApiParam('create_after','2010-01-01T00:00:00+0800');
$request->addApiParam('update_after','2010-01-01T00:00:00+0800');
$request->addApiParam('limit','10');
$request->addApiParam('options','1');
$request->addApiParam('sku_seller_list',' [\"39817:01:01\", \"Apple 6S Black\"]');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/products/get");
request.SetHttpMethod("GET");
request.AddApiParameter("filter", "live");
request.AddApiParameter("update_before", "2018-01-01T00:00:00+0800");
request.AddApiParameter("create_before", "2018-01-01T00:00:00+0800");
request.AddApiParameter("offset", "0");
request.AddApiParameter("create_after", "2010-01-01T00:00:00+0800");
request.AddApiParameter("update_after", "2010-01-01T00:00:00+0800");
request.AddApiParameter("limit", "10");
request.AddApiParameter("options", "1");
request.AddApiParameter("sku_seller_list", " [\"39817:01:01\", \"Apple 6S Black\"]");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);

```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/products/get','GET')
request.add_api_parameter("filter", "live")
request.add_api_parameter("update_before", "2018-01-01T00:00:00+0800")
request.add_api_parameter("create_before", "2018-01-01T00:00:00+0800")
request.add_api_parameter("offset", "0")
request.add_api_parameter("create_after", "2010-01-01T00:00:00+0800")
request.add_api_parameter("update_after", "2010-01-01T00:00:00+0800")
request.add_api_parameter("limit", "10")
request.add_api_parameter("options", "1")
request.add_api_parameter("sku_seller_list", " [\"39817:01:01\", \"Apple 6S Black\"]")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/products/get','GET')
request.add_api_param('filter', 'live')
request.add_api_param('update_before', '2018-01-01T00:00:00+0800')
request.add_api_param('create_before', '2018-01-01T00:00:00+0800')
request.add_api_param('offset', '0')
request.add_api_param('create_after', '2010-01-01T00:00:00+0800')
request.add_api_param('update_after', '2010-01-01T00:00:00+0800')
request.add_api_param('limit', '10')
request.add_api_param('options', '1')
request.add_api_param('sku_seller_list', ' [\"39817:01:01\", \"Apple 6S Black\"]')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/products/get?timestamp=1655866493615&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&filter=live&update_before=2018-01-01T00%3A00%3A00%2B0800&create_before=2018-01-01T00%3A00%3A00%2B0800&offset=0&create_after=2010-01-01T00%3A00%3A00%2B0800&update_after=2010-01-01T00%3A00%3A00%2B0800&limit=10&options=1&sku_seller_list=+%5B%2239817%3A01%3A01%22%2C+%22Apple+6S+Black%22%5D'
```

### Response Example
---
```
{
  "code": "0",
  "data": {
    "total_products": "10",
    "products": [
      {
        "trialProduct": "false",
        "created_time": "1611554725000",
        "updated_time": "1611554725000",
        "images": "[     \"https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg\",     \"https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg\" ]",
        "skus": [
          {
            "Status": "active",
            "quantity": 0,
            "product_weight": "0.03",
            "Images": [
              "http://sg-live-01.slatic.net/p/BUYI1-catalog.jpg",
              "",
              "",
              "",
              "",
              "",
              "",
              ""
            ],
            "SellerSku": "39817:01:01",
            "ShopSku": "BU565ELAX8AGSGAMZ-1104491",
            "Url": "https://alice.lazada.sg/asd-1083832.html",
            "package_width": "10.00",
            "special_to_time": "2020-02-0300:00",
            "special_from_time": "2015-07-3100:00",
            "package_height": "4.00",
            "special_price": 9,
            "price": 32,
            "package_length": "10.00",
            "package_weight": "0.04",
            "Available": 0,
            "SkuId": 314525867,
            "special_to_date": "2020-02-03"
          }
        ],
        "item_id": "180226526",
        "primary_category": "10000211",
        "marketImages": "[     \"https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg\",     \"https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg\" ]",
        "attributes": {
          "short_description": "\u003cul\u003e\u003cli\u003easdasd\u003c/li\u003e\u003c/ul\u003e",
          "name": "asd",
          "description": "\u003cp\u003easd\u003c/p\u003e\n",
          "warranty_type": "International Manufacturer",
          "brand": "Asante"
        },
        "suspendedSkus": [],
        "subStatus": "Lock,Reject,Live Reject,Admin",
        "status": "Active,InActive,Pending QC,Suspended,Deleted"
      },
      {
        "trialProduct": "false",
        "created_time": "1611554725000",
        "updated_time": "1611554725000",
        "images": "[     \"https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg\",     \"https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg\" ]",
        "skus": [
          {
            "Status": "active",
            "quantity": 0,
            "product_weight": "0.03",
            "Images": [
              "http://sg-live-01.slatic.net/p/BUYI1-catalog.jpg",
              "",
              "",
              "",
              "",
              "",
              "",
              ""
            ],
            "SellerSku": "39817:01:01",
            "ShopSku": "BU565ELAX8AGSGAMZ-1104491",
            "Url": "https://alice.lazada.sg/asd-1083832.html",
            "package_width": "10.00",
            "special_to_time": "2020-02-0300:00",
            "special_from_time": "2015-07-3100:00",
            "package_height": "4.00",
            "special_price": 9,
            "price": 32,
            "package_length": "10.00",
            "package_weight": "0.04",
            "Available": 0,
            "SkuId": 314525867,
            "special_to_date": "2020-02-03"
          }
        ],
        "item_id": "180226526",
        "primary_category": "10000211",
        "marketImages": "[     \"https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg\",     \"https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg\" ]",
        "attributes": {
          "short_description": "\u003cul\u003e\u003cli\u003easdasd\u003c/li\u003e\u003c/ul\u003e",
          "name": "asd",
          "description": "\u003cp\u003easd\u003c/p\u003e\n",
          "warranty_type": "International Manufacturer",
          "brand": "Asante"
        },
        "suspendedSkus": [],
        "subStatus": "Lock,Reject,Live Reject,Admin",
        "status": "Active,InActive,Pending QC,Suspended,Deleted"
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
| 5                 | E005: Invalid Request Format	    | The request URL is not valid.|
| 6	                | E006: Unexpected internal error	| Unexpected internal error.|
| 14                | E014: "%s" Invalid Offset	        | The value for the offset parameter is not valid.|
| 17	            | E017: "%s" Invalid Date Format	| The date format is not valid.|
| 19	            | E019: "%s" Invalid Limit	        | The value for the limit parameter is not valid.|
| 36	            | E036: Invalid status filter	    | The specified status filter is not valid.|
| 70	            | E070: You have corrupt dat a in your sku seller list.	| Data in the SKU list are not valid.
| 506	            | E506: Get product failed	        | Failed to get the product information.|
| 901	            |E901: The request is too frequent, or the requested functionality is temporarily disabled.	| Failed to return the requested data due to high calling frequency or disabled functionality. Please try again later. |

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)