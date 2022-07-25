---
sidebar_position: 3
---

# Get Order List

```
GET /api/v2/order/get_order_list
```

export const Highlight2 = ({children, color}) => (
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

Create a new getorderlist, probably with input from previous steps.

## Common Parameters

| Name    | Type | Sample | Description    |
| :------ | :--- | :----- | :------------- |
| shop_id | int  | 123456 | Store Shop ID. |

## Request Parameters

|        Name      |    Type    |            Required           |      Sample     |    Description    |
|        :---      |    :---    |             :---              |      :---       |       :---        |
| time_range_field |    string  | <Highlight2>True</Highlight2> |   create_time   | The kind of time_from and time_to. Available value: create_time, update_time. |
|   time_from      |     int    | <Highlight2>True</Highlight2> |    1607235072   | The time_from and time_to fields specify a date range for retrieving orders (based on the time_range_field). The time_from field is the starting date range. The maximum date range that may be specified with the time_from and time_to fields is 15 days. |
|     time_to      |     int    | <Highlight2>True</Highlight2> |    1608271872   | The time_from and time_to fields specify a date range for retrieving orders (based on the time_range_field). The time_from field is the starting date range. The maximum date range that may be specified with the time_from and time_to fields is 15 days. |
|    page_size     |     int    | <Highlight2>True</Highlight2> |        20       | Each result set is returned as a page of entries. Use the "page_size" filters to control the maximum number of entries to retrieve per page (i.e., per call). This integer value is used to specify the maximum number of entries to return in a single "page" of data.The limit of page_size if between 1 and 100. |
|     cursor       |   string   | <Highlight1>False</Highlight1> |        ""       | Specifies the starting entry of data to return in the current call. Default is "". If data is more than one page, the offset can be some entry to start next call. |
|   order_status   |   string   | <Highlight1>False</Highlight1> |  READY_TO_SHIP  | The order_status filter for retriveing orders and each one only every request. Available value: UNPAID/READY_TO_SHIP/PROCESSED/SHIPPED/COMPLETED/IN_CANCEL/CANCELLED/INVOICE_PENDING |
| response_optional_fields | string | <Highlight1>False</Highlight1> |   order_status  | Optional fields in response. Available value: order_status. |

## Response Parameters

|     Name      |   Type   |              Sample               |                           Description                            |
|     :---      |   :---   |              :---                 |                              :---                                |
|   request_id  |  string  | b937c04e554847789cbf3fe33a0ad5f1  |       The identifier for an API request for error tracking.      |
|     error     |  string  |          common.error_auth        |   Indicate error type if hit error. Empty if no error happened.  |
|    message    |  string  |        Invalid access_token.      | Indicate error details if hit error. Empty if no error happened. |
|   -response   |  object  |                                   |                Detail informations you are querying              |
|    --more     |  boolean |               false               | This is to indicate whether the order list is more than one page. If this value is true, you may want to continue to check next page to retrieve orders.|
|  -order_list  | object[] |                                   |                                                                  |
|  --order_sn   |  string  |            201218V2Y6E59M         |              Shopee's unique identifier for an order.            |
|--order_status |  string  |            READY_TO_SHIP          |     The order_status filter for retriveing orders and each one only every request. Available value: UNPAID/READY_TO_SHIP/PROCESSED/SHIPPED/COMPLETED/IN_CANCEL/CANCELLED |
| -next_cursor  |  string  |                20                 | If more is true, you should pass the next_cursor in the next request as cursor. The value of next_cursor will be empty string when more is false. |

## Request Example

```js title="Java"

Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("https://partner.shopeemobile.com/api/v2/order/get_order_list?page_size=20&response_optional_fields=order_status&timestamp=timestamp&shop_id=shop_id&order_status=READY_TO_SHIP&partner_id=partner_id&access_token=access_token&cursor=""&time_range_field=create_time&time_from=1607235072&time_to=1608271872&sign=sign")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/order/get_order_list?access_token=access_token&cursor=%22%22&order_status=READY_TO_SHIP&page_size=20&partner_id=partner_id&response_optional_fields=order_status&shop_id=shop_id&sign=sign&time_from=1607235072&time_range_field=create_time&time_to=1608271872&timestamp=timestamp',
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

curl --location --request GET 'https://partner.shopeemobile.com/api/v2/order/get_order_list?timestamp=timestamp&shop_id=shop_id&order_status=READY_TO_SHIP&partner_id=partner_id&access_token=access_token&page_size=20&response_optional_fields=order_status&time_range_field=create_time&time_from=1607235072&time_to=1608271872&sign=sign&cursor=""' 
```

```js title="Python"
import requests

url = "https://partner.shopeemobile.com/api/v2/order/get_order_list?access_token=access_token&cursor=%22%22&order_status=READY_TO_SHIP&page_size=20&partner_id=partner_id&response_optional_fields=order_status&shop_id=shop_id&sign=sign&time_from=1607235072&time_range_field=create_time&time_to=1608271872&timestamp=timestamp"

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
        "more": true,
        "next_cursor":"20",
        "order_list": [
            {
                "order_sn": "201218V2Y6E59M"
            },
            {
                "order_sn": "201218V2W2SG1E"
            },
            {
                "order_sn": "201218V2VJJC70"
            },
            {
                "order_sn": "201218V2TEURPF"
            },
            {
                "order_sn": "201218UXWNTUNP"
            },
            {
                "order_sn": "201218UWFYSCF1"
            },
            {
                "order_sn": "201215MPRFUUNN"
            },
            {
                "order_sn": "201215MCR3V9N8"
            },
            {
                "order_sn": "201214JASXYXY6"
            },
            {
                "order_sn": "201214JAJXU6G7"
            }
        ]
    },
    "request_id": "b937c04e554847789cbf3fe33a0ad5f1"
}
```
## Error Example
No Error Example Set

## Error Codes

| Error | Error Description |
| :---  |  :---  |
| error_not_found | Wrong parameters, detail: {msg}. |
| error_param | Wrong parameters, detail: {msg}. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| error_server | System error. Please try again later. |
| order.order_list_invalid_time | Start time must be earlier than end time and diff in 15days. |
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