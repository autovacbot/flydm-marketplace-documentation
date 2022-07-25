---
sidebar_position: 1
---

# Cancel Order

```
GET /api/v2/order/cancel_order
```
Use this api to cancel an order

## Commmon Parameters

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

|      Name       |   Type   |          Required           |      Sample    |                Description                     |
|      :---       |   :---   |           :---              |      :---      |                  :---                          |
|     order_sn    |   string | <Highlight>True</Highlight> | 201020SQQ5K2EP |     Shopee's unique identifier for an order.   |
|  cancel_reason  |   string | <Highlight>True</Highlight> |   OUT_OF_STOCK | The reason seller want to cancel this order. Applicable values: OUT_OF_STOCK, CUSTOMER_REQUEST, UNDELIVERABLE_AREA, COD_NOT_SUPPORTED. |
|   -item_list    | object[] | <Highlight1>False</Highlight1> |                |   Required when cancel_reason is OUT_OF_STOCK. |
|   --item_id     |   int    | <Highlight>True</Highlight> |      1680783   |               Id of item.                      |
|   --model_id    |   int    | <Highlight>True</Highlight> |     327890123  | Id of the model that belongs to the same item. |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| request_id | string | 2ead12d461c34e7c9275c42c2f70fa7d | The identifier for an API request for error tracking. |
| error | string | common.error_auth | Indicate error type if hit error. Empty if no error happened. |
| message | string | Invalid access_token. | Indicate error details if hit error. Empty if no error happened. |
| -response | object |  | Detail informations you are querying. |
| --update_time | timestamp | 1603184533 | The time when the order is updated. |

## Request Example

```js title="Payload"
{
	"order_sn": "201020SQQ5K2EP",
	"cancel_reason": "OUT_OF_STOCK",
	"item_list": [
		{
			"item_id": 1680783,
			"model_id": 327890123
		}
	]
}
```

```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("https://partner.shopeemobile.com/api/v2/order/cancel_order?sign=sign&access_token=access_token&timestamp=timestamp&shop_id=shop_id&partner_id=partner_id")
.header("Content-Type","application/json")
.body("{
   \"cancel_reason\": \"OUT_OF_STOCK\",
   \"item_list\": [
      {
         \"item_id\": 1680783,
         \"model_id\": 327890123
      }
   ],
   \"order_sn\": \"201020SQQ5K2EP\"
}")
.asString();
```

```js title="PHP"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("https://partner.shopeemobile.com/api/v2/order/cancel_order?sign=sign&access_token=access_token&timestamp=timestamp&shop_id=shop_id&partner_id=partner_id")
.header("Content-Type","application/json")
.body("{
   \"cancel_reason\": \"OUT_OF_STOCK\",
   \"item_list\": [
      {
         \"item_id\": 1680783,
         \"model_id\": 327890123
      }
   ],
   \"order_sn\": \"201020SQQ5K2EP\"
}")
.asString();
```

```js title="cURL"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/order/cancel_order?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => '{
    "cancel_reason": "OUT_OF_STOCK",
    "item_list": [
        {
            "item_id": 1680783,
            "model_id": 327890123
        }
    ],
    "order_sn": "201020SQQ5K2EP"
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```js title="cURL"
curl --location --request POST 'https://partner.shopeemobile.com/api/v2/order/cancel_order?shop_id=shop_id&partner_id=partner_id&sign=sign&access_token=access_token&timestamp=timestamp' \
--header 'Content-Type: application/json' \
--data-raw '{
   "cancel_reason": "OUT_OF_STOCK",
   "item_list": [
      {
         "item_id": 1680783,
         "model_id": 327890123
      }
   ],
   "order_sn": "201020SQQ5K2EP"
}'
```

```js title="Python"
import requests
import json

url = "https://partner.shopeemobile.com/api/v2/order/cancel_order?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp"

payload=json.dumps({
  "cancel_reason": "OUT_OF_STOCK",
  "item_list": [
    {
      "item_id": 1680783,
      "model_id": 327890123
    }
  ],
  "order_sn": "201020SQQ5K2EP"
})
headers = {
  'Content-Type': 'application/json'
}
response = requests.request("POST",url,headers=headers, data=payload, allow_redirects=False)

print(response.text)
```

## Response Example

```js title="JSON"
{
    "error": "",
    "message": "",
    "request_id": "2ead12d461c34e7c9275c42c2f70fa7d",
    "response": {
        "update_time": 1603184533
    } 
}
```
## Error Example
No Error Example Set

## Error Codes

|          Error          |              Error Description                       |
|          :---           |                   :---                               |
|     error_not_found     |           Wrong parameters, detail: {msg}.           |
|        error_param      |           Wrong parameters, detail: {msg}.           |
|     error_permission    | Sorry you don't have the permission, detail: {msg}.  |
|       error_server      |          System error. Please try again later.       |
|    order.error_limit    |             Can not cancel this order.               |
|    order. error_param   |          You can not cancel warehouse order.         |
| order. error_permission | Please link shop and partner on seller center first. |
|        error_param      |            There is no access_token in query.        |
|        error_auth       |                Invalid access_token.                 |
|        error_param      |                Invalid partner_id.                   |
|        error_param      |            There is no partner_id in query.          |
|        error_auth       |            No permission to current api.             |
|        error_param      |               There is no sign in query.             |
|        error_sign       |                     Wrong sign.                      | 
|        error_param      |                     no timestamp                     |
|        error_param      |                   Invalid timestamp                  |
|        error_network    |                 Inner http call failed               |