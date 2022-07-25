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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/order/document/awb/pdf/get</Highlight1>


Use this API to retrieve order-related documents, only for shipping labels.

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

| Name             | Type   | Required                      | Demo Value       | Rule               | Description                                                                           |
| :--------------- | :----- | :---------------------------- | :--------------- | :----------------- | :------------------------------------------------------------------------------------ |
| - order_item_ids | String | <Highlight2>true</Highlight2> | [279709, 279709] | Max List Size: 100 | Identifier of the order item for which the caller wants to get a document. Mandatory. |

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

| Name                                                                                                             | Type   | Demo Value                         | Description                                                                                                             |
| :--------------------------------------------------------------------------------------------------------------- | :----- | :--------------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
| data                                                                                                             | Object | {}                                 | response data                                                                                                           |
| -document                                                                                                        | Object | {}                                 | document                                                                                                                |
| --file [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297) | String | PHN0eWxlPnRlRrU3VRbUNDJyAvPjwvcD4K | To reconstruct the file, the data from the node needs to be base64 decoded, and interpreted according to the mime_type. |
| --mime_type                                                                                                      | String | text/html                          | To reconstruct the file, the data from the node needs to be base64 decoded, and interpreted according to the mime_type. |
| --document_type                                                                                                  | String | shippingLabel                      | Document types, only shippingLabel                                                                                      |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "document": {
      "file": "PHN0eWxlPnRlRrU3VRbUNDJyAvPjwvcD4K",
      "mime_type": "text/html",
      "document_type": "shippingLabel"
    }
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
