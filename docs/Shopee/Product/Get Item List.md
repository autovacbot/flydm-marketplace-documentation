---
sidebar_position: 1
---

# Get Item List

```
GET /api/v2/product/get_item_list
```
Use this call to get a list of items

## Common Parameters

| Name    | Type | Sample | Description    |
| :------ | :--- | :----- | :------------- |
| shop_id | int  | 123456 | Store Shop ID. |

## Request Parameters

export const Highlight = ({children, color}) => (
  <span
    style={{
      backgroundColor: color,
      color: '#00ff00',
    }}>
    {children}
  </span>
);

export const Highlight1 = ({children, color}) => (
  <span
    style={{
      backgroundColor: color,
      color: '#FF5F1F',
    }}>
    {children}
  </span>
);

|       Name       |    Type    |          Required           |      Sample    | Description |
|       :---       |    :---    |            :---             |       :---     | :--- |
|      offset      |     int    | <Highlight>True</Highlight> |        0       | Specifies the starting entry of data to return in the current call. Default is 0. if data is more than one page, the offset can be some entry to start next call. |
|     page_size    |     int    | <Highlight>True</Highlight> |        10      | the size of one page.Max=100 |
| update_time_from |  timestamp | <Highlight1>False</Highlight1> |   1611311600   |The update_time_from and update_time_to fields specify a date range for retrieving orders (based on the item update time). The update_time_from field is the starting date range. |
|  update_time_to  |  timestamp | <Highlight1>False</Highlight1> |   1611311631   | The update_time_from and update_time_to fields specify a date range for retrieving orders (based on the item update time). The update_time_to field is the ending date range |
|    item_status   |  string[]  | <Highlight>True</Highlight> |   ["NORMAL"]   | NORMAL/BANNED/DELETED/UNLIST If you want to search multiple status, please upload the url like this: item_status=NORMAL&item_status=BANNED |

## Response Parameters

|         Name      |   Type    |             Sample               | Description |
|         :---      |   :---    |             :---                 | :--- |
|         error     |   string  |                                  | Indicate error type if hit error. Empty if no error happened. |
|        message    |   string  |                                  | Indicate error details if hit error. Empty if no error happened. |
|        warning    |   string  |                                  | Indicate waring details if hit waring. Empty if no waring happened. |
|       request_id  |   string  | 7b9da0c6926642199c33ee9dd3a266f5 | The identifier for an API request for error tracking |
|       -response   |   object  |                                  |  |
|        --item     | object[]  |                                  | list of item info with item_id/ item_status/ update_time |
|      ---item_id   |    int    |             2500139861           | Shopee's unique identifier for an item. |
|    ---item_status |   string  |              NORMAL              | Enumerated type that defines the current status of the item. Applicable values: NORMAL, DELETED, UNLIST and BANNED. |
|   ---update_time  | timestamp |            1608128470            | The update time of item. |
|   --total_count   |    int    |                10                | total count of all items |
|   --has_next_page |  boolean  |               true               | This is to indicate whether the item list is more than one page. If this value is true, you may want to continue to check next page to retrieve the rest of items. |
|   --next_offset   |    int    |                10                | if has_next_page is true, this value need set to next request.offset |

## Request Example

```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("https://partner.shopeemobile.com/api/v2/product/get_item_list?page_size=10&item_status=NORMAL&offset=0&partner_id=partner_id&access_token=access_token&timestamp=timestamp&update_time_from=1611311600&update_time_to=1611311631&sign=sign&shop_id=shop_id")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/product/get_item_list?access_token=access_token&item_status=NORMAL&offset=0&page_size=10&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp&update_time_from=1611311600&update_time_to=1611311631',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```js title="cURL"

curl --location --request GET 'https://partner.shopeemobile.com/api/v2/product/get_item_list?access_token=access_token&timestamp=timestamp&update_time_from=1611311600&page_size=10&item_status=NORMAL&offset=0&partner_id=partner_id&update_time_to=1611311631&sign=sign&shop_id=shop_id' 
```

```js title="Python"
import requests

url = "https://partner.shopeemobile.com/api/v2/product/get_item_list?access_token=access_token&item_status=NORMAL&offset=0&page_size=10&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp&update_time_from=1611311600&update_time_to=1611311631"

payload={}
headers = {

}
response = requests.request("GET",url,headers=headers, data=payload, allow_redirects=False)

print(response.text)
```

## Response Example

```js title="JSON"
{
    "error": "",
    "message": "",
    "warning": "",
    "request_id": "6faac36a4a3242aabad2941e3acd7297",
    "response": {
        "item": [
            {
                "item_id": 2500139861,
                "item_status": "NORMAL",
                "update_time": 1608128470
            }
        ],
        "total_count": 19,
        "has_next_page": true,
        "next_offset": 10
    }
}
```

## Error Example
No Error Example Set

## Error Codes
|              Error                | Error Description |
|               :---                |       :---        |
|             error_param           | There is no access_token in query. |
|             error_auth            | Invalid access_token. |
|             error_param           | Invalid partner_id. |
|             error_param           | There is no partner_id in query. |
|             error_auth            | No permission to current api. |
|             error_param           | There is no sign in query. |
|             error_sign            | Wrong sign. |
|             error_param           | no timestamp |
|             error_param           | Invalid timestamp |
|             error_network         | Inner http call failed |
|       error_param_item_status     | Item status error. |
|    error_param_shop_id_not_found  | Shop_id is not found. |
|             error_inner           | Our system is taking some time to respond, please try later. |
|             error_inner           | System error, please try again later or contact the OpenAPI support team |
|         error_item_not_found      | Product not found |
|             error_inner           | Update item failed {{.error_info}} |
|             error_inner           | Update item failed {{.error_info}} |
|             error_inner           | System error, please try again later or contact the OpenAPI support team. |
|             error_inner           | System error, please try again later or contact the OpenAPI support team. |
|             error_auth            | Your shop can not use model level dts |
|         error_system_busy         | Our system is taking some time to respond, please try later |
| error_query_condition_list_limit  | Interal error, please contact openapi team. |
| error_query_query_limit_too_large | Interal error, please contact openapi team. |
