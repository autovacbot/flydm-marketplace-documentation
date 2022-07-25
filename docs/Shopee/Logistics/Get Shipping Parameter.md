---
sidebar_position: 5
---

# Get Shipping Parameter

```
GET /api/v2/logistics/get_tracking_number
```
Use this api to get tracking_number when you have shipped order

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
| order_sn | string | <Highlight>True</Highlight> | 201214JASXYXY6 | Shopee's unique identifier for an order. |
| package_number | string | <Highlight1>False</Highlight1> |  | Shopee's unique identifier for the package under an order. You should't fill the field with empty string when there isn't a package number. |
| response_optional_fields | string | <Highlight1>False</Highlight1> | first_mile_tracking_number | Indicate response fields you want to get. Please select from the below response parameters. If you input an object field, all the params under it will be included automatically in the response. If there are multiple response fields you want to get, you need to use English comma to connect them. Available values: plp_number, first_mile_tracking_number,last_mile_tracking_number |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| request_id | string | 9d07076ffda5407bb7c559f0b82ed91e | The identifier for an API request for error tracking. |
| error | string | error_auth | Indicate error type if hit error. Empty if no error happened. |
| message | string | Invalid access_token. | Indicate error details if hit error. Empty if no error happened. |
| -response | object |  | Detail informations you are quesrying |
| --tracking_number | string | MY200448706479IT | The tracking number of this order. |
| --plp_number | string |  | The unique identifier for package of BR correios. |
| --first_mile_tracking_number | string | CNF877146678717210312 | The first mile tracking number of the order. Only for Cross Border Seller |
| --last_mile_tracking_number | string | 200448706479IT | The last mile tracking number of the order. Only for Cross Border BR seller. |
| --hint | string | Buyers CVS closed， waiting for buyer to reselect another CVS stores，auto cancel time 2021-01-01 | Indicate hint information if cannot get some fields under special scenarios. For example, cannot get tracking_number when cvs store is closed. |

## Request Example
```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("https://partner.shopeemobile.com/api/v2/logistics/get_tracking_number?partner_id=partner_id&order_sn=201214JASXYXY6&access_token=access_token&timestamp=timestamp&sign=sign&response_optional_fields=first_mile_tracking_number&shop_id=shop_id&package_number=-")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/logistics/get_tracking_number?access_token=access_token&order_sn=201214JASXYXY6&package_number=-&partner_id=partner_id&response_optional_fields=first_mile_tracking_number&shop_id=shop_id&sign=sign&timestamp=timestamp',
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
curl --location --request GET 'https://partner.shopeemobile.com/api/v2/logistics/get_tracking_number?package_number=-&partner_id=partner_id&order_sn=201214JASXYXY6&access_token=access_token&timestamp=timestamp&sign=sign&response_optional_fields=first_mile_tracking_number&shop_id=shop_id' 
```

```js title="Python"
import requests

url = "https://partner.shopeemobile.com/api/v2/logistics/get_tracking_number?access_token=access_token&order_sn=201214JASXYXY6&package_number=-&partner_id=partner_id&response_optional_fields=first_mile_tracking_number&shop_id=shop_id&sign=sign&timestamp=timestamp"

payload={}
headers = {

}
response = requests.request("GET",url,headers=headers, data=payload, allow_redirects=False)

print(response.text)
```

```js title="JSON"
{
    "error": "",
    "message": "",
    "response": {
        "tracking_number": "MY200448706479IT",
        "first_mile_tracking_number": "CNF877146678717210312"
    },
    "request_id": "9d07076ffda5407bb7c559f0b82ed91e"
}
```

## Error Example
No Error Example Set

## Error Codes

| Error | Error Description |
| :--- | :--- |
| logistics.error_param | The order is being allocated, please wait until the allocate is completed. |
| error_not_found | Wrong parameters, detail: {msg}. |
| error_param | Wrong parameters, detail: {msg}. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| error_server | System error. Please try again later. |
| logistics.invalid_error | The order is not exist. |
| logistics.package_not_exist | The package is not exist. |
| common.invalid_shop | Shop id is invalid. Please check your shop. |
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
