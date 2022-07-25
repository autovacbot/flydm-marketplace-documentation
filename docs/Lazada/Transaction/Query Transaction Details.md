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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/finance/transaction/details/get</Highlight1>

API to query seller transaction details within specific date range.

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

| Name                  | Type   | Required                      | Demo Value   | Rule | Description                                                                           |
| :-------------------- | :----- | :---------------------------- | :----------- | :--- | :------------------------------------------------------------------------------------ |
| - offset              | String | false                         | 0            |      | Number of transaction lines to skip at the beginning of the list.                     |
| - trans_type          | String | false                         | -1           |      | Transaction type ID.                                                                  |
| - trade_order_id      | String | false                         | 123123213213 |      | Order ID.                                                                             |
| - limit               | String | false                         | 100          |      | Number of lines of transactions to be extracted. The supported maximum number is 500. |
| - start_time          | String | <Highlight2>true</Highlight2> | 2021-01-01   |      | Starting date when transactions need to be extracted.                                 |
| - end_time            | String | <Highlight2>true</Highlight2> | 2021-01-05   |      | Ending date when transactions need to be extracted.                                   |
| - trade_order_line_id | String | false                         | 45645674566  |      | Order Item ID.                                                                        |

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

| Name                    | Type     | Demo Value                | Description                                                       |
| :---------------------- | :------- | :------------------------ | :---------------------------------------------------------------- |
| data                    | Object[] | data                      | Response body                                                     |
| -fee_type               | String   | 13                        | Transaction type ID.                                              |
| -details                | String   | details                   | Transaction details                                               |
| -seller_sku             | String   | sellerSKU                 | The seller SKU                                                    |
| -lazada_sku             | String   | Item test -123            | The Lazada SKU                                                    |
| -amount                 | String   | -0.62                     | Total transaction value                                           |
| -VAT_in_amount          | String   | 0.0672                    | The VAT in amount                                                 |
| -WHT_amount             | String   | 0.0112                    | The WHT amount                                                    |
| -WHT_included_in_amount | String   | Yes                       | The WHT included in amount or not                                 |
| -statement              | String   | 11 May 2016 - 17 May 2016 | Statement ID                                                      |
| -paid_status            | String   | Not paid                  | Yes / No                                                          |
| -order_no               | String   | 123445666666              | Order ID                                                          |
| -orderItem_no           | String   | 1666666                   | Order item number                                                 |
| -orderItem_status       | String   | orderItemStatus           | The order item status                                             |
| -shipping_provider      | String   | LEX                       | The shipping provider                                             |
| -shipping_speed         | String   | shippingSpeed             | The shipping speed                                                |
| -shipment_type          | String   | Dropshipping              | The shipment type                                                 |
| -reference              | String   | 1340                      | The Order Item ID (the Sub-order ID of "Order ID" parameter)      |
| -comment                | String   | comment                   | Comments by regional finance team                                 |
| -payment_ref_id         | String   | paymentRefId              | Payment reference ID from bank or other payment provider          |
| -fee_name               | String   | feeName                   | feeName                                                           |
| -transaction_date       | String   | 17 May 2016               | Date of the transaction                                           |
| -transaction_type       | String   | Payment Fee               | Transaction type or fee name                                      |
| -transaction_number     | String   | SG103EF-1P9VK1A           | Unique ID of the transaction in the format "Seller code- xxxxxxx" |

### Response Example

---

```
{
  "code": "0",
  "data": [
    {
      "order_no": "123445666666",
      "transaction_date": "17 May 2016",
      "amount": "-0.62",
      "paid_status": "Not paid",
      "shipping_provider": "LEX",
      "WHT_included_in_amount": "Yes",
      "payment_ref_id": "paymentRefId",
      "lazada_sku": "Item test -123",
      "fee_type": "13",
      "transaction_type": "Payment Fee",
      "orderItem_no": "1666666",
      "orderItem_status": "orderItemStatus",
      "reference": "1340",
      "fee_name": "feeName",
      "shipping_speed": "shippingSpeed",
      "WHT_amount": "0.0112",
      "transaction_number": "SG103EF-1P9VK1A",
      "seller_sku": "sellerSKU",
      "statement": "11 May 2016 - 17 May 2016",
      "details": "details",
      "comment": "comment",
      "VAT_in_amount": "0.0672",
      "shipment_type": "Dropshipping"
    },
    {
      "order_no": "123445666666",
      "transaction_date": "17 May 2016",
      "amount": "-0.62",
      "paid_status": "Not paid",
      "shipping_provider": "LEX",
      "WHT_included_in_amount": "Yes",
      "payment_ref_id": "paymentRefId",
      "lazada_sku": "Item test -123",
      "fee_type": "13",
      "transaction_type": "Payment Fee",
      "orderItem_no": "1666666",
      "orderItem_status": "orderItemStatus",
      "reference": "1340",
      "fee_name": "feeName",
      "shipping_speed": "shippingSpeed",
      "WHT_amount": "0.0112",
      "transaction_number": "SG103EF-1P9VK1A",
      "seller_sku": "sellerSKU",
      "statement": "11 May 2016 - 17 May 2016",
      "details": "details",
      "comment": "comment",
      "VAT_in_amount": "0.0672",
      "shipment_type": "Dropshipping"
    }
  ],
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
