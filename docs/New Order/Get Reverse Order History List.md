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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/order/reverse/return/history/list</Highlight1>

Get the communication history of the reverse order

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
| page_size             | Number | false                         | 10         |      | default 10            |
| page_number           | Number | false                         | 1          |      | default 1             |

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

| Name                  | Type     | Demo Value    | Description         |
| :-------------------- | :------- | :------------ | :------------------ |
| data                  | Object   | {}            | {}                  |
| -list                 | Object[] | []            | history             |
| --operator            | String   | Jason         | operator            |
| --picture             | String[] | []            | picture url         |
| --time                | Number   | 1627562669235 | timestamp           |
| -page_info            | Object   | {}            | page info           |
| --page_size           | Number   | 10            | page size           |
| --current_page_number | Number   | 1             | current page number |
| --total               | Number   | 10            | total number        |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "page_info": {
      "total": "10",
      "page_size": "10",
      "current_page_number": "1"
    },
    "list": [
      {
        "time": "1627562669235",
        "operator": "Jason",
        "picture": [
          "[]",
          "[]"
        ]
      },
      {
        "time": "1627562669235",
        "operator": "Jason",
        "picture": [
          "[]",
          "[]"
        ]
      }
    ]
  },
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
| 120        | E0120: page size invalid                                       | E0120: page size invalid                                       |
| 121        | E0121: page number invalid                                     | E0121: page number invalid                                     |
