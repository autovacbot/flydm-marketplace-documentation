---
sidebar_position: 3
---

# Get Payout Detail

```
Post /api/v2/payment/get_payout_detail
```
This API is applicable for Cross Border (CB) sellers only to get the shop's payout data, such as the payout amount, currency, FX rate, the payout's associated order income and adjustment records etc.

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

| Name | Type | Required | Sample | Description |
| :--- | :--- | :--- | :--- | :--- |
| page_size | int | <Highlight>True</Highlight> |  | Number of pages returned max:100 |
| page_no | int | <Highlight>True</Highlight> |  | The page number min:1 default:1 |
| payout_time_from | timestamp | <Highlight>True</Highlight> |  | Strat time |
| payout_time_to | timestamp | <Highlight>True</Highlight> |  | End time |

## Response Parameters
| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| error | string |  | Error code |
| message | string |  | Error message |
| request_id | string |  | The unique id for request. |
| -response | object |  | The business content of the response |
| --more | boolean |  |  |
| -payout_list | object[] |  |  |
| --payout_info | object |  | The information of payout |
| ---from_currency | string |  | The settlement currency of orders. |
| ---payout_currency | string |  | The actual currency of payout. |
| ---from_amount | float |  | The settlement amount. |
| ---payout_amount | float |  | The actual amount of payout. |
| ---exchange_rate | string |  | The exchange rate |
| ---payout_time | timestamp |  | The time of payout. |
| ---pay_service | string |  | The service provider of seller. Available value: payoneer, pingpong, lianlian. |
| ---payee_id | string |  | Seller's account to receive the payout. |
| --offline_adjustment_list | object[] |  | The list of offline adjustments. |
| --adjustment_amount | float |  | The amount of offline adjustments. |
| --module | string |  | The reason for offline adjustment. |
| --remark | string |  | The remark for the reason. |
| --scenario | string |  | The scenario of adjustment. |
| --adjustment_level | string |  | Dimension of offline adjustment. Available value: shop, order. |
| --order_sn | string |  | Shopee's unique identifier for an order. |

## Response Example

```js title = "JSON"
{
"response": {
"more": false,
"payout_list": [{
"payout_info": {
"from_currency": "TWD",
"payout_currency": "USD",
"from_amount": 1004,
"payout_amount": 313.59,
"exchange_rate": "0.31234",
"payout_time": 1604457102,
"pay_service": "PAYONEER",
"payee_id": "111107627145"
},
"escrow_list": [{
"escrow_amount": 33.55,
"currency": "MYR",
"order_sn": "200930444R0703"
},
{
"escrow_amount": 20.48,
"currency": "MYR",
"order_sn": "201009UPR97432"
},
{
"escrow_amount": 22.65,
"currency": "MYR",
"order_sn": "201006KGYAMT1M"
},
{
"escrow_amount": 15.33,
"currency": "MYR",
"order_sn": "201003BV7JDTU7"
}
],
"offline_adjustment_list": [{
"adjustment_amount": -92.5,
"module": "ActualShippingFee",
"remark": "CODRejectionOrderActualShippingFee",
"scenario": "OrderASFCharge",
"adjustment_level": "order",
"order_sn": "200920945YPT5E"
},
{
"adjustment_amount": -213,
"module": "ActualShippingFee",
"remark": "CODRejectionOrderActualShippingFee",
"scenario": "OrderASFCharge",
"adjustment_level": "order",
"order_sn": "2008262BJS6PNP"
},
{
"adjustment_amount": -128.5,
"module": "ActualShippingFee",
"remark": "CODRejectionOrderActualShippingFee",
"scenario": "OrderASFCharge",
"adjustment_level": "order",
"order_sn": "200819G1AE876X"
}
],
"more": true
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
