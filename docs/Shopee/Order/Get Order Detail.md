---
sidebar_position: 2
---

# Get Order Detail

```
GET /api/v2/order/get_attributes
```
Use this api to get order detail



## Common Parameter

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
| :--- | :--- | :---     | :---   | :---        |
| order_sn_list | string[] | <Highlight>True</Highlight> | ["201214JASXYXY6"] | The set of order_sn. If there are multiple order_sn, you need to use English comma to connect them. limit [1,50] |
| response_optional_fields | string[] | <Highlight1>False</Highlight1> | ["buyer_user_id,buyer_username,estimated_shipping_fee"] | Indicate response fields you want to get. Please select from the below response parameters. If you input an object field, all the params under it will be included automatically in the response. If there are multiple response fields you want to get, you need to use English comma to connect them. Available values: buyer_user_id,buyer_username,estimated_shipping_fee,recipient_address,actual_shipping_fee ,goods_to_declare,note,note_update_time,item_list,pay_time,dropshipper,dropshipper_phone,split_up,buyer_cancel_reason,cancel_by,cancel_reason,actual_shipping_fee_confirmed,buyer_cpf_id,fulfillment_flag,pickup_done_time,package_list,shipping_carrier,payment_method,total_amount,buyer_username,invoice_data, checkout_shipping_carrier, reverse_shipping_fee, order_chargeable_weight_gram etc. |

## Response Parameters

| Name | Type | Sample |  Description |
| :--- | :--- | :---   |  :---        |
| request_id | string | a8e1b94f51d64540bf5762abe7783073 | The identifier for an API request for error tracking. |
| error | string | common.error_auth | Indicate error type if hit error. Empty if no error happened. |
| message | string | Invalid access_token. | Indicate error details if hit error. Empty if no error happened. |
| -response | object |  | Detail informations you are querying. | 
| --order_list | object[] |  | The list of orders |
| ---order_sn | string | 201214JASXYXY6 | Return by default. Shopee's unique identifier for an order. |
| ---region | string | MY | Return by default. The two-digit code representing the region where the order was made. |
| ---currency | string | MYR | Return by default. The three-digit code representing the currency unit for which the order was paid. |
| ---cod | boolean | false | Return by default. This value indicates whether the order was a COD (cash on delivery) order. |
| ---total_amount | float | 1004.00 | The total amount paid by the buyer for the order. This amount includes the total sale price of items, shipping cost beared by buyer; and offset by Shopee promotions if applicable. This value will only return after the buyer has completed payment for the order. |
| ---order_status | string | CANCELLED | Return by default. Enumerated type that defines the current status of the order. |
| ---shipping_carrier | string | Standard Delivery | The logistics service provider that the buyer selected for the order to deliver items. |
| ---payment_method | string | Bank Transfer | The payment method that the buyer selected to pay for the order. |
| ---estimated_shipping_fee | float | 4.0 | The estimated shipping fee is an estimation calculated by Shopee based on specific logistics courier's standard. |
| ---message_to_seller | string |  | Return by default. Message to seller. |
| ---create_time | timestamp | 1607930885 | Return by default. Timestamp that indicates the date and time that the order was created. |
| ---update_time | timestamp | 1608134691 | Return by default. Timestamp that indicates the last time that there was a change in value of order, such as order status changed from 'Paid' to 'Completed'. |
| ---days_to_ship | int | 2 | Return by default. Shipping preparation time set by the seller when listing item on Shopee. |
| ---ship_by_date | int | 1608103685 | Return by default. The deadline to ship out the parcel. |
| ---buyer_user_id | int | 9193214 | The user id of buyer of this order |
| ---buyer_username | string | Tom | The name of buyer |
| ---recipient_address | object |  | This object contains detailed breakdown for the recipient address. |
| ----name | string | Max | Recipient's name for the address. |
| ----phone | string | 3828203 | Recipient's phone number input when order was placed. |
| ----town | string | Sara | The town of the recipient's address. Whether there is a town will depend on the region and/or country. |
| ----district | string | Dada | The district of the recipient's address. Whether there is a district will depend on the region and/or country. |
| ----city | string | Asajaya | The city of the recipient's address. Whether there is a city will depend on the region and/or country. |
| ----state | string | Sarawak | The state/province of the recipient's address. Whether there is a state/province will depend on the region and/or country. |
| ----region | string | MY | The two-digit code representing the region of the Recipient |
| ----zipcode | string | 40009 | Recipient's postal code. |
| ----full_address | string | C-15-14 BLOK C JALAN 30/146, Asajaya, 40009, Sarawak | The full address of the recipient, including country, state, even street, and etc. |
| ---actual_shipping_fee | float | 2.0 | The actual shipping fee of the order if available from external logistics partners. |
| ---goods_to_declare | boolean | false | Only work for cross-border order.This value indicates whether the order contains goods that are required to declare at customs. "T" means true and it will mark as "T" on the shipping label; "F" means false and it will mark as "P" on the shipping label. This value is accurate ONLY AFTER the order trackingNo is generated, please capture this value AFTER your retrieve the trackingNo. |
| ---note | string | haha | The note seller made for own reference. |
| ---note_update_time | timestamp | 1608103685 | Update time for the note. |
| ---item_list | object[] |  | This object contains the detailed breakdown for the result of this API call. |
| ----item_id | int | 2600144043 | Shopee's unique identifier for an item. |
| ----item_name | string | backpack | The name of the item |
| ----item_sku | string | sku | A item SKU (stock keeping unit) is an identifier defined by a seller, sometimes called parent SKU. Item SKU can be assigned to an item in Shopee Listings. |
| ----model_id | int | 105933822990 | ID of the model that belongs to the same item |
| ----model_name | string | Grey blue 40*60cm | Name of the model that belongs to the same item. A seller can offer models of the same item. For example, the seller could create a fixed-priced listing for a t-shirt design and offer the shirt in different colors and sizes. In this case, each color and size combination is a separate model. Each model can have a different quantity and price. |
| ----model_sku | string | DMM1952804068 | A model SKU (stock keeping unit) is an identifier defined by a seller. It is only intended for the seller's use. Many sellers assign a SKU to an item of a specific type, size, and color, which are models of one item in Shopee Listings. |
| ----model_quantity_purchased | int | 1 | The number of identical items purchased at the same time by the same buyer from one listing/item. |
| ----model_original_price | float | 1000.0 | The original price of the item in the listing currency |
| ----model_discounted_price | float | 800.0 | The after-discount price of the item in the listing currency. If there is no discount, this value will be same as that of model_original_price. In case of bundle deal item, this value will return 0 as by design bundle deal discount will not be breakdown to item/model level. Due to technical restriction, the value will return the price before bundle deal if we don't configure it to 0. Please call GetEscrowDetails if you want to calculate item-level discounted price for bundle deal item. |
| ----wholesale | boolean | false | This value indicates whether buyer buy the order item in wholesale price. |
| ----weight | float | 1.0 | The weight of the item |
| ----add_on_deal | boolean | false | To indicate if this item belongs to an addon deal. |
| ----main_item | boolean | false | To indicate if this item is main item or sub item. True means main item, false means sub item. |
| ----add_on_deal_id | int | 7850296 | A unique ID to distinguish groups of items in Cart, and Order. (e.g. AddOnDeal) |
| ----promotion_type | string | flash_sale | Available type：product_promotion, flash_sale, group_by, bundle_deal, add_on_deal_main, add_on_deal_sub, add_on_free_gift_main, add_on_free_gift_sub |
| ----promotion_id | int | 7850297 | The ID of the promotion. |
| ----order_item_id | int | 2600144043 | The identify of order item. For items in one same bundle deal promotion, the order_item_id should share the same id, such as 1,2. For items not in bundle deal promotion, the order_item_id should be the same as item_id. |
| ----promotion_group_id | int | 7850298 | The identy of product promotion |
| ----image_info | object |  | Image info of the product |
| -----image_url | string | https://cf.shopee.com.my/file/a9930777e98444e8a55f2d23646b8026_tn | The image url of the product. Default to be variation image, if the model does not have a variation image, will use an item main image instead. |
| ----product_location_id | string[] | ["IDL", "IDG"] | The list of warehouse IDs of the item. |
| ---pay_time | timestamp | 1607930885 | The time when the order status is updated from UNPAID to PAID. This value is NULL when order is not paid yet. |
| ---dropshipper | string |  | For Indonesia orders only. The name of the dropshipper. |
| ---dropshipper_phone | string |  | The phone number of dropshipper, could be empty. |
| ---split_up | boolean | false | To indicate whether this order is split to fullfil order(forder) level. Call v2.order.split_order if it's "true". |
| ---buyer_cancel_reason | string | Need to Modify Oredr | Cancel reason from buyer, could be empty. |
| ---cancel_by | string | system | Could be one of buyer, seller, system or Ops. |
| ---cancel_reason | string | BACKEND_LOGISTICS_NOT_STARTED | Use this field to get reason for buyer, seller, and system cancellation. |
| ---actual_shipping_fee_confirmed | boolean | false | Use this filed to judge whether the actual_shipping_fee is confirmed. |
| ---buyer_cpf_id | string |  | Buyer's CPF number for taxation and invoice purposes. Only for Brazil order. |
| ---fulfillment_flag | string | fullfiled_by_shopee | Use this field to indicate the order is fulfilled by shopee or seller. Applicable values: fulfilled_by_shopee, fulfilled_by_cb_seller, fulfilled_by_local_seller. |
| ---pickup_done_time | timestamp | 0 | The timestamp when pickup is done. |
| ---package_list | object[] |  | The list of package under an order |
| ----package_number | string | "61630084074470" | Shopee's unique identifier for the package under an order. |
| ----logistics_status | string | LOGISTICS_INVALID | The Shopee logistics status for the order. Applicable values: See Data Definition-LogisticsStatus. |
| ----shipping_carrier | string | Standard Delivery | The logistics service provider that the buyer selected for the order to deliver items. |
| ----item_list | object[] |  | The list of items |
| -----item_id | int | 2600144043 | Shopee's unique identifier for an item. |
| -----model_id | int | 0 | Shopee's unique identifier for a model. |
| ----Parcel_chargeable_weight_gram | int | 500 | For CB shop, display weight used to calculate actual_shipping_fee for this parcel. |
| ---invoice_data | object |  | The invoice data of the order. pt: Nota Fiscal eletronica (NF-e) do pedido. |
| ----number | string |  | The number of the invoice. The number should be 9 digits. pt: número da NF-e. |
| ----series_number | string |  | The series number of the invoice. The series number should be 3 digits. pt: série da NF-e. |
| ----access_key | string |  | The access key of the invoice. The access key should be 44 digits. pt: chave de acesso da NF-e. |
| ----issue_date | timestamp |  | The issue date of the invoice. The issue date should be later than the order pay date. pt: data de emissão da NF-e. |
| ----total_value | float |  | The total value of the invoice. pt: valor total da NF-e (R$). |
| ----products_total_value | float |  | The products total value of the invoice. pt: valor total dos products (R$) da NF-e. |
| ----tax_code | string |  | The tax code for the invoice. The tax code should be 4 digits. pt: Código Fiscal de Operações e Prestações (CFOP) predominante na NF-e. |
| ---checkout_shipping_carrier | string | Standard Delivery | For non masking order, the logistics service provider that the buyer selected for the order to deliver items. For masking order, the logistics service type that the buyer selected for the order to deliver items. | 
| ---reverse_shipping_fee | float |  | Shopee charges the reverse shipping fee for the returned order.The value of this field will be non-negative. |
| ---order_chargeable_weight_gram | int | 500 | For CB shop, display weight used to calculate actual_shipping_fee for this order. |
| warning | string[] |  | Indicate warning message you should take care. |

## Request Example

```js title="Java"

Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.get("https://partner.shopeemobile.com/api/v2/order/get_order_detail?timestamp=timestamp&sign=sign&response_optional_fields=[buyer_user_id,buyer_username,estimated_shipping_fee]&shop_id=shop_id&partner_id=partner_id&order_sn_list=[201214JASXYXY6]&access_token=access_token")
.asString();
```

```js title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/order/get_order_detail?access_token=access_token&order_sn_list=%5B201214JASXYXY6%5D&partner_id=partner_id&response_optional_fields=%5Bbuyer_user_id%2Cbuyer_username%2Cestimated_shipping_fee%5D&shop_id=shop_id&sign=sign&timestamp=timestamp',
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

curl --location --request GET 'https://partner.shopeemobile.com/api/v2/order/get_order_detail?order_sn_list=[201214JASXYXY6]&access_token=access_token&timestamp=timestamp&sign=sign&response_optional_fields=[buyer_user_id,buyer_username,estimated_shipping_fee]&shop_id=shop_id&partner_id=partner_id' 
```

```js title="Python"
import requests

url = "https://partner.shopeemobile.com/api/v2/order/get_order_detail?access_token=access_token&order_sn_list=%5B201214JASXYXY6%5D&partner_id=partner_id&response_optional_fields=%5Bbuyer_user_id%2Cbuyer_username%2Cestimated_shipping_fee%5D&shop_id=shop_id&sign=sign&timestamp=timestamp"

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
        "order_list": [
            {
                " checkout_shipping_carrier": null,
                " reverse_shipping_fee.": null,
                "actual_shipping_fee ": null,
                "actual_shipping_fee_confirmed": false,
                "buyer_cancel_reason": "",
                "buyer_cpf_id": null,
                "buyer_user_id": 258065,
                "buyer_username": "drcbuy_uat_sg_1",
                "cancel_by": "",
                "cancel_reason": "",
                "cod": false,
                "create_time": 1632973421,
                "currency": "SGD",
                "days_to_ship": 3,
                "dropshipper": "",
                "dropshipper_phone": "",
                "estimated_shipping_fee": 3.99,
                "fulfillment_flag": "fulfilled_by_local_seller",
                "goods_to_declare": false,
                "invoice_data": null,
                "item_list": [
                    {
                        "item_id": 101513055,
                        "item_name": "Vitamin Bottles - Acc",
                        "item_sku": "",
                        "model_id": 0,
                        "model_name": "",
                        "model_sku": "",
                        "model_quantity_purchased": 1,
                        "model_original_price": 3000,
                        "model_discounted_price": 3000,
                        "wholesale": false,
                        "weight": 0.3,
                        "add_on_deal": false,
                        "main_item": false,
                        "add_on_deal_id": 0,
                        "promotion_type": "",
                        "promotion_id": 0,
                        "order_item_id": 101513055,
                        "promotion_group_id": 0,
                        "image_info": {
                            "image_url": "https://cf.shopee.sg/file/fe05b113170c5e97ed515cf0f2fb9c0e_tn"
                        },
                        "product_location_id": ["IDL", "IDG"]
                    }
                ],
                "message_to_seller": "",
                "note": "",
                "note_update_time": 0,
                "order_sn": "210930KJDNF06T",
                "order_status": "COMPLETED",
                "package_list": [
                    {
                        "package_number": "OFG86672620092786",
                        "logistics_status": "LOGISTICS_DELIVERY_DONE",
                        "shipping_carrier": "Singpost POPstation - LPS (seller)",
                        "item_list": [
                            {
                                "item_id": 101513055,
                                "model_id": 0
                            }
                        ]
                    }
                ],
                "pay_time": 1632973437,
                "payment_method": "Credit/Debit Card",
                "pickup_done_time": 1632973711,
                "recipient_address": {
                    "name": "Buyer",
                    "phone": "******10",
                    "town": "",
                    "district": "",
                    "city": "",
                    "state": "",
                    "region": "SG",
                    "zipcode": "820116",
                    "full_address": "BLOCK 116, EDGEFIELD PLAINS, #05-334, SG, 820116"
                },
                "region": "SG",
                "reverse_shipping_fee": 0,
                "ship_by_date": 1633405439,
                "shipping_carrier": "Singpost POPstation - LPS (seller)",
                "split_up": false,
                "total_amount": 2988.99,
                "update_time": 1633001809
            }
        ]
    },
    "request_id": "971b45d6a002bfc680019320c9a685a0"
}
```

## Error Example
No Error Example Set

## Error Codes
| Error | Error Description |
| :--- | :--- |
| error_not_found | Wrong parameters, detail: {msg}. |
| error_param | Wrong parameters, detail: {msg}. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| error_server | System error. Please try again later. |
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