---
sidebar_position: 1
---

Create Shipping Document

```
POST /api/v2/logistics/create_shipping_document
```

Use this api to create shipping document task for each order or package

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

| Name                     | Type     | Required                       | Sample              | Description                                                                                                                                  |
| :----------------------- | :------- | :----------------------------- | :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- |
| -order_list              | object[] | <Highlight>True</Highlight>    |                     | The list of order you want to create shipping document. limit [1, 50]                                                                        |
| --order_sn               | string   | <Highlight>True</Highlight>    | 201118BCKPJQQ8      | Shopee's unique identifier for an order.                                                                                                     |
| --package_number         | string   | <Highlight1>False</Highlight1> | 2485710696837122445 | Shopee's unique identifier for the package under an order. You should't fill the field with empty string when there is not a package number. |
| --tracking_number        | string   | <Highlight1>False</Highlight1> |                     | The tracking number of order. Required except for the channel allow print before arrange shipment.                                           |
| --shipping_document_type | string   | <Highlight1>False</Highlight1> | NORMAL_AIR_WAYBILL  | The type of shipping document. Available values: NORMAL_AIR_WAYBILL,THERMAL_AIR_WAYBILL,NORMAL_JOB_AIR_WAYBILL,THERMAL_JOB_AIR_WAYBILL       |

## Response Parameters

| Name              | Type     | Sample                                                              | Description                                                      |
| :---------------- | :------- | :------------------------------------------------------------------ | :--------------------------------------------------------------- |
| request_id        | string   | 5551ce8db5314c70a362dfe33544f074                                    | The identifier of the API request for error tracking.            |
| error             | string   | error_auth                                                          | Indicate error type if hit error. Empty if no error happened.    |
| message           | string   | Invalid access_token.                                               | Indicate error details if hit error. Empty if no error happened. |
| -warning          | object[] |                                                                     | indicate warning message you should take care.                   |
| --order_sn        | string   | 201118BCKPJKW0                                                      | Shopee's unique identifier for an order.                         |
| --package_number  | string   | 12345678                                                            | Shopee's unique identifier for the package under an order.       |
| -response         | object   |                                                                     | Detail informations you are querying                             |
| --result_list     | object[] |                                                                     | Ths list of the result data.                                     |
| ---order_sn       | string   | 201118BCKPJQQ8                                                      | Shopee's unique identifier for an order.                         |
| ---package_number | string   | 2485710696837122445                                                 | Shopee's unique identifier for the package under an order.       |
| ---fail_error     | string   | logistics.order_not_exist                                           | Indicate error type if one element hit error.                    |
| ---fail_message   | string   | The order_sn 201118BCKPJKW0 you provided is not exist. Please check | Indicate error details if one element hit error.                 |

## Request Example

```js title="Payload"
{
    "order_list": [
        {
            "order_sn": "201118BCKPJQQ8",
            "package_number": "2485710696837122445"
        },
        {
            "order_sn": "201118BCKPJKW0",
            "package_number": "12345678"
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
                "order_sn": "201118BCKPJQQ8",
                "package_number": "2485710696837122445"
            },
            {
                "order_sn": "201118BCKPJKW0",
                "package_number": "12345678",
                "fail_error": "logistics.order_not_exist",
                "fail_message": "The order_sn 201118BCKPJKW0 you provided is not exist. Please check"
            }
        ]
    },
    "warning": [
        {
            "order_sn": "201118BCKPJKW0",
            "package_number": "12345678"
        }
    ],
    "request_id": "5551ce8db5314c70a362dfe33544f074"
}
```

## Error Example

No Error Example Set.

## Error Codes

| Error                                    | Error Description                                                                   |
| :--------------------------------------- | :---------------------------------------------------------------------------------- |
| logistics.error_param                    | The order is being allocated, please wait until the allocate is completed.          |
| logistics.order_status_error             | Order status does not support awb printing.                                         |
| common.batch_api_all_failed              | Failed, please check result_list for more details.                                  |
| error_not_found                          | Wrong parameters, detail: {msg}.                                                    |
| error_param                              | Wrong parameters, detail: {msg}.                                                    |
| error_permission                         | Sorry you don't have the permission, detail: {msg}.                                 |
| error_server                             | System error. Please try again later.                                               |
| logistics.shipping_document_type_invalid | The shipping_document_type is not invalid. Please check the shipping_document_type. |
| logistics.package_can_not_print          | The package can not print now.                                                      |
| logistics.package_number_not_found       | The package_number {package_number} is not exist.                                   |
| logistics.package_number_not_exist       | Please request with package_number for this split order.                            |
| logistics.tracking_number_invalid        | The tracking number is invalid. Please check the tracking number.                   |
| error_param                              | There is no access_token in query.                                                  |
| error_auth                               | Invalid access_token.                                                               |
| error_param                              | Invalid partner_id.                                                                 |
| error_param                              | There is no partner_id in query.                                                    |
| error_auth                               | No permission to current api.                                                       |
| error_param                              | There is no sign in query.                                                          |
| error_sign                               | Wrong sign.                                                                         |
| error_param                              | no timestamp                                                                        |
| error_param                              | Invalid timestamp                                                                   |
| error_network                            | Inner http call failed                                                              |