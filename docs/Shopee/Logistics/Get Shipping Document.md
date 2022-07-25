---
sidebar_position: 4
---

# Get Shipping Document Parameter

```
GET /api/v2/logistics/get_shipping_document_parameter
```
Use this api to get the selectable shipping_document_type and suggested shipping_document_type

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
| -order_list | object[] | <Highlight>True</Highlight> |  | The list of orders you want to get. limit [1,50] |
| --order_sn | string | <Highlight>True</Highlight> | 201201E81SYYKE | Shopee's unique identifier for an order. |
| --package_number | string | <Highlight1>False</Highlight1> | 60489687088750 | Shopee's unique identifier for the package under an order. You should't fill the field with empty string when there is't a package number. |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| request_id | string | 8412939d0fbd48c9a548fba4b710a7f6 | The identifier for an API request for error tracking. |
| error | string | error_auth | Indicate error type if hit error. Empty if no error happened. |
| message | string | Invalid access_token. | Indicate error details if hit error. Empty if no error happened. |
| -warning | object[] |  | Indicate warning message you should take care. |
| --order_sn | string | 201201V81SYYDG | Shopee's unique identifier for an order. |
| --package_number | string |  | Shopee's unique identifier for the package under an order. |
| -response | object |  | Detail informations you are querying |
| --order_sn | string | 201201E81SYYKE | Shopee's unique identifier for an order. |
| --package_number | string | 60489687088750 | Shopee's unique identifier for the package under an order. |
| --suggest_shipping_document_type | string | THERMAL_AIR_WAYBILL | The shipping document type Shopee suggests. If you don't select any shipping document type, Shopee will use this as default shipping document type. |
| --selectable_shipping_document_type | string[] | THERMAL_AIR_WAYBILL | The shipping document type you can select of this order. |
| --fail_error | string | logistics.order_not_exist | Indicate error type if one element hit error. |
| --fail_message | string | The order_sn 201201V81SYYDG you provided is not exist. Please check | Indicate error details if one element hit error. |

## Request Example

```js title="Payload"
{
    "order_list": [
        {
            "order_sn": "201201E81SYYKE",
            "package_number": "60489687088750"
        },
        {
            "order_sn": "201201V81SYYDG"
        }
    ]
}
```

## Response Example

```js title="JSON"
{
    "error": "",
    "message": "",
    "response": {
        "result_list": [
            {
                "order_sn": "201201E81SYYKE",
                "package_number": "60489687088750",
                "suggest_shipping_document_type": "THERMAL_AIR_WAYBILL",
                "selectable_shipping_document_type": [
                    "THERMAL_AIR_WAYBILL"
                ]
            },
            {
                "order_sn": "201201V81SYYDG",
                "fail_error": "logistics.order_not_exist",
                "fail_message": "The order_sn 201201V81SYYDG you provided is not exist. Please check"
            }
        ]
    },
    "warning": [
        {
            "order_sn": "201201V81SYYDG"
        }
    ],
    "request_id": "8412939d0fbd48c9a548fba4b710a7f6"
}
```

## Error Example
No Error Example Set

## Error Codes

| Error | Error Description |
| :--- | :--- |
| logistics.error_param | The order is being allocated, please wait until the allocate is completed. |
| common.batch_api_all_failed | Failed, please check result_list for more details. |
| error_not_found | Wrong parameters, detail: {msg}. |
| error_param | Wrong parameters, detail: {msg}. |
| error_permission | Sorry you don't have the permission, detail: {msg}. |
| error_server | System error. Please try again later. |
| logistics.package_number_not_found | The package_number {package_number} is not exist. |
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
