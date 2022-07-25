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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/order/reverse/reason/list</Highlight1>

Get the list of reject reason. Need to be used in all refuse refund actions

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

| Name                  | Type   | Required                      | Demo Value | Rule | Description           |
| :-------------------- | :----- | :---------------------------- | :--------- | :--- | :-------------------- |
| reverse_order_line_id | Number | <Highlight2>true</Highlight2> | 0          |      | reverse order line id |

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

| Name                | Type     | Demo Value   | Description           |
| :------------------ | :------- | :----------- | :-------------------- |
| data                | Object[] | []           | data                  |
| -reason_id          | Number   | 1000017      | reason id             |
| -muti_language_text | String   | out of stock | multi-language reason |
| -text               | String   | out of stock | english reason        |

### Response Example

---

```
{
  "code": "0",
  "data": [
    {
      "muti_language_text": "out of stock",
      "text": "out of stock",
      "reason_id": "1000017"
    },
    {
      "muti_language_text": "out of stock",
      "text": "out of stock",
      "reason_id": "1000017"
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

| Error Code | Error Message                                                  | Description                                                    |
| :--------- | :------------------------------------------------------------- | :------------------------------------------------------------- |
| 103        | E0103: reverse order line id is empty when query reject reason | E0103: reverse order line id is empty when query reject reason |
| 106        | E0106: ROC internal error                                      | E0106: ROC internal error                                      |
| 116        | E0116: no seller id                                            | E0116: no seller id                                            |
| 117        | E0117: no user id                                              | E0117: no user id                                              |
| 118        | E0118: no user email                                           | E0118: no user email                                           |
| 119        | E0119: cannot find any cancel reasons for these orders         | E0119: cannot find any cancel reasons for these orders         |
