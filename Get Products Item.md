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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/product/item/get</Highlight1>

Get single product by ItemId or SellerSku.

### Common Parameters
---
#### Service Endpoints

| Region        | Endpoint |
| :---          | :----    |
| Indonesia     | https://api.lazada.co.id/rest |
| Malaysia      | https://api.lazada.com.my/rest |
| Vietnam       | https://api.lazada.vn/rest |
| Singapore     | https://api.lazada.sg/rest |
| Thailand      | https://api.lazada.co.th/rest |
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
| - item_id     | Number   | false     | 692345699   |          | Item Id |
| - seller_sku  | String   | false     | Apple-6S-Black  |          | Seller Sku |


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
| -suspendedSkus                        | Object[]     | "suspendedSkus":[{"rejectReason":"Possible counterfeit. Please provide proof of authenticity in order to reactivate your product. Refer to this link for more info: https://goo.gl/YjeXER:null", "SellerSku":"2142206567-1640869121385-0", "SkuId":12185089556}] | An array contains at least one Suspended SKU.    |
| -variation                            | Object     | [] | self define attributes   |
| --variation1                          | Object     | [] | self define attributes   |
| ---name                               | String     | color_family  | self define attributes  |
| ---has_image                          | Boolean    | red           | self define attributes  |
| ---customize                          | Boolean    | true          | self define attributes  |
| ---options                            | String[]   | false         | self define attributes  |
| ---label                              | String     | color         | self define attributes  |
| --variation2                          | Object     | []            | self define attributes   |
| ---name                               | String     | SizeX  | self define attributes  |
| ---has_image                          | Boolean    | false           | self define attributes  |
| ---customize                          | Boolean    | true          | self define attributes  |
| ---options                            | String[]   | ss         | self define attributes  |
| ---label                              | String     | color         | self define attributes  |
| --variation3                          | Object     | [] | self define attributes   |
| ---name                               | String     | Volume  | self define attributes  |
| ---has_image                          | Boolean    | false           | self define attributes  |
| ---customize                          | Boolean    | false          | self define attributes  |
| ---options                            | String[]   | 100ml         | self define attributes  |
| ---label                              | String     | color         | self define attributes  |
| --variation4                          | Object     | [] | self define attributes   |
| ---name                               | String     | Size  | self define attributes  |
| ---has_image                          | Boolean    | false           | self define attributes  |
| ---customize                          | Boolean    | false          | self define attributes  |
| ---options                            | String[]   | m         | self define attributes  |
| ---label                              | String     | color         | self define attributes  |
| -primary_category                     | Number     | 10000211 | CategoryId   |
| -attributes                           | Object     | [     {         "Status": "active",         "SkuId": 314525867,         "quantity": 0,         "product_weight": "0.03",         "Images": [             "http://sg-live-01.slatic.net/p/BUYI1-catalog.jpg",             "",             "",             "",             "",             "",             "",             ""         ],         "SellerSku": "39817:01:01",         "ShopSku": "BU565ELAX8AGSGAMZ-1104491",         "Url": "https://alice.lazada.sg/asd-1083832.html",         "package_width": "10.00",         "special_to_time": "2020-02-0300:00",         "special_from_time": "2015-07-3100:00",         "package_height": "4.00",         "special_price": 9,         "price": 32,         "package_length": "10.00",         "package_weight": "0.04",         "Available": 0,         "special_to_date": "2020-02-03",         "multiWarehouseInventories":[          {              "warehouseCode":"warehouseTest1",              "quantity": 20          },         {              "warehouseCode":"warehouseTest2",              "quantity": 30          }         ]     } ] | Item attributes.   |
| -skus                                 | Object[]     | [     {         "Status": "active",         "SkuId": 314525867,         "quantity": 0,         "product_weight": "0.03",         "Images": [             "http://sg-live-01.slatic.net/p/BUYI1-catalog.jpg",             "",             "",             "",             "",             "",             "",             ""         ],         "SellerSku": "39817:01:01",         "ShopSku": "BU565ELAX8AGSGAMZ-1104491",         "Url": "https://alice.lazada.sg/asd-1083832.html",         "package_width": "10.00",         "special_to_time": "2020-02-0300:00",         "special_from_time": "2015-07-3100:00",         "package_height": "4.00",         "special_price": 9,         "price": 32,         "package_length": "10.00",         "package_weight": "0.04",         "Available": 0,         "special_to_date": "2020-02-03",         "multiWarehouseInventories":[          {              "warehouseCode":"warehouseTest1",              "quantity": 20          },         {              "warehouseCode":"warehouseTest2",              "quantity": 30          }         ]     } ] | Sku List   |
| -item_id                              | Number     | 234222211 | Item Id   |
| -created_time                         | String     | 1611554725000 | create time   |
| -updated_time                         | String     | 1611554725000 | update time   |
| -images                               | String     | [ "https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg",     "https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg" ] | product images List   |
| -marketImages                         | String     | [ "https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg",     "https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg" ] | product market images    |
| -status                               | String     | Active,InActive,Pending QC,Suspended,Deleted | product status   |
| -trialProduct                         | Boolean     | true,false | trial product   |
| -subStatus                            | String     | Lock,Reject,Live_Reject,Admin | product reject status   |


