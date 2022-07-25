---
sidebar_position: 8
---

# Update Shipping Order

```
POST /api/v2/logistics/update_shipping_order
```
Use this api update pickup address and pickup time for shipping order

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
| order_sn | string | <Highlight>True</Highlight> | 201214JASXYXY6 | Shopee's unique identifier for an order. |
| package_number | string | <Highlight1>False</Highlight1> |  | Shopee's unique identifier for the package under an order. You should't fill the field with empty string when there is't a package number. |
| -pickup | object | <Highlight>True</Highlight> |  | Required parameter ONLY if GetParameterForInit returns "pickup" or if GetLogisticsInfo returns "pickup" under "info_needed" for the same order. Developer should still include "pickup" field in the call even if "pickup" has empty value. |
| --address_id | int | <Highlight>True</Highlight> | 126194 | The identity of address. Retrieved from get_shipping_parameter. |
| --pickup_time_id | string | <Highlight>True</Highlight> | 439291 | The pickup time id. Retrieved from get_shipping_parameter. |


## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| request_id | string | 3dad66f43b8447d282ae6da36626c6b7 | The identifier for an API request for error tracking. |
| error | string | error_auth | Indicate error type if hit error. Empty if no error happened. |
| message | string | Invalid access_token. | Indicate error details if hit error. Empty if no error happened. |

## Request Example

```js title="Payload"
{
	"order_sn": "201214JASXYXY6",
	"package_number": "-",
	"pickup": {
		"address_id": 126194,
		"pickup_time_id": "439291"
	}
}
```

```js title="Java"
Unirest.setTimeouts(0, 0);
HttpResponse<String> response = Unirest.post("https://partner.shopeemobile.com/api/v2/logistics/update_shipping_order?partner_id=partner_id&sign=sign&access_token=access_token&timestamp=timestamp&shop_id=shop_id")
.header("Content-Type","application/json")
.body("{
   \"order_sn\": \"201214JASXYXY6\",
   \"package_number\": \"-\",
   \"pickup\": {
      \"address_id\": 126194,
      \"pickup_time_id\": \"439291\"
   }
}")
.asString();
```

```java title="PHP"
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://partner.shopeemobile.com/api/v2/logistics/update_shipping_order?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => '{
    "order_sn": "201214JASXYXY6",
    "package_number": "-",
    "pickup": {
        "address_id": 126194,
        "pickup_time_id": "439291"
    }
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```

```js title="cURL"

curl --location --request POST 'https://partner.shopeemobile.com/api/v2/logistics/update_shipping_order?partner_id=partner_id&sign=sign&access_token=access_token&timestamp=timestamp&shop_id=shop_id' \
--header 'Content-Type: application/json' \
--data-raw '{
   "order_sn": "201214JASXYXY6",
   "package_number": "-",
   "pickup": {
      "address_id": 126194,
      "pickup_time_id": "439291"
   }
}'
```

```js title="Python"
import requests
import json

url = "https://partner.shopeemobile.com/api/v2/logistics/update_shipping_order?access_token=access_token&partner_id=partner_id&shop_id=shop_id&sign=sign&timestamp=timestamp"

payload=json.dumps({
  "order_sn": "201214JASXYXY6",
  "package_number": "-",
  "pickup": {
    "address_id": 126194,
    "pickup_time_id": "439291"
  }
})
headers = {
  'Content-Type': 'application/json'
}
response = requests.request("POST",url,headers=headers, data=payload, allow_redirects=False)

print(response.text)
```

## Response Example

```js title="JSON"
{
    "error": "",
    "message": "",
    "request_id": "3dad66f43b8447d282ae6da36626c6b7"
}
```
## Error Codes

| Error | Error Description |
| :--- | :--- |
| logistics.error_param | The address is invalid. Please check the address. |
| logistics.error_param | The address is invalid. Please check the address. |
| logistics.address_not_found | Address is not found. |
| logistics.ADDRESS_NOT_SUPPORT | Address is not supported. |
| logistics.address_not_supported | Address is not supported current operation. |
| logistics.error_param | The order is being allocated, please wait until the allocate is completed. |
| logistics.block_buyer_name | Buyer name is prohibited. |
| logistics.business_process_error | Business process failed. |
| logistics.business_validation_error | Business validation failed. |
| logistics.buyer_address_not_found | Buyer address is not found. |
| logistics.error_param |Please wait for buyer to reselect the delivery convenience store.  |
| logistics.error_param | Logistic status is not supported. |
| logistics.cancel_not_allowed | Cancel is not allowed. |
| logistics.category_prohibited | There are contraband goods in the order. |
| logistics.error_channel_exist | Fail to find the fulfillment channel of this order. |
| logistics.error_param | Deliver address not support COD. |
| logistics.error_param | Delivery address do not support COD. |
| logistics.error_param | This address do not support delivery. |
| logistics.error_param | Delivery address is not exist. |
| logistics.error_param | Buyer address is not exist. |
| logistics.error_param | Delivery store is not exist. |
| logistics.error_param | Delivery address is not completed |
| logistics.error_address | Address is invalid. Please check the address. |
| logistics.error_param | The address is invalid. Please check the address. |
| logistics.error_limit | The batch request reach limit 50. |
| logistics.error_buyer_addressid | Buyer addressid is invalid. Please check the buyer addressid. |
| logistics.error_param | This order is not allowed to cancel. |
| logistics.error_cannot_cancel_logistic_txn | Cancel operation is not supported for current logistics txn. |
| logistics.error_param | Error, please check the channel. |
| logistics.error_param | Fast Escrow ID was not found ! |
| logistics.error_param | COD is currently not supported in the area. Please check Shopee Help Center for COD serviceable area. |
| logistics.error_connection | Connection to external system is failed. |
| logistics.error_consignment | Fail to get consignment number. |
| logistics.error_consignment_no_accepted | Consignment number is not allow to update. |
| logistics.error_core_server | Fail to call core server. |
| logistics.error_other | System error, please try again later. |
| logistics.error_param | System error, please try again later. |
| logistics.error_cutoff_time | Pickup time is not invalid. Please check the pickup time. |
| logistics.error_decimal | Receive invalid decimal. |
| logistics.error_duplicate_consignment | Consignment number is duplicated. |
| logistics.error_duplicated_consignment | Consignment number is duplicate. |
| logistics.error_expired | Order is expired. |
| logistics.error_failed_get_nearest_whs_idn | Faile to get the nearest whsId. |
| logistics.error_not_exist | Forder is not exist. |
| logistics.error_param | System error, please try again later. |
| logistics.error_format | Content format from external system is invalid. Please check the format. |
| logistics.error_param | System error, please try again later. |
| logistics.error_other | System error, please try again later. |
| logistics.error_invalid_channel_id | Channel id is invalid. Please check the channel. |
| logistics.error_param | The forder_ids should belong to one order/orderId and forderIds cannot be empty at the same time/parse forderId error. |
| logistics.error_param | System error, please try again later |
| logistics.error_ip | Ip address: {ip} is deny. |
| logistics.error_other | System error, please try again later. |
| logistics.error_param | Items in the same bundle should be in the same parcel. |
| logistics.error_item_not_found | Can not find the item. |
| logistics.error_param | System error, please try again later. |
| logistics.error_loginfo | Logistic info is invalid. Please check the logistic info. |
| logistics.error_logistic_txn_not_found | Logistics record is not found. |
| logistics.error_logistics_shop_require_pickup_address | Pickup address is required. |
| logistics.error_limit | Can not update order logistics in current status. |
| logistics.error_message_type | Message type is invalid. Please check the message type. |
| logistics.error_method | Operation is not supported. |
| logistics.error_missing_cdt | Cdt settings is not found. |
| logistics.error_param | Seller address is invalid. Please check your address. |
| logistics.error_no_pickup | Pickup is not supported. |
| logistics.error_no_pickup_address | Pickup address is missing. |
| error_not_found | Wrong parameters, detail: {msg}. |
| logistics.error_operation_failed | Operation failed. |
| logistics.error_order_context | Order context is invalid. Please check the order context. |
| logistics.error_param | Order list length exceeds limit. |
| logistics.error_param | System error, please try again later. |
| logistics.error_param | This order is not allowed to cancel. |
| logistics.error_param | Order is not exist. |
| logistics.error_order_not_found | Order is not found. |
| logistics.error_param | This order can not be splited. |
| logistics.error_param | Order is not splittable. |
| logistics.error_param | Parcels of this order can not be combined. |
| logistics.error_param | Order/Forder can not update. |
| logistics.error_param | Order has been shipped. |
| logistics.error_param | Order has been splitted. |
| logistics.error_order_state | Operation is not allow with current order status. |
| logistics.error_param | The order status is not ready to ship. |
| error_param | Wrong parameters, detail: {msg}. |
| logistics.error_limit | Parcel count should not exceed limit. |
| logistics.error_param | System error, please try again later. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| logistics.error_phone | Phone number is invalid. Please check the phone number. |
| logistics.error_pickup_time | Pickup time is invalid. Please check the pick up time. |
| logistics.error_param | The buyer address is invalid. Please check the buyer address. |
| logistics.error_return_tracking_num_not_found | Return tracking number is not found. |
| logistics.error_not_exist | Address does not exist. |
| logistics.error_seller_never_apply_tracking_no_before | History is not found. |
| logistics.error_sender_address | Sender address is invalid. Please check the sender address. |
| error_server | System error. Please try again later. |
| logistics.error_set_asf_by_weight | Fail to set actual shipping fee. |
| logistics.error_set_seller_address | Fail to set seller address. |
| logistics.error_param | System error, please try again later. |
| logistics.error_param | Shop not found. |
| logistics.error_param | Only support local warehouse, this shop do not support local warehouse. |
| logistics.error_param | This shop do not support split parcels. |
| logistics.error_param | System error, please try again later. |
| logistics.error_param | Size setting error. |
| logistics.error_other | System error, please try again later. |
| logistics.error_state | Currently, operation is not supported with current logistics record status. |
| logistics.error_status | Operation is not supported with current logistics record status. |
| logistics.error_store_not_found | Store is not found. |
| logistics.error_param | System error, please try again later. |
| logistics.error_other | System error, please try again later. |
| logistics.error_third_party_server | Failed to call external system. |
| logistics.error_param | System error, please try again later. |
| logistics.error_param | System error, please try again later. |
| logistics.error_timeout | Timeout to call external system. |
| logistics.error_token | Token is invalid. Please check the token. |
| logistics.error_too_many_invoke_function | Failed to get lock. |
| logistics.error_traceno_required | Trace number is required. |
| logistics.error_unknown | Unknown exception, exception details is: {details}. |
| logistics.error_unsupported | Operation is not supported. |
| logistics.error_unsupported_address | Address is not supported. |
| logistics.error_param | Invalid logistics channel. Please check the logictics channel. |
| logistics.error_param | Thaipost do not support this country. |
| logistics.error_param | System error, please try again later. |
| logistics.error_update | Fail to update. |
| logistics.error_update_logistic_unsupported | Currently, logistics is not supported to update. |
| logistics.error_param | Can not update order logistics. |
| logistics.error_param | Warehouse address not supported. |
| logistics.error_other | System error, please try again later. |
| logistics.error_other | System error, please try again later. |
| logistics.error_zipcode_not_found | Zipcode is not found. |
| logistics.feature_not_supported | Feature is not supported. |
| logistics.error_param | The EMS tracking number must begin with “E” |
| logistics.error_param | The EMS tracking number must end with “TH” |
| logistics.error_param | The Registered Mail tracking number must begin with “E”, “R” or “O” |
| logistics.error_param | The Registered Mail tracking number must end with “TH” |
| logistics.error_param | Please fill in a valid tracking number (13 digits) |
| logistics.error_param | The tracking number has been used by other orders, please fill in a valid one. |
| logistics.error_param | Please fill in the tracking number (13 digits) |
| logistics.invalid_size | Size is invalid. Please check the |
| logistics.error_data | Store status is unavailable,pending buyer update. |
| logistics.item_is_in_bundle | Channel is not allow to disable due to there is item in the bundle. |
| logistics.logistic_order_is_locked_on_creating | Fail to get the lock. |
| logistics.max dimension is limited | Max dimension or weight is limited. |
| logistics.error_param | Package exceeds weight limit. Please adjust or contact Shopee CS for more info. |
| logistics.missing_cdt | Cdt settings is missing. |
| logistics.no buyer_store | Buyer store is missing. |
| logistics.no_proportion | Can Not Found Proportion. |
| logistics.not_found | Not found. |
| logistics.order not found | Relative order is not found. |
| logistics.order_finalized | Order is already in finalized status. |
| logistics.order_not_ready_to_update | The order status is not ready to update. |
| logistics.package_not_exist | The package is not exist. |
| logistics.parcel_amount_over_limit | The order amount is over limit. |
| logistics.pickup_whitelist_not_supported | Permission is deny for pickup. |
| logistics.error_other | Pick up address not support COD. |
| logistics.error_param | Pickup address do not support COD. |
| logistics.error_other | Can not support deliver address. |
| logistics.error_other | Can not support pick up address. |
| logistics.error_param | This address do not support pickup. |
| logistics.pickup_address_unsupported | Pickup address is not supported. |
| logistics.error_param | System error, please try again later. |
| logistics.price_error | The price is invalid. Please check the price. |
| logistics.quantity_error | The quantity is invalid. Please check the quantity. |
| logistics.RcvStoreId not found | Receiver storeid is not found. |
| logistics.error_param | Seller address is not completed. |
| logistics.seller_address_not_support_cod | Cod pickup is not supported with the seller address. |
| logistics.error_param | Seller address is not exist. Please try other address. |
| logistics.error_param | Sender address is not exist. |
| logistics.ship_order_need_address_pickup_time | Parameter address_id and pickup_time_id are required. |
| logistics.ship_order_need_pacakge_number | Please request with package_number for this split order. |
| logistics.ship_order_need_tracking_number | Parameter tracking_number can not be null. |
| logistics.ship_order_not_need_pacakge_number | Please don’t request with package_number for this unsplit order. |
| logistics.ship_order_only_support_one_type | Please select just one way to ship order: pickup or dropoff or non_integrated. |
| logistics.ship_order_pff_init | You can not ship warehouse order. |
| logistics.ship_order_pickup_time_invalid | Invalid pickup time id. Please check the pick up time id. |
| logistics.ship_order_unsupport_pickup | This order does not support ship with pickup. |
| logistics.shop_not_found | Shop is not found. |
| logistics.shop_not_support_wms | Wms is not supported for the shop. |
| common.invalid_shop | Shop id is invalid. Please check your shop. |
| logistics.sls calculate fail | Fail to calculate estimated shipping fee. |
| logistics.error_param | The address is invalid. Please check the address. |
| logistics.error_param | Logistic status is not supported. |
| logistics.error_limit | Order status not support update logistics. |
| logistics.update_not_allowed | Currently, update is not allow. |
| logistics.update_shipping_order_no_param_change | You can’t update shipping with all the same parameters. |
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
