---
sidebar_position: 2
---

# Get Escrow List

```
GET /api/v2/payment/get_escrow_list
```
Use this API to fetch the accounting list of order

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
| release_time_from | timestamp | <Highlight>True</Highlight> |  | Query start time |
| release_time_to | timestamp | <Highlight>True</Highlight> |  | Query end time |
| page_size| int | <Highlight1>False</Highlight1> |  | Number of pages returned max:100 default:40 |
| page_no | int | <Highlight1>False</Highlight1> |  | The page number min:1 default:1 |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| error | string |  | error code |
| message | string |  | error message |
| request_id | string |  | The request id |
| -response | object |  | The business content of the response |
| --escrow_list | object[] |  |  |
| ---order_sn | string |  |  |
| ---payout_amount | float |  | The settlement amount |
| ---escrow_release_time | timestamp |  | The release time |
| --more | boolean |  |  |

## Request Example
No Request Example Set

## Response Example

```js title="JSON"
{
    "response": {
        "escrow_list": [{
            "order_sn": 123456,
            "payout_amount": 123456,
            "escrow_release_time": 1
        }],
        "more": true
    },
    "error": "",
    "message": "",
    "request_id": "xduiwekui134"
}
```

## Error Example
No Error Example Set

# Error Codes

| Error | Error Description |
| :--- | :--- |
| error_param | There is no access_token in query. |
| error_auth | Invalid access_token |
| error_param | Invalid partner_id. |
| error_param | There is no partner_id in query. |
| error_auth | No permission to current api. |
| error_param | There is no sign in query. |
| error_sign | Wrong sign. |
| error_param | no timestamp |
| error_param | Invalid timestamp |
| error_network | Inner http call failed |
| get_item_error_server | Get item failed. |
| income_error_server | Get escrow income failed. |
| decoded_failed_error | The escrow item extinfo decoded failed. |
| income_not_found | The escrow income not found. |
| order_error_server | The escrow order extinfo decoded failed. |
| order_not_found | The order info not found. |
| order_shopid_invalid | The escrow order's shopid is invalid. |
| return_info_error_server | Get return or refund info failed. |
| internal_error_server | The inner server err when warp http req. |
| shopid_invalid | Shopid is invalid. |
| userid_invalid | Userid is invalid. |