---
sidebar_position: 1
---

# Add Voucher

```
POST /api/v2/voucher/add_voucher
```
Add voucher

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
| voucher_name | string | <Highlight>True</Highlight> | testamount | 	
The name of the voucher. |
| voucher_code | string | <Highlight>True</Highlight> | test | The code of the voucher. |
| start_time | timestamp | <Highlight>True</Highlight> | 1624719600 | The timing from when the voucher is valid; so buyer is allowed to claim and to use. Field can only be updated if voucher has not started. |
| end_time | timestamp | <Highlight>True</Highlight> | 1624978800 | The timing until when the voucher is still valid. Any time after this end_time, buyer is not allowed to claim or to use. |
| voucher_type | int | <Highlight>True</Highlight> | 1 | The type of the voucher. The available values are: 1: shop voucher, 2: product voucher. |
| reward_type | int | <Highlight>True</Highlight> | 1 | The reward type of the voucher. The available values are: 1: fix_amount voucher, 2: discount_percentage voucher, 3: coin_cashback voucher. |
| usage_quantity | int | <Highlight>True</Highlight> | 20000 | The number of times for this particular voucher could be used. |
| min_basket_price | float | <Highlight>True</Highlight> | 12.01 | The minimum spend required for using this voucher. |
| discount_amount | float | <Highlight1>False</Highlight1> | 1.55 | The discount amount set for this particular voucher. Only fill in when you are creating a fix amount voucher. |
| percentage | int | <Highlight1>False</Highlight1> | 22 | The discount percentage set for this particular voucher. Only fill in when you are creating a discount percentage voucher or coins cashback voucher. |
| max_price | float | <Highlight1>False</Highlight1> | 12.0 | The max amount of discount/value a user can enjoy by using this particular voucher. Only fill in when you are creating a discount percentage voucher or coins cashback voucher. |
| display_channel_list | int[] | <Highlight1>False</Highlight1> | [1] | The FE channel where the voucher will be displayed. The available values are: 1: display_all, 2: order page, 3: feed, 4: live streaming, [] (empty - which is hidden). |
| item_id_list | int[] | <Highlight1>False</Highlight1> | [1223223,1223213] | The list of items which is applicable for the voucher. Only fill in when you are creating a product type of voucher. |
| display_start_time | int | <Highlight1>False</Highlight1> | 162078900 | The timing of when voucher is displayed on shop pages; so buyer is allowed to claim.display_start_time must be left empty if the display_channel_list is empty (when voucher is hidden), otherwise it will show error. |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| error | string |  | Indicate error type if hit error. Empty if no error happened. |
| message | string |  | Indicate error details if hit error. Empty if no error happened. |
| request_id | string | 4e5d881ac1bc11ebba0dacde48001122 | The identifier of the API request for error tracking. |
| -response | object |  | Detailed informations you are querying. |
| --voucher_id | int | 123 | The unique identifier for the created voucher. |

## Request Example

```js title="Payload"
{
    "voucher_name": "testamount",
    "voucher_code": "test",
    "start_time": 1624719600,
    "end_time": 1624978800,
    "voucher_type": 1,
    "reward_type": 1,
    "usage_quantity": 20000,
    "min_basket_price": 12.01,
    "discount_amount": 1.55,
    "max_price": 12.12,
    "display_channel_list": [
        1
    ],
    "display_start_time":162078900
}
```

## Response Example

``` js title="JSON"
{
    "response": {
        "voucher_id": 123
    },
    "request_id": "4e5d881ac1bc11ebba0dacde48001122",
    "error": "",
    "message": ""
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
| voucher.voucher_min_price_error | Min_basket_price must be higher than the fix amount if Min_basket_price is not 0. |
| voucher.voucher_code_duplicate_error | Duplicated voucher code. |
| voucher.voucher_code_error | Voucher code doesn't meet the requirement. Only support 0-9 or A-Z or a-z. Up to 5 characters. |
| voucher.voucher_coin_error | Cannot create coin cashback voucher. |
| voucher.voucher_display_channel_error | Voucher display channel is set wrongly. |
| voucher.voucher_end_time_error | Voucher valid period can not be longer than 3 months. |
| voucher.fix_amount_low_qualtiy_errorr | Voucher cannot be saved as it is lower than {limit}%. Please adjust the percentage amount to be more than or equal to {limit}%. |
| voucher.voucher_item_blocked_from_promotion_error | Some items cannot be uploaded as they are prohibited from promotions due to regulations |
| voucher.voucher_item_duplication_error | Duplicated items in item_id_list. |
| voucher.voucher_item_count_limit_error | The number of items in item_id_list exceeds the limit. |
| voucher.voucher_item_not_exist | Some item in item_id_list doesn't exist |
| voucher.voucher_item_status_error | Not all the items in item_id_list are in normal status. |
| voucher.voucher_item_stock_error | Some item in item_id_list has 0 stock. |
| voucher.voucher_max_discount_low_quality | To attract buyers to use your voucher, please increase maximum discount price to > {percentage_input*min_spend*0.01} or reduce minimum basket price to < {max_discount*100/percentage_input} to ensure buyers can enjoy the percentage discount configured. |
| voucher.voucher_over_limit | The total number of ongoing voucher and upcoming voucher cannot exceed 1000. |
| voucher.percentage_low_quality_error | Voucher cannot be saved as it is lower than {limit}.00%. Please adjust the percentage amount to be more than or equal to {limit}.00%. |
| voucher.voucher_start_time_error | Voucher start time is earlier than current time. |
| voucher.voucher_time_period_error | Voucher end time must be 1 hour later than the start time. |
