---
sidebar_position: 3
---

# Get Boosted List

```
GET /api/v2/get_boosted_list
```
Get boosted item list

## Common Parameters

| Name    | Type | Sample | Description    |
| :------ | :--- | :----- | :------------- |
| shop_id | int  | 123456 | Store Shop ID. |

## Request Parameters
No Request Parameters Set

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| error | string |  | Indicate error type if hit error. Empty if no error happened. |
| message | string | success | Indicate error details if hit error. Empty if no error happened. |
| warning | string |  | Warning message. |
| request_id | string | 053ee90ef2bf472598b98208af02c8ad | The identifier for an API request for error tracking. |
| -response | object |  |  |
| --item_list | object[] |  |  |
| ---item_id | int | 3200139749 | Shopee's unique identifier for an item |
| ---cool_down_second | int | 59 | Remain cool down time |

## Request Example

```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("https://partner.shopeemobile.com/api/v2/product/get_boosted_list?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/product/get_boosted_list?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp',
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
curl --location --request GET 'https://partner.shopeemobile.com/api/v2/product/get_boosted_list?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp' 
```

```js title="Python"
import requests

url = "https://partner.shopeemobile.com/api/v2/product/get_boosted_list?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp"

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
    "request_id": "053ee90ef2bf472598b98208af02c8ad",
    "response": {
        "item_list": [
            {
                "item_id": 3200139749,
                "cool_down_second": 59
            },
            {
                "item_id": 3400138725,
                "cool_down_second": 59
            },
            {
                "item_id": 2400143710,
                "cool_down_second": 59
            },
            {
                "item_id": 2300069665,
                "cool_down_second": 59
            },
            {
                "item_id": 2700128119,
                "cool_down_second": 59
            }
        ]
    }
}
```

## Error Example
No Error Example Set

## Error Codes

| Error | Error Description |
| :--- | :--- |
| error_param | There is no access_token in query. |
| error_auth | Invalid access_token. |
| error_param | Invalid partner_id. |
| error_param | There is no partner_id in query. |
| error_auth | No permission to current api. |
| error_param | There is no sign in query. |
| error_sign | Wrong sign. |
| error_param | no timestamp |
| error_param | Invalid timestamp |
| error_network | Inner http call failed |
| error_get_parnter_token_failed | Cannot get partner token. |
| error_get_boosted_item_info_failed | Get boosted item infomation failed. please try later. |
| error_inner | Our system is taking some time to respond, please try later. |
| error_inner | System error, please try again later or contact the OpenAPI support team. |
| error_item_not_found | Product not found |
| error_inner | Update item failed {{.error_info}} |
| error_inner | Update item failed {{.error_info}} |
| error_inner | System error, please try again later or contact the OpenAPI support team. |
| error_inner | System error, please try again later or contact the OpenAPI support team. |
| error_auth | Your shop can not use model level dts |
| error_system_busy | Our system is taking some time to respond, please try later. |