### Request Example
---
```md title="JAVA"
LazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.setApiName("/product/item/get");
request.setHttpMethod("GET");
request.addApiParameter("item_id", "692345699");
request.addApiParameter("seller_sku", "Apple-6S-Black");
LazopResponse response = client.execute(request, accessToken);
System.out.println(response.getBody());
Thread.sleep(10);
```

```md title="PHP"
$c = new LazopClient(url,appkey,appSecret);
$request = new LazopRequest('/product/item/get','GET');
$request->addApiParam('item_id','692345699');
$request->addApiParam('seller_sku','Apple-6S-Black');
var_dump($c->execute($request, $accessToken));
```

```md title=".NET"
ILazopClient client = new LazopClient(url, appkey, appSecret);
LazopRequest request = new LazopRequest();
request.SetApiName("/product/item/get");
request.SetHttpMethod("GET");
request.AddApiParameter("item_id", "692345699");
request.AddApiParameter("seller_sku", "Apple-6S-Black");
LazopResponse response = client.Execute(request, accessToken);
Console.WriteLine(response.IsError());
Console.WriteLine(response.Body);

```

```md title="RUBY"
client = LazopApiClient::Client.new(url, appkey, appSecret)
request = LazopApiClient::Request.new('/product/item/get','GET')
request.add_api_parameter("item_id", "692345699")
request.add_api_parameter("seller_sku", "Apple-6S-Black")
response = client.execute(request, accessToken)
puts response.success?
puts response.body
```

```md title="PYTHON"
client = lazop.LazopClient(url, appkey ,appSecret)
request = lazop.LazopRequest('/product/item/get','GET')
request.add_api_param('item_id', '692345699')
request.add_api_param('seller_sku', 'Apple-6S-Black')
response = client.execute(request, access_token)
print(response.type)
print(response.body)
```

```md title="CURL"
curl -X GET url + '/product/item/get?timestamp=1655868811278&app_key=12345678&sign_method=sha256&sign=D13F2A03BE94D9AAE9F933FFA7B13E0A5AD84A3DAEBC62A458A3C382EC2E91EC&access_token=37c66819338b4562e17675b8c5c4dbd0&item_id=692345699&seller_sku=Apple-6S-Black'
```

### Response Example
---
```
{
  "code": "0",
  "data": {
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
        "multiWarehouseInventories": [
          {
            "quantity": 20,
            "warehouseCode": "warehouseTest1"
          },
          {
            "quantity": 30,
            "warehouseCode": "warehouseTest2"
          }
        ],
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
    "item_id": "234222211",
    "suspendedSkus": [],
    "variation": {
      "variation3": {
        "has_image": "false",
        "name": "Volume",
        "options": [
          "100ml",
          "100ml"
        ],
        "label": "color",
        "customize": "false"
      },
      "variation4": {
        "has_image": "false",
        "name": "Size",
        "options": [
          "m",
          "m"
        ],
        "label": "color",
        "customize": "false"
      },
      "variation1": {
        "has_image": "red",
        "name": "color_family",
        "options": [
          "false",
          "false"
        ],
        "label": "color",
        "customize": "true"
      },
      "variation2": {
        "has_image": "false",
        "name": "SizeX",
        "options": [
          "ss",
          "ss"
        ],
        "label": "color",
        "customize": "true"
      }
    },
    "subStatus": "Lock,Reject,Live_Reject,Admin",
    "trialProduct": "true,false",
    "primary_category": "10000211",
    "marketImages": "[     \"https://my-live.slatic.net/p/540bc796d1eadf316018038d8840f20a.jpg\",     \"https://my-live.slatic.net/p/8913fc357e139ef78ad2f071e9586334.jpg\" ]",
    "attributes": {
      "short_description": "\u003cul\u003e\u003cli\u003easdasd\u003c/li\u003e\u003c/ul\u003e",
      "name": "asd",
      "description": "\u003cp\u003easd\u003c/p\u003e\n",
      "warranty_type": "International Manufacturer",
      "brand": "Asante"
    },
    "status": "Active,InActive,Pending QC,Suspended,Deleted"
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
| 200	            | E200: Empty SellerSku	            | Empty Item Id and Seller Sku.|
| 207	            | E207: SKU not exist	            | Cannot find a Sku by the Seller Sku.|
| 208	            | E208: Item not exist	            | Cannot find a Item by the Item Id.|

### API Test Tools
---
[API Test Tool](https://iopaccount.lazada.com/login?redirect_url=http://open.lazada.com/app/index.htm#/api/test?apiPath=%2Forder%2Fget&appkey=100132)