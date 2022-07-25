---
sidebar_position: 4
---

# Get Wallet Transaction List

```
GET /api/v2/payment/get_wallet_transaction
```
Use this API to get the transaction records of wallet


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
| page_no | int | <Highlight>True</Highlight> |  | Specifies the starting entry of data to return in the current call. Default is 0. if data is more than one page, the offset can be some entry to start next call. |
| page_size | int | <Highlight>True</Highlight> |  | If many transactions are available to retrieve, you may need to call GetTransactionList multiple times to retrieve all the data. Each result set is returned as a page of entries. Default is 40. Use the Pagination filters to control the maximum number of entries (<= 100) to retrieve per page (i.e., per call), the offset number to start next call. This integer value is usUed to specify the maximum number of entries to return in a single ""page"" of data. |
| create_time_from | int | <Highlight>True</Highlight> |  | The create_time_from field is the starting date range. The maximum date range that may be specified with the create_time_from and create_time_to fields is 15 days. |
| create_time_to | int | <Highlight>True</Highlight> |  | The create_time_to field is the ending date range. The maximum date range that may be specified with the create_time_from and create_time_to fields is 15 days. |
| wallet_type | string | <Highlight1>False</Highlight1> |  | This field indicates the wallet type. |
| transaction_type | string | <Highlight1>False</Highlight1> |  | This field indicates the transaction type. More detail can refer Data Definition to check. |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| -response | object |  |  |
| --transaction_list | object[] |  |  |
| ---status | string |  | The status of the transaction，available values: FAILED,COMPLETED,PENDING,INITIAL. |
| ---transaction_type | string |  | The type of transaction. |
| ---amount | float |  | The amount of transaction. |
| ---current_balance | float |  | The current balance of this account. |
| ---create_time | int |  | The create time of the transaction. |
| ---order_sn | string |  | Shopee's unique identifier for an order. |
| ---refund_sn | string |  | The serial number of return. |
| ---withdrawal_type | string |  | The type of withdrawal. |
| ---transaction_fee | float |  | This field indicates the transaction fee. |
| ---description | string |  | The detailed description of TOPUP SUCCESS and TOPUP FAILED. |
| ---buyer_name | string |  | The name of buyer. |
| ---pay_order_list | object[] |  |  |
| ----order_sn | string |  | Shopee's unique identifier for an order. |
| ----shop_name | string |  | Name of the shop. |
| ---shop_name | string |  | Name of the shop. |
| ---withdraw_id | int |  | Withdraw ID when transaction type is withdraw_created, withdrawal_completed, withdrawal_cancelled. |
| ---reason | string |  | The reason for ADJUSTMENT_ADD and ADJUSTMENT_MINUS. |
| ---root_withdrawal_id | int |  | Use this field to indicate the event where a withdrawal is split into several withdrawals due to the withdrawal limit. |
| --more | boolean |  |  |
| request_id | string | xduiwekui134 |  |
| message | string |  |  |
| error | string |  |  |

## Request Example
No Request Example Set

## Response Example
```js title="JSON"
{
    "response": {
        "more": true,
        "transaction_list": [{
            "status": "COMPLETED",
            "pay_order_list": [{
                "order_sn": "201108FKCHJJSY",
                "shop_name": "Luna Studio\u65e5\u97d3\u5546\u57ce"
            }],
            "buyer_name": "xiaotide",
            "description": "",
            "current_balance": 23552.59374,
            "reason": "",
            "transaction_type": "ESCROW_VERIFIED_ADD",
            "wallet_type": "shopee_pay",
            "amount": 5.91,
            "create_time": 1603152486,
            "transaction_fee": 0,
            "order_sn": "200924J11B6S0F",
            "refund_sn": "",
            "transaction_id": 2998861709,
            "withdrawal_type": ""
        }]
    },
    "error": "",
    "message": "",
    "request_id": "xduiwekui134"
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
| error_server | The inner server err when send http request. |
| time_period_too_large | The param error: time period too large. |
| time_invalid | The param error: create_time_from bigger than create_time_to. |
| time_invalid | The param error: time is invalid |
