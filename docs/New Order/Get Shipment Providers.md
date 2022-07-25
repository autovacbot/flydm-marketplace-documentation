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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/shipment/providers/get</Highlight1>

Use this API to get the list of all active shipping providers, which is needed when working with the SetStatusToPackedByMarketplace API.

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

| Name                             | Type     | Demo Value                       | Description                                                                                                                                                           |
| :------------------------------- | :------- | :------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data                             | Object   | {}                               | response data                                                                                                                                                         |
| -shipment_providers              | Object[] | []                               | shipment providers                                                                                                                                                    |
| --is_default                     | Number   | 1                                | This shipment provider will be the standard selection for order processing.                                                                                           |
| --tracking_code_example          | String   | 1200234789012                    | The example of tracking code.                                                                                                                                         |
| --enabled_delivery_options       | String   | []                               | Shipment provider's speed eligibility, which could be multiple values. Possible values are economy, standard, and express.                                            |
| --name                           | String   | NinjaVan API                     | Name of the shipment provider. This is the string that is needed for SetStatusToPackedByMarketplace.                                                                  |
| --cod                            | Number   | 1                                | The shipment provider will be available for cash on delivery orders.                                                                                                  |
| --tracking_code_validation_regex | String   | /^[0-9]{12}[-]{0,1}[0-9]{0,2}$/i | The regular expression for validation of tracking code. Example: /^[a-z0-9]{10}$/i Please check using http://regex101.com/#pcre.                                      |
| --tracking_url                   | String   | https://sofp.lazada.sg           | Shipment provider's tracking URL. Placeholder {{{TRACKING_NR}}} can be used for tracking code. Otherwise tracking code should be appended to the end of tracking URL. |
| --api_integration                | Number   | 1                                | Value will be 1 if this shipment provider has an API.                                                                                                                 |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "shipment_providers": [
      {
        "tracking_code_example": "1200234789012",
        "enabled_delivery_options": "[]",
        "name": "NinjaVan API",
        "cod": "1",
        "tracking_code_validation_regex": "/^[0-9]{12}[-]{0,1}[0-9]{0,2}$/i",
        "is_default": "1",
        "tracking_url": "https://sofp.lazada.sg",
        "api_integration": "1"
      },
      {
        "tracking_code_example": "1200234789012",
        "enabled_delivery_options": "[]",
        "name": "NinjaVan API",
        "cod": "1",
        "tracking_code_validation_regex": "/^[0-9]{12}[-]{0,1}[0-9]{0,2}$/i",
        "is_default": "1",
        "tracking_url": "https://sofp.lazada.sg",
        "api_integration": "1"
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

| Error Code | Error Message          | Description |
| :--------- | :--------------------- | :---------- |
|            | Query result is empty. |             |
