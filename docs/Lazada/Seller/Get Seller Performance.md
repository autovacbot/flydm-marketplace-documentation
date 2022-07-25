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

<Highlight color="#00A854">GET/POST</Highlight> <Highlight1 color="#EEEEEE">/seller/performance/get</Highlight1>

Provide the performance metrics of the current seller, such as positive seller rating, ship on time, etc.

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

| Name     | Type   | Required | Demo Value | Rule | Description                                                                                                                |
| :------- | :----- | :------- | :--------- | :--- | :------------------------------------------------------------------------------------------------------------------------- |
| language | String | false    | en-US      |      | Optional ISO 639-1 standard language code (default: en-US, supported languages: en-US, zh-CN, ms-MY, th-TH, vi-VN, id-ID). |

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

| Name                | Type     | Demo Value                                                                                                                                     | Description                                                                                                                                                                                                                                            |
| :------------------ | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data                | Object   | N/A                                                                                                                                            | Response payload.                                                                                                                                                                                                                                      |
| -seller_id          | Number   | 42                                                                                                                                             | Seller ID.                                                                                                                                                                                                                                             |
| -main_category_id   | Number   | 12356                                                                                                                                          | Seller's main category ID.                                                                                                                                                                                                                             |
| -main_category_name | String   | Mobile & Tablet                                                                                                                                | Seller's main category name.                                                                                                                                                                                                                           |
| -indicators         | Object[] | N/A                                                                                                                                            | Performance indicators.                                                                                                                                                                                                                                |
| --type              | String   | POSITIVE_SELLER_RATING                                                                                                                         | Indicator type (e.g. POSITIVE_SELLER_RATING, PRODUCT_RATING_COVERAGE, ...).                                                                                                                                                                            |
| --name              | String   | Positive Seller Rating                                                                                                                         | Name of the indicator is the seller's language.                                                                                                                                                                                                        |
| --tip               | String   | Positive Seller Rating The ratio of total positive ratings to total ratings from verified buyers. This is measured for period of last 8 weeks. | Longer description of the indicator is the seller's language.                                                                                                                                                                                          |
| --score             | Number   | 92.0                                                                                                                                           | Raw score value. Note: if the indicator doesn't contain any value, a null value is set instead.                                                                                                                                                        |
| --score_format      | String   | PERCENTAGE                                                                                                                                     | Score format: INTEGER, DOUBLE, PERCENTAGE, MINUTES, HOURS.                                                                                                                                                                                             |
| --formatted_score   | String   | 92%                                                                                                                                            | Score formatted in the seller's language and locale. Note: if the indicator doesn't contain any value, a "-" is set instead.                                                                                                                           |
| --target            | Number   | 85.0                                                                                                                                           | Indicator target (raw value). Note: if the indicator doesn't contain any value, a null value is set instead.                                                                                                                                           |
| --target_format     | String   | GREATER_THAN_PERCENTAGE                                                                                                                        | Target format: GREATER_THAN_DOUBLE ('≥' #.##), GREATER_THAN_PERCENTAGE ('≥' #.##'%'), LOWER_THAN_PERCENTAGE('≤' #.##'%'), LOWER_THAN_MINUTES('≤' #'min'), STRICTLY_LOWER_THAN_HOURS('<' #'h'), GREATER_THAN_DOUBLE ('≥' #.##), EQUALS_TO_INTEGER(= #). |
| --formatted_target  | String   | ≥ 85%                                                                                                                                          | Indicator target formatted in the seller's language and locale.                                                                                                                                                                                        |
| --target_respected  | Boolean  | true                                                                                                                                           | true if the formattedScore respects the formattedTarget, false if not.                                                                                                                                                                                 |
| --action_url        | String   | /apps/review/manage                                                                                                                            | Relative (from the Seller Portal) or absolute URL to redirect the seller to the page where he cans handle the task.                                                                                                                                    |
| success             | Boolean  | true                                                                                                                                           | true for success, false for error.                                                                                                                                                                                                                     |
| error_code          | String   | REQUEST_CANNOT_BE_NULL                                                                                                                         | Error code if success = false.                                                                                                                                                                                                                         |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "main_category_name": "Mobile \u0026 Tablet",
    "indicators": [
      {
        "action_url": "/apps/review/manage",
        "score": "92.0",
        "score_format": "PERCENTAGE",
        "formatted_score": "92%",
        "name": "Positive Seller Rating",
        "tip": "\u003cdiv style\u003d\u0027font-weight: bold\u0027 \u003ePositive Seller Rating\u003c/div\u003e\u003cbr /\u003eThe ratio of total positive ratings to total ratings from verified buyers. This is measured for period of last 8 weeks.",
        "type": "POSITIVE_SELLER_RATING",
        "formatted_target": "≥ 85%",
        "target": "85.0",
        "target_format": "GREATER_THAN_PERCENTAGE",
        "target_respected": "true"
      },
      {
        "action_url": "/apps/review/manage",
        "score": "92.0",
        "score_format": "PERCENTAGE",
        "formatted_score": "92%",
        "name": "Positive Seller Rating",
        "tip": "\u003cdiv style\u003d\u0027font-weight: bold\u0027 \u003ePositive Seller Rating\u003c/div\u003e\u003cbr /\u003eThe ratio of total positive ratings to total ratings from verified buyers. This is measured for period of last 8 weeks.",
        "type": "POSITIVE_SELLER_RATING",
        "formatted_target": "≥ 85%",
        "target": "85.0",
        "target_format": "GREATER_THAN_PERCENTAGE",
        "target_respected": "true"
      }
    ],
    "seller_id": "42",
    "main_category_id": "12356"
  },
  "success": "true",
  "error_code": "REQUEST_CANNOT_BE_NULL",
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
