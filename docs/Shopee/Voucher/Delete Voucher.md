---
sidebar_position: 2
---

# Delete Voucher

```
POST /api/v2/voucher/delete_voucher
```
Delete voucher

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
| voucher_id | int | <Highlight>True</Highlight> | 1104340665 | The unique identifier for the voucher you want to delete. |

## Response Parameters

| Name | Type | Sample | Description |
| :--- | :--- | :--- | :--- |
| error | string |  | Indicate error type if hit error. Empty if no error happened. |
| message | string |  | Indicate error details if hit error. Empty if no error happened. |
| request_id | string | 034f813abf5e11eb9c4eacde48001122 | The identifier of the API request for error tracking. |
| -response | object |  | Detail informations you are querying. |
| --voucher_id | int | 1104340665 | The unique identifier for the voucher it is being deleted. |

## Request Example

```js title="Payload"
{"voucher_id":1104340665}
```

## Response Example

```js title="JSON"
{
    "response": {
        "voucher_id": 1104340665
    },
    "request_id": "034f813abf5e11eb9c4eacde48001122",
    "error": "",
    "message": ""
}
```

## Error Example
No Error Example Set

## Error Codes

| Error | Error Description |
| :--- | :--- |
| voucher.delete_voucher_error | Can only delete upcoming voucher. |
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
| common.error_not_found | The information you queried is not found. |
| common.error_server | Internal server error |
| common.error_shop | Shopid is invalid |
| voucher.operate_voucher_permission_error | The Voucher created in Shopee admin/Shop Game/Follow Prize/Member ship/Voucher campaign can't be updated |
