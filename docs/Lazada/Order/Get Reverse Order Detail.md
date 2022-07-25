export const Highlight = ({children, color}) => (
<span
style={{
      backgroundColor: color,
      borderRadius: '2px',
      color: '#FFFFFF',
      padding: '0.2rem',
    }}>
{children}
</span>
);

export const Highlight1 = ({children, color}) => (
<span
style={{
      backgroundColor: color,
      borderRadius: '2px',
      color: '#333333',
      padding: '0.2rem',
    }}>
{children}
</span>
);

export const Highlight2 = ({children, color}) => (
<span
style={{
      backgroundColor: color,
      color: '#FF0000',
    }}>
{children}
</span>
);

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/order/reverse/return/history/list</Highlight1>

Get the communication history of the reverse order

### Common Parameters

---

#### Common Request Parameters

---

| Name      | Type   | Required                      | Description                         |
| :-------- | :----- | :---------------------------- | :---------------------------------- |
| seller_id | String | <Highlight2>true</Highlight2> | Seller store id                     |
| country   | String | <Highlight2>true</Highlight2> | Seller country, Ex: MY,SG,ID,TH,etc |

### Request Parameters

---

| Name                  | Type   | Required                      | Demo Value            | Rule | Description |
| :-------------------- | :----- | :---------------------------- | :-------------------- | :--- | :---------- |
| reverse_order_line_id | Number | <Highlight2>true</Highlight2> | reverse order line id |      | 0           |

### Common Response Parameters

---

| Name       | Type     | Description                                                                                                                                                            |
| :--------- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type       | String   | Error type. Optional values ​​are ISP (service provider error), ISV (developer error), SYSTEM (platform system error)                                                  |
| code       | String   | Error code. For example: ServiceUnavailable                                                                                                                            |
| message    | String   | Description of error details                                                                                                                                           |
| request_id | String   | Request a unique identifier                                                                                                                                            |
| detail     | Object[] | If the API call is for batch processing, when the call fails (all or part of the request failure), the response contains the error details. See the following example: |

```bash
{
    "detail": [
        {
            "field": "Product",
            "seller_sku": "api-create-test-1",
            "message": "SELLER_SKU_INVALID"
        },
        {
            "field": "Product2",
            "message": "SELLER_SKU_INVALID"
        }
    ]
}
```

### Response Parameters

---

