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

<Highlight color="#00A854">GET/POST</Highlight> <Highlight1 color="#EEEEEE">/reverse/getreverseordersforseller</Highlight1>

Use this API to get the list of items for a range of reverse orders.

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

| Name                | Type     | Required                      | Demo Value           | Rule              | Description                          |
| :------------------ | :------- | :---------------------------- | :------------------- | :---------------- | :----------------------------------- |
| ofc_status_list     | String[] | false                         | ["RETURN_CANCELED"]  |                   | Limit the ofc status                 |
| reverse_order_id    | Number   | false                         | 0                    |                   | Specify trade order id               |
| trade_order_id      | Number   | false                         | 0                    |                   | Specify reverse order id             |
| page_size           | Number   | <Highlight2>true</Highlight2> | 10                   | Default Value: 10 | Page size, default 10                |
| reverse_status_list | String[] | false                         | ["REQUEST_INITIATE"] |                   | Limit the reverse status.            |
| page_no             | Number   | <Highlight2>true</Highlight2> | 1                    | Default Value: 1  | Page no                              |
| return_to_type      | String   | false                         | RTM                  |                   | Return Type. Enum Values：[RTM, RTW] |
| dispute_in_progress | Boolean  | false                         | true                 |                   | Is dispute in progress               |

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

| Name                              | Type     | Demo Value       | Description                                                                                                        |
| :-------------------------------- | :------- | :--------------- | :----------------------------------------------------------------------------------------------------------------- |
| result                            | Object   | {}               | Response body                                                                                                      |
| -total                            | Number   | 50               | The total number of data                                                                                           |
| -items                            | Object[] | {}               | Data list                                                                                                          |
| --reverse_order_id                | Number   | 0                | Reverse order id                                                                                                   |
| --trade_order_id                  | Number   | 0                | Trade order id                                                                                                     |
| --request_type                    | String   | CANCEL           | Reverse request type                                                                                               |
| --is_rtm                          | Boolean  | true             | rtm:true, rtw:false                                                                                                |
| --shipping_type                   | String   | DEFAULT          | Shipping type                                                                                                      |
| --reverse_order_lines             | Object[] | [{}]             | Reverse order lines list                                                                                           |
| --reverse_order_line_id           | Number   | 0                | Reverse order line id                                                                                              |
| ---trade_order_line_id            | Number   | 0                | Trade order line id                                                                                                |
| ---reverse_status                 | String   | REQUEST_INITIATE | Reverse order status                                                                                               |
| ---is_need_refund                 | String   | true             | Is need refund                                                                                                     |
| ---ofc_status                     | String   | RETURN_CANCELED  | Ofc status                                                                                                         |
| ---product                        | Object   | {}               | Product Object                                                                                                     |
| ----product_id                    | Number   | 0                | Product id                                                                                                         |
| ----product_sku                   | String   | 0                | Product sku                                                                                                        |
| ---product                        | Object   | {}               | Product Object                                                                                                     |
| ---buyer                          | Object   | {}               | Buyer Object                                                                                                       |
| ----buyer_id                      | Number   | 0                | Buyer id                                                                                                           |
| ---trade_order_gmt_create         | Number   | 0                | trade order create time                                                                                            |
| ---refund_amount                  | Number   | 0                | refund amount, currency in cent, except VN (for example for SG, 100 equals SGD $1; for VN, 10000 equals VND 10000) |
| ---reason_text                    | String   | Out of stock     | reverse reason                                                                                                     |
| ---reason_code                    | Number   | 123              | reverse reason code                                                                                                |
| ---refund_payment_method          | String   | Alipay           | payment method                                                                                                     |
| ---whqc_decision                  | String   | scrap            | warehouse decision                                                                                                 |
| ---return_order_line_gmt_create   | Number   | 0                | reverse order line create time                                                                                     |
| ---return_order_line_gmt_modified | Number   | 0                | reverse order line modified time                                                                                   |
| ---is_dispute                     | Boolean  | true             | is in dispute or not                                                                                               |
| ---seller_sku_id                  | String   | th-1000          | seller sku id                                                                                                      |
| ---item_unit_price                | Number   | 0                | price, currency in cent, except VN (for example for SG, 100 equals SGD $1; for VN, 10000 equals VND 10000)         |
| ---platform_sku_id                | String   | th-1001          | platform sku id                                                                                                    |
| -page_no                          | Number   | 1                | Page no                                                                                                            |
| -success                          | Boolean  | true             | Result                                                                                                             |
| -page_size                        | Number   | 10               | Page size                                                                                                          |

### Response Example

---

```
{
  "result": {
    "total": "50",
    "success": "true",
    "page_no": "1",
    "items": [
      {
        "reverse_order_lines": [
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          },
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          }
        ],
        "reverse_order_id": "0",
        "request_type": "CANCEL",
        "is_rtm": "true",
        "shipping_type": "DEFAULT",
        "trade_order_id": "0"
      },
      {
        "reverse_order_lines": [
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          },
          {
            "product": {
              "product_sku": "0",
              "product_id": "0"
            },
            "return_order_line_gmt_create": "0",
            "platform_sku_id": "th-1001",
            "is_need_refund": "true",
            "trade_order_gmt_create": "0",
            "reason_text": "Out of stock",
            "item_unit_price": "0",
            "trade_order_line_id": "0",
            "return_order_line_gmt_modified": "0",
            "ofc_status": "RETURN_CANCELED",
            "seller_sku_id": "th-1000",
            "refund_payment_method": "Alipay",
            "buyer": {
              "buyer_id": "0"
            },
            "reason_code": "123",
            "whqc_decision": "scrap",
            "reverse_status": "REQUEST_INITIATE",
            "refund_amount": "0",
            "is_dispute": "true",
            "reverse_order_line_id": "0"
          }
        ],
        "reverse_order_id": "0",
        "request_type": "CANCEL",
        "is_rtm": "true",
        "shipping_type": "DEFAULT",
        "trade_order_id": "0"
      }
    ],
    "page_size": "10"
  },
  "code": "0",
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

| Error Code | Error Message          | Description |
| :--------- | :--------------------- | :---------- |
|            | Query result is empty. |             |
