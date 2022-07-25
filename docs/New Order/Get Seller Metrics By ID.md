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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/seller/metrics/get</Highlight1>

Provide seller metrics data of the specific seller, like positive seller rating, ship on time rate and etc.

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

| Name | Type | Required | Demo Value | Rule | Description |
| :--- | :--- | :------- | :--------- | :--- | :---------- |

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

| Name                    | Type   | Demo Value        | Description            |
| :---------------------- | :----- | :---------------- | :--------------------- |
| data                    | Object | {}                | response data          |
| -main_category_name     | String | Furniture & Décor | main_category_name     |
| -seller_id              | Number | 1000038888        | seller_id              |
| -response_rate          | String | 1.0000            | response_rate          |
| -response_time          | String | 10.3333           | response_time          |
| -ship_on_time           | String | 93.62             | ship_on_time           |
| -main_category_id       | Number | 10000336          | main_category_id       |
| -positive_seller_rating | String | 67.0              | positive_seller_rating |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "main_category_name": "Furniture \u0026 Décor",
    "ship_on_time": "93.62",
    "positive_seller_rating": "67.0",
    "response_time": "10.3333",
    "seller_id": "1000038888",
    "response_rate": "1.0000",
    "main_category_id": "10000336"
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

| Error Code | Error Message          | Description |
| :--------- | :--------------------- | :---------- |
|            | Query result is empty. |             |