| Name                             | Type     | Demo Value       | Description                                                                                                        |
| :------------------------------- | :------- | :--------------- | :----------------------------------------------------------------------------------------------------------------- |
| data                             | Object   | {}               | data                                                                                                               |
| -reverse_order_id                | Number   | 0                | reverse order id                                                                                                   |
| -trade_order_id                  | Number   | 0                | trade order id                                                                                                     |
| -request_type                    | String   | CANCEL           | CANCEL;RETURN;ONLY_REFUND                                                                                          |
| -shipping_type                   | String   | PICK_UP          | PICK_UP;DROP_OFF                                                                                                   |
| -is_rtm                          | Boolean  | true             | is Return to Merchant or not                                                                                       |
| -reverseOrderLineDTOList         | Object[] | []               | reverseOrderLineDTOList                                                                                            |
| --reverse_order_line_id          | Number   | 0                | reverse order line id                                                                                              |
| --trade_order_line_id            | Number   | 0                | trade order line id                                                                                                |
| --buyer                          | Object   | {}               | buyer                                                                                                              |
| ---user_id                       | Number   | 0                | buyer user id                                                                                                      |
| --reverse_status                 | String   | REQUEST_INITIATE | REQUEST_INITIATE;REQUEST_REJECT;REQUEST_CANCEL;CANCEL_SUCCESS                                                      |
| --productDTO                     | Object   | {}               | productDTO                                                                                                         |
| ---product_id                    | Number   | 0                | product id                                                                                                         |
| ---sku                           | String   | 0                | sku id                                                                                                             |
| --is_need_refund                 | Boolean  | true             | need refund or not                                                                                                 |
| --ofc_status                     | String   | INITIAL          | fulfillment status                                                                                                 |
| --trade_order_gmt_create         | Number   | 0                | trade order create time                                                                                            |
| --refund_amount                  | Number   | 0                | refund amount, currency in cent, except VN (for example for SG, 100 equals SGD $1; for VN, 10000 equals VND 10000) |
| --reason_text                    | String   | Out of stock     | reason text                                                                                                        |
| --reason_code                    | Number   | 123              | reason code                                                                                                        |
| --refund_payment_method          | String   | Alipay           | refund payment Method                                                                                              |
| --whqc_decision                  | String   | scrap            | warehouse decision                                                                                                 |
| --return_order_line_gmt_create   | Number   | 0                | reverse order line create time                                                                                     |
| --return_order_line_gmt_modified | Number   | 0                | reverse order line modified time                                                                                   |
| --is_dispute                     | Boolean  | true             | is in dispute or not                                                                                               |
| --seller_sku_id                  | String   | th-123           | seller sku id                                                                                                      |
| --item_unit_price                | Number   | 0                | price, currency in cent, except VN (for example for SG, 100 equals SGD $1; for VN, 10000 equals VND 10000)         |
| --platform_sku_id                | String   | th-000           | platform sku id                                                                                                    |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "reverse_order_id": "0",
    "request_type": "CANCEL",
    "reverseOrderLineDTOList": [
      {
        "return_order_line_gmt_create": "0",
        "platform_sku_id": "th-000",
        "is_need_refund": "true",
        "trade_order_gmt_create": "0",
        "reason_text": "Out of stock",
        "item_unit_price": "0",
        "trade_order_line_id": "0",
        "return_order_line_gmt_modified": "0",
        "ofc_status": "INITIAL",
        "seller_sku_id": "th-123",
        "productDTO": {
          "product_id": "0",
          "sku": "0"
        },
        "refund_payment_method": "Alipay",
        "buyer": {
          "user_id": "0"
        },
        "reason_code": "123",
        "whqc_decision": "scrap",
        "reverse_status": "REQUEST_INITIATE",
        "refund_amount": "0",
        "is_dispute": "true",
        "reverse_order_line_id": "0"
      },
      {
        "return_order_line_gmt_create": "0",
        "platform_sku_id": "th-000",
        "is_need_refund": "true",
        "trade_order_gmt_create": "0",
        "reason_text": "Out of stock",
        "item_unit_price": "0",
        "trade_order_line_id": "0",
        "return_order_line_gmt_modified": "0",
        "ofc_status": "INITIAL",
        "seller_sku_id": "th-123",
        "productDTO": {
          "product_id": "0",
          "sku": "0"
        },
        "refund_payment_method": "Alipay",
        "buyer": {
          "user_id": "0"
        },
        "reason_code": "123",
        "whqc_decision": "scrap",
        "reverse_status": "REQUEST_INITIATE",
        "refund_amount": "0",
        "is_dispute": "true",
        "reverse_order_line_id": "0"
      }
    ],
    "shipping_type": "PICK_UP",
    "is_rtm": "true",
    "trade_order_id": "0"
  },
  "request_id": "0ba2887315178178017221014"
}
```

### Error Example

---

```
{
  "code": "MISSING_PARAMETER",
  "type": "ISV",
  "message": "missing required parameter: access_token",
  "request_id": "0ba2887315172940728551014"
}
```

### Error Codes

---

| Error Code | Error Message                               | Description                                 |
| :--------- | :------------------------------------------ | :------------------------------------------ |
| 105        | E0105: reverse order id is empty or invalid | E0105: reverse order id is empty or invalid |
| 106        | E0106: ROC internal error                   | E0106: ROC internal error                   |
| 116        | E0116: no seller id                         | E0116: no seller id                         |
| 117        | E0117: no user id                           | E0117: no user id                           |
| 118        | E0118: no user email                        | E0118: no user email                        |
