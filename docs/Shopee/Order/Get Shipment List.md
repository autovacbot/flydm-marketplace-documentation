---
sidebar_position: 4
---

# Get Shipment List

```
GET /api/v2/order/get_shipment_list
```
Use this api to get order list which order_status is READY_TO_SHIP

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


|    Name    |    Type    |           Required          |    Sample    |     Description     |
|    :---    |    :---    |           :---              |     :---     |         :---        |
|    cursor  |   string   | <Highlight1>False</Highlight1> |      ""      | Specifies the starting entry of data to return in the current call. Default is "". If data is more than one page, the offset can be some entry to start next call. |
|  page_size |     int    | <Highlight>True</Highlight> |      20      | Each result set is returned as a page of entries. Use the "page_size" filters to control the maximum number of entries to retrieve per page (i.e., per call). This integer value is used to specify the maximum number of entries to return in a single "page" of data.The limit of page_size if between 1 and 100. |

## Response Parameters

|       Name        |   Type   |           Sample              |                       Description                                |
|       :---        |   :---   |            :---               |                          :---                                    |
|       error       |   string |        common error_auth      |   Indicate error type if hit error. Empty if no error happened.  |
|       message     |   string |       Invalid access_token    | Indicate error details if hit error. Empty if no error happened. |
|      -response    |   object |                               |               Detail informations you are querying.              |
|     --order_list  | object[] |                               |                    The list of shipment orders                   |
|     ---order_sn   |   string |          2003160SXK2A3T       |                 Shopee's unique identifier for an order.         |
| ---package_number |   string |          38027870177402       |      Shopee's unique identifier for the package under an order   |
|      --more       |  boolean |   <Highlight>true</Highlight> | This is to indicate whether the order list is more than one page. If this value is true, you may want to continue to check next page to retrieve orders. |
|    --next_cursor  |   string |              20               | If more is true, you should pass the next_cursor in the next request as cursor. The value of next_cursor will be empty string when more is false. |
|     request_id    |   string | 69ee3f61ec6f4e3f85836391e5b78dbc |        The identifier for an API request for error tracking.  |

## Request Example

```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("https://partner.shopeemobile.com/api/v2/order/get_shipment_list?page_size=20&sign=sign&cursor=""&shop_id=shop_id&partner_id=partner_id&access_token=access_token&timestamp=timestamp")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/order/get_shipment_list?access_token=access_token&cursor=%22%22&page_size=20&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp',
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

curl --location --request GET 'https://partner.shopeemobile.com/api/v2/order/get_shipment_list?access_token=access_token&timestamp=timestamp&page_size=20&sign=sign&cursor=""&shop_id=shop_id&partner_id=partner_id' 
```

```js title="Python"
import requests

url = "https://partner.shopeemobile.com/api/v2/order/get_shipment_list?access_token=access_token&cursor=%22%22&page_size=20&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp"

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
    "response": {
        "order_list": [
            {
                "order_sn": "2003160SXK2A3T",
                "package_number": "38027870177402"
            },
            {
                "order_sn": "200313Q1GR98GC",
                "package_number": "37791910064652"
            },
            {
                "order_sn": "201228RDKTYMXV",
                "package_number": "62839258199004"
            },
            {
                "order_sn": "201228RDQN04K7",
                "package_number": "62839386141287"
            },
            {
                "order_sn": "201228RDQN04K8",
                "package_number": "62839386141288"
            }
        ],
        "more": true,
        "next_cursor": "20"
    },
    "request_id": "69ee3f61ec6f4e3f85836391e5b78dbc"
}
```
## Error Example
No Error Example Set

## Error Codes

|       Error      |             Error Description                       |
|       :---       |                   :---                              |
| error_not_found  |            Wrong parameters, detail: {msg}.         |
|   error_param    |            Wrong parameters, detail: {msg}.         |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
|   error_server   |           System error. Please try again later.     |
|   error_param    |           There is no access_token in query.        |
|   error_auth     |                Invalid access_token.                |
|   error_param    |                 Invalid partner_id.                 |
|   error_param    |           There is no partner_id in query.          |
|   error_auth     |             No permission to current api.           |
|   error_param    |               There is no sign in query.            |
|   error_sign     |                     Wrong sign.                     |
|   error_param    |                    no timestamp                     |
|   error_param    |                  Invalid timestamp                  |
|  error_network   |                Inner http call failed               |