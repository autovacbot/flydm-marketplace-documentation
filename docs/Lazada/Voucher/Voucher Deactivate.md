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

<Highlight color="#00A854">POST</Highlight>  <Highlight1 color="#EEEEEE">/promotion/voucher/deactivate</Highlight1>

deactivate seller voucher promotion

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

| Name          | Type     | Required  | Demo Value  | Rule     | Description   |
| :---          | :---     | :---      | :---        | :---     | :---          |
| voucher_type  | String   | <Highlight2>true</Highlight2>  | COLLECTIBLE_VOUCHER   |          | voucher type COLLECTIBLE_VOUCHER \ CODE_VOUCHER|
| id            | Number   | <Highlight2>true</Highlight2>	| 91471121134707        |          |  Promotion ID|


### Common Response Parameters 
---

| Name        | Type        | Description        |
| :---         | :---         | :---                |
| type        | String      | Error type. Optional values ​​are ISP (service provider error), ISV (developer error), SYSTEM (platform system error) |
| code        | String      | Error code. For example: ServiceUnavailable                |
| message     | String      | Description of error details                |
| request_id  | String      | Request a unique identifier               |
| detail      | Object[]    | If the API call is for batch processing, when the call fails (all or part of the request failure), the response contains the error details. See the following example: |
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
| Name                                  | Type       | Demo Value                               | Description     |
| :---                                  | :---       | :---                                     | :---            |
| success                               | Boolean	 | true                                     | true \ false| 
| error_code                            | Number	 | null                                     | error code
| error_msg                             | String	 | null                                     | error message| 

### Response Example
---
```
{
  "error_msg": "null",
  "code": "0",
  "success": "true",
  "error_code": "null",
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
| Error Code            | 	Error Message               | Description        |
| :---                  | :---                          | :---               |
| 	| Query result is empty. 	      | |  
