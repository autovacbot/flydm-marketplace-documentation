---
sidebar_position: 3
---

# Get Shipping Document Result

```
GET /api/v2/logistics/get_shipping_document_result
```
Use this api to get the shipping_document of each order or package status.

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

| Name | Type | Required | Sample | Description |
| :--- | :--- | :--- | :--- | :--- |
| -order_list | object[] | <Highlight>True</Highlight> |  | The list of orders, limit [1,50] |
| --order_sn | string | <Highlight>True</Highlight> | 201118BCKPJQQ8 | Shopee's unique identifier for an order. |
| --package_number | string | <Highlight1>False</Highlight1> | 2485710696837122445 | Shopee's unique identifier for the package under an order. You should't fill the field with empty string when there is't a package number. |
| --shipping_document_type | string | <Highlight1>False</Highlight1> | NORMAL_AIR_WAYBILL | The type of shipping document. Available values: NORMAL_AIR_WAYBILL, THERMAL_AIR_WAYBILL, NORMAL_JOB_AIR_WAYBILL, THERMAL_JOB_AIR_WAYBILL |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| request_id | string | 5551ce8db5314c70a362dfe33544f074 | The identifier for an API request for error tracking. |
| error | string | error_auth | Indicate error type if hit error. Empty if no error happened. |
| message | string | Invalid access_token. | Indicate error details if hit error. Empty if no error happened. |
| -warning | object[] |  | Indicate warning message you should take care. |
| --order_sn | string |  | Shopee's unique identifier for an order. |
| --package_number | string |  | Shopee's unique identifier for the package under an order. |
| -response | object |  | Detail informations you are querying. |
| --result_list | object[] |  | The result data list of the API response. |
| ---order_sn | string | 201118BCKPJQQ8 | Shopee's unique identifier for an order. |
| ---package_number | string | 2485710696837122445 | Shopee's unique identifier for the package under an order. |
| ---status | string | READY | The status of the shipping document task you querying with order_sn. Available values: READY， FAILED， PROCESSING |
| ---fail_error | string |  | Indicate error type if one element hit error. |
| ---fail_message | string |  | Indicate error details if one element hit error. |

```js title="Payload"
{
	"order_list": [
		{
			"order_sn": "201118BCKPJQQ8",
			"package_number": "2485710696837122445",
			"shipping_document_type": "NORMAL_AIR_WAYBILL"
		}
	]
}
```

```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("https://partner.shopeemobile.com/api/v2/logistics/get_shipping_document_result?sign=sign&access_token=access_token&timestamp=timestamp&shop_id=shop_id&partner_id=partner_id")
.header("Content-Type","application/json")
.body("{
   \"order_list\": [
      {
         \"order_sn\": \"201118BCKPJQQ8\",
         \"package_number\": \"2485710696837122445\",
         \"shipping_document_type\": \"NORMAL_AIR_WAYBILL\"
      }
   ]
}")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/logistics/get_shipping_document_result?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => '{
    "order_list": [
        {
            "order_sn": "201118BCKPJQQ8",
            "package_number": "2485710696837122445",
            "shipping_document_type": "NORMAL_AIR_WAYBILL"
        }
    ]
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
curl --location --request POST 'https://partner.shopeemobile.com/api/v2/logistics/get_shipping_document_result?access_token=access_token&timestamp=timestamp&shop_id=shop_id&partner_id=partner_id&sign=sign' \
--header 'Content-Type: application/json' \
--data-raw '{
   "order_list": [
      {
         "order_sn": "201118BCKPJQQ8",
         "package_number": "2485710696837122445",
         "shipping_document_type": "NORMAL_AIR_WAYBILL"
      }
   ]
}'
```

```js title="Python"
import requests
import json

url = "https://partner.shopeemobile.com/api/v2/logistics/get_shipping_document_result?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp"

payload=json.dumps({
  "order_list": [
    {
      "order_sn": "201118BCKPJQQ8",
      "package_number": "2485710696837122445",
      "shipping_document_type": "NORMAL_AIR_WAYBILL"
    }
  ]
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
    "response": {
        "result_list": [
            {
                "order_sn": "201118BCKPJQQ8",
                "package_number": "2485710696837122445",
                "shipping_document_type": "READY"
            }
        ]
    },
    "request_id": "5551ce8db5314c70a362dfe33544f074"
}
```

## Error Example
No Error Example Set

## Error Codes

| Error | Error Description |
| :--- | :--- |
| common.batch_api_all_failed | Failed, please check result_list for more details. |
| error_not_found | Wrong parameters, detail: {msg}. |
| error_param | Wrong parameters, detail: {msg}. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| error_server | System error. Please try again later. |
| logistics.unknown_error | Unknown error, please contact Shopee to check. Detail: {msg} |
| logistics.order_not_exist | The order_sn {order_sn} is not exist. |
| logistics.shipping_document_should_print_first | The package can not print now, please create shipping document first.Detail: {msg} |
| logistics.package_number_not_exist | Please request with package_number for this split order. |
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