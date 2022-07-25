---
sidebar_position: 2
---

Download Shipping Document

```
POST /api/v2/logistics/download_shipping_document
```
Use this api to download shipping_document. You have to call v2.logistics.create_shipping_document to create a new shipping document task first and call v2.logistics.get_shipping_document_resut to get the task status second. If the task is READY, you can download this shipping document.

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
| shipping_document_type | string | <Highlight1>False</Highlight1> | NORMAL_AIR_WAYBILL | The type of shipping document. Available values: NORMAL_AIR_WAYBILL,THERMAL_AIR_WAYBILL,NORMAL_JOB_AIR_WAYBILL,THERMAL_JOB_AIR_WAYBILL |
| -order_list | object[] | <Highlight>True</Highlight> |  | The list of orders you need to download it's shipping document. |
| --order_sn | string | <Highlight>True</Highlight> | 201118BCKPJQQ8 | Shopee's unique identifier for an order. |
| --package_number | string | <Highlight1>False</Highlight1> | 2485710696837122445 | Shopee's unique identifier for the package under an order. You should't fill the field with empty string when there is't a package number. |

## Response Parameters

## Request Example

```js title="Payload"
{
    "shipping_document_type": "NORMAL_AIR_WAYBILL",
    "order_list": [
        {
            "order_sn": "201118BCKPJQQ8",
            "package_number": "2485710696837122445"
        }
    ]
}
```

## Response Example

```js title="JSON"

If Success, this api will return a waybill file.
If Fail, this api will return the error message as the example below.
{
    "error":"logistics.xxxxx",
    "message":"The package can not print now, please .......",
    "request_id":"814468c0f07157681b78f6f0b58030db"
}
```
## Error Example
No Error Example

## Error Codes

| Error | Error Description |
| :--- | :--- |
| logistics.error_network | System error. Please try again later. |
| error_not_found | Wrong parameters, detail: {msg}. |
| error_param | Wrong parameters, detail: {msg}. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| error_server | System error. Please try again later. |
| logistics.unknown_error | Unknown error, please contact Shopee to check. Detail: {msg} |
| logistics.order_not_exist | The order_sn {order_sn} is not exist. |
| logistics.package_number_not_found | The package_number {package_number} is not exist. |
| logistics.package_print_failed | Some package failed to print, please try again later. Detail: {msg} |
| logistics.packages_can_not_download_together | Packages can not download together. Detail: {msg} |
| logistics.shipping_document_should_print_first | The package can not print now, please create shipping document first.Detail: {msg} |
| logistics.package_number_not_exist | Please request with package_number for this split order. |
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