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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/order/items/get</Highlight1>

Use this API to get the item information of an order.

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

| Name       | Type   | Required                      | Demo Value | Rule | Description                                                         |
| :--------- | :----- | :---------------------------- | :--------- | :--- | :------------------------------------------------------------------ |
| - order_id | Number | <Highlight2>true</Highlight2> | 31202      |      | The identifier that was assigned to the order by the Seller Center. |

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

| Name                            | Type     | Demo Value                                                                                          | Description                                                                                                                                                                                                                                                    |
| :------------------------------ | :------- | :-------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data                            | Object[] | {}                                                                                                  | Response body                                                                                                                                                                                                                                                  |
| -pick_up_store_info             | Object   | {}                                                                                                  | Pick-up Store infos                                                                                                                                                                                                                                            |
| --pick_up_store_name            | String   | Alibaba                                                                                             | Pick-up Store's name                                                                                                                                                                                                                                           |
| --pick_up_store_address         | String   | Ali Center, Shenzhen                                                                                | Pick-up Store's address                                                                                                                                                                                                                                        |
| --pick_up_store_code            | String   | d4b04804-9192-4a8c-8ed1-5ebcd7d3c067                                                                | Pick-up Store's id                                                                                                                                                                                                                                             |
| --pick_up_store_open_hour       | String[] | ["Sunday 9:00-18:00", "Mondday,Tuesday,Wendnesday,Thursday,Friday 8:00-20:00"]                      | Pick-up Store's business hours                                                                                                                                                                                                                                 |
| -purchase_order_number          | String   | 345345                                                                                              | Returned when calling SetPackedByMarketPlace                                                                                                                                                                                                                   |
| -name                           | String   | Bean Rester Dooby Red                                                                               | Product name                                                                                                                                                                                                                                                   |
| -product_main_image             | String   | http://th-live-02.slatic.net/p/3/jianyue-7699-09550735-ccd244666871f12a523c77d68cd76d74-catalog.jpg | Product main image URL                                                                                                                                                                                                                                         |
| -item_price                     | String   | 99.00                                                                                               | Product price                                                                                                                                                                                                                                                  |
| -tax_amount                     | String   | 6.48                                                                                                | Tax amount                                                                                                                                                                                                                                                     |
| -status                         | String   | canceled                                                                                            | Status                                                                                                                                                                                                                                                         |
| -cancel_return_initiator        | String   | cancellation-customer                                                                               | Indicates who initiated the canceled or returned order. Possible values are cancellation-internal, cancellation-customer, cancellation-failed Delivery, cancellation-seller, return-customer, and refund-internal.                                             |
| -voucher_platform               | String   | 0.00                                                                                                | The voucher that is issued by Lazada                                                                                                                                                                                                                           |
| -voucher_seller                 | String   | 0.00                                                                                                | The voucher that is issued by the seller                                                                                                                                                                                                                       |
| -order_type                     | String   | Normal                                                                                              | The type of order，maybe Normal, PreSale, Coupon, O2O or InStoreO2O                                                                                                                                                                                            |
| -stage_pay_status               | String   | unpaid                                                                                              | The payment status of Presale order at presale stage. The possible values are null, "unpaid" or "unpaid final payment". (unpaid: presale deposit has not been paid; unpaid final payment: presale deposit is paid but final payment / balance due is not paid) |
| -warehouse_code                 | String   | WH-01                                                                                               | Warehouse Code of multi-wh sellers                                                                                                                                                                                                                             |
| -voucher_seller_lpi             | String   | 0.00                                                                                                | The Lazada Bonus that is sponsored by the seller                                                                                                                                                                                                               |
| -voucher_platform_lpi           | String   | 0.00                                                                                                | The Lazada Bonus that is sponsored by Lazada                                                                                                                                                                                                                   |
| -buyer_id                       | String   | 1001                                                                                                | Buyer ID                                                                                                                                                                                                                                                       |
| -shipping_fee_original          | String   | 0.00                                                                                                | shipping fee original                                                                                                                                                                                                                                          |
| -shipping_fee_discount_seller   | String   | 0.00                                                                                                | shipping fee discount from seller                                                                                                                                                                                                                              |
| -shipping_fee_discount_platform | String   | 0.00                                                                                                | shipping fee discount from platform                                                                                                                                                                                                                            |
| -voucher_code_seller            | String   | X234                                                                                                | voucher code from seller                                                                                                                                                                                                                                       |
| -voucher_code_platform          | String   | Y123                                                                                                | voucher code from platform                                                                                                                                                                                                                                     |
| -delivery_option_sof            | String   | 0                                                                                                   | The mark of whether is seller own fleet, values included 1 and 0.                                                                                                                                                                                              |
| -is_fbl                         | String   | 0                                                                                                   | The mark of whether is fulfilled by LAZADA, values included 1 and 0.                                                                                                                                                                                           |
| -is_reroute                     | String   | 0                                                                                                   | The mark of whether is secondary sale, values included 1 and 0.                                                                                                                                                                                                |
| -reason                         | String   | reason                                                                                              | Cancel, Return or other reason, defined in the table sales_order_reason                                                                                                                                                                                        |
| -digital_delivery_info          | String   | delivery                                                                                            | Digital deliery information                                                                                                                                                                                                                                    |
| -promised_shipping_time         | String   | 2014-10-15 19:12:15 +0800                                                                           | Promised shipping time                                                                                                                                                                                                                                         |
| -order_id                       | String   | 31202                                                                                               | Order ID                                                                                                                                                                                                                                                       |
| -voucher_amount                 | String   | 0.00                                                                                                | Voucher amount                                                                                                                                                                                                                                                 |
| -return_status                  | String   | 1                                                                                                   | Return status                                                                                                                                                                                                                                                  |
| -shipping_type                  | String   | Dropshipping                                                                                        | Shipping type, Drop-shipping or Warehouse                                                                                                                                                                                                                      |
| -shipment_provider              | String   | LEL                                                                                                 | 3PL shipment provider, such as LEX                                                                                                                                                                                                                             |
| -variation                      | String   | 1                                                                                                   | Variation                                                                                                                                                                                                                                                      |
| -created_at                     | String   | 2014-10-15 19:12:15 +0800                                                                           | Time of the feed's creation in ISO 8601 format                                                                                                                                                                                                                 |
| -invoice_number                 | String   | 1342                                                                                                | Invoice number                                                                                                                                                                                                                                                 |
| -shipping_amount                | String   | 0.00                                                                                                | Shipping fee                                                                                                                                                                                                                                                   |
| -currency                       | String   | SGD                                                                                                 | ISO 4217 compatible currency code                                                                                                                                                                                                                              |
| -order_flag                     | String   | GUATANTEE                                                                                           | The type of order, Possible values are GUARANTEE, NORMAL and GLOBAL_COLLECTION. Orders tagged with "GUARANTEE" or "GLOBAL_COLLECTION" have shorter SLA requirement in order fulfillment.                                                                       |
| -shop_id                        | String   | dawen dp                                                                                            | Seller name                                                                                                                                                                                                                                                    |
| -sla_time_stamp                 | String   | 2019-06-24T23:59:59+08:00                                                                           | Time of the ship SLA in ISO 8601 format(yyyy-MM-dd'T'HH:mm:ssXXX)                                                                                                                                                                                              |
| -sku                            | String   | BRSD#02                                                                                             | Product SKU                                                                                                                                                                                                                                                    |
| -voucher_code                   | String   | X3453                                                                                               | Not used                                                                                                                                                                                                                                                       |
| -wallet_credits                 | String   | 0.00                                                                                                | Wallet credit                                                                                                                                                                                                                                                  |
| -updated_at                     | String   | 2014-10-15 19:12:15 +0800                                                                           | Time of the feed's last update in ISO 8601 format                                                                                                                                                                                                              |
| -is_digital                     | Number   | 0                                                                                                   | Is digital goods or not                                                                                                                                                                                                                                        |
| -tracking_code_pre              | String   | 23534                                                                                               | Not used                                                                                                                                                                                                                                                       |
| -order_item_id                  | Number   | 98108                                                                                               | Order item ID                                                                                                                                                                                                                                                  |
| -package_id                     | String   | 345                                                                                                 | Package source ID                                                                                                                                                                                                                                              |
| -tracking_code                  | String   | 456                                                                                                 | Tracking code retrieved from 3PL shipment provider                                                                                                                                                                                                             |
| -shipping_service_cost          | Number   | 0                                                                                                   | Shipping service cost                                                                                                                                                                                                                                          |
| -extra_attributes               | String   | null                                                                                                | JSON encoded string with extra attributes                                                                                                                                                                                                                      |
| -paid_price                     | String   | 99.00                                                                                               | Paid price                                                                                                                                                                                                                                                     |
| -hipping_provider_type          | String   | standard                                                                                            | One of the following options: EXPRESS, STANDARD, ECONOMY, INSTANT, SELLER_OWN_FLEET, PICKUP_IN_STORE or DIGITAL                                                                                                                                                |
| -product_detail_url             | String   | http://www.lazada.co.th/535590.html                                                                 | Product detail URL                                                                                                                                                                                                                                             |
| -shop_sku                       | String   | BE494HLAAUE3SGAMZ-39898                                                                             | Product outer ID                                                                                                                                                                                                                                               |
| -reason_detail                  | String   | reason detail                                                                                       | Reason detail                                                                                                                                                                                                                                                  |
| -purchase_order_id              | String   | 3454                                                                                                | Returned when calling SetPackedByMarketPlace                                                                                                                                                                                                                   |
| -sku_id                         | String   | 666                                                                                                 | Sku ID                                                                                                                                                                                                                                                         |
| -product_id                     | String   | 12345                                                                                               | Product ID                                                                                                                                                                                                                                                     |

### Response Example

---

```
{
  "code": "0",
  "data": [
    {
      "pick_up_store_info": {
        "pick_up_store_address": "Ali Center, Shenzhen",
        "pick_up_store_name": "Alibaba",
        "pick_up_store_open_hour": [
          "[\"Sunday 9:00-18:00\", \"Mondday,Tuesday,Wendnesday,Thursday,Friday 8:00-20:00\"]",
          "[\"Sunday 9:00-18:00\", \"Mondday,Tuesday,Wendnesday,Thursday,Friday 8:00-20:00\"]"
        ],
        "pick_up_store_code": "d4b04804-9192-4a8c-8ed1-5ebcd7d3c067"
      },
      "tax_amount": "6.48",
      "reason": "reason",
      "sla_time_stamp": "2019-06-24T23:59:59+08:00",
      "voucher_seller": "0.00",
      "purchase_order_id": "3454",
      "voucher_code_seller": "X234",
      "voucher_code": "X3453",
      "package_id": "345",
      "buyer_id": "1001",
      "variation": "1",
      "product_id": "12345",
      "voucher_code_platform": "Y123",
      "purchase_order_number": "345345",
      "sku": "BRSD#02",
      "order_type": "Normal",
      "invoice_number": "1342",
      "cancel_return_initiator": "cancellation-customer",
      "shop_sku": "BE494HLAAUE3SGAMZ-39898",
      "is_reroute": "0",
      "stage_pay_status": "unpaid",
      "sku_id": "666",
      "tracking_code_pre": "23534",
      "order_item_id": "98108",
      "shop_id": "dawen dp",
      "order_flag": "GUATANTEE",
      "is_fbl": "0",
      "name": "Bean Rester Dooby Red",
      "delivery_option_sof": "0",
      "order_id": "31202",
      "status": "canceled",
      "product_main_image": "http://th-live-02.slatic.net/p/3/jianyue-7699-09550735-ccd244666871f12a523c77d68cd76d74-catalog.jpg",
      "voucher_platform": "0.00",
      "paid_price": "99.00",
      "product_detail_url": "http://www.lazada.co.th/535590.html",
      "warehouse_code": "WH-01",
      "promised_shipping_time": "2014-10-15 19:12:15 +0800",
      "shipping_type": "Dropshipping",
      "created_at": "2014-10-15 19:12:15 +0800",
      "voucher_seller_lpi": "0.00",
      "shipping_fee_discount_platform": "0.00",
      "wallet_credits": "0.00",
      "updated_at": "2014-10-15 19:12:15 +0800",
      "currency": "SGD",
      "shipping_provider_type": "standard",
      "voucher_platform_lpi": "0.00",
      "shipping_fee_original": "0.00",
      "item_price": "99.00",
      "is_digital": "0",
      "shipping_service_cost": "0",
      "tracking_code": "456",
      "shipping_fee_discount_seller": "0.00",
      "shipping_amount": "0.00",
      "reason_detail": "reason detail",
      "return_status": "1",
      "shipment_provider": "LEL",
      "voucher_amount": "0.00",
      "digital_delivery_info": "delivery",
      "extra_attributes": "null"
    },
    {
      "pick_up_store_info": {
        "pick_up_store_address": "Ali Center, Shenzhen",
        "pick_up_store_name": "Alibaba",
        "pick_up_store_open_hour": [
          "[\"Sunday 9:00-18:00\", \"Mondday,Tuesday,Wendnesday,Thursday,Friday 8:00-20:00\"]",
          "[\"Sunday 9:00-18:00\", \"Mondday,Tuesday,Wendnesday,Thursday,Friday 8:00-20:00\"]"
        ],
        "pick_up_store_code": "d4b04804-9192-4a8c-8ed1-5ebcd7d3c067"
      },
      "tax_amount": "6.48",
      "reason": "reason",
      "sla_time_stamp": "2019-06-24T23:59:59+08:00",
      "voucher_seller": "0.00",
      "purchase_order_id": "3454",
      "voucher_code_seller": "X234",
      "voucher_code": "X3453",
      "package_id": "345",
      "buyer_id": "1001",
      "variation": "1",
      "product_id": "12345",
      "voucher_code_platform": "Y123",
      "purchase_order_number": "345345",
      "sku": "BRSD#02",
      "order_type": "Normal",
      "invoice_number": "1342",
      "cancel_return_initiator": "cancellation-customer",
      "shop_sku": "BE494HLAAUE3SGAMZ-39898",
      "is_reroute": "0",
      "stage_pay_status": "unpaid",
      "sku_id": "666",
      "tracking_code_pre": "23534",
      "order_item_id": "98108",
      "shop_id": "dawen dp",
      "order_flag": "GUATANTEE",
      "is_fbl": "0",
      "name": "Bean Rester Dooby Red",
      "delivery_option_sof": "0",
      "order_id": "31202",
      "status": "canceled",
      "product_main_image": "http://th-live-02.slatic.net/p/3/jianyue-7699-09550735-ccd244666871f12a523c77d68cd76d74-catalog.jpg",
      "voucher_platform": "0.00",
      "paid_price": "99.00",
      "product_detail_url": "http://www.lazada.co.th/535590.html",
      "warehouse_code": "WH-01",
      "promised_shipping_time": "2014-10-15 19:12:15 +0800",
      "shipping_type": "Dropshipping",
      "created_at": "2014-10-15 19:12:15 +0800",
      "voucher_seller_lpi": "0.00",
      "shipping_fee_discount_platform": "0.00",
      "wallet_credits": "0.00",
      "updated_at": "2014-10-15 19:12:15 +0800",
      "currency": "SGD",
      "shipping_provider_type": "standard",
      "voucher_platform_lpi": "0.00",
      "shipping_fee_original": "0.00",
      "item_price": "99.00",
      "is_digital": "0",
      "shipping_service_cost": "0",
      "tracking_code": "456",
      "shipping_fee_discount_seller": "0.00",
      "shipping_amount": "0.00",
      "reason_detail": "reason detail",
      "return_status": "1",
      "shipment_provider": "LEL",
      "voucher_amount": "0.00",
      "digital_delivery_info": "delivery",
      "extra_attributes": "null"
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

| Error Code | Error Message               | Description                          |
| :--------- | :-------------------------- | :----------------------------------- |
| 16         | E016: "%s" Invalid Order ID | The specified order ID is not valid. |
| 6          | E006: System Error          | System Error                         |
