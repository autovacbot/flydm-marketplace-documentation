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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/promotion/voucher/get</Highlight1>

get a seller voucher promotion detail

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
| voucher_type  | String   | <Highlight2>true</Highlight2>	| COLLECTIBLE_VOUCHER  |          | voucher type COLLECTIBLE_VOUCHER \ CODE_VOUCHER|
| id            | Number   | <Highlight2>true</Highlight2>	   | 91471121134707    |          | promotion ID|


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
| data                                  | Object     | response body                            | response body   |
| -criteria_over_money                  |String	     | 100                                      | Discount details, if order value reaches set value, will money discount or percentage discount|
| -apply                                |String	     | SPECIFIC_PRODUCTS                        | apply scope: ENTIRE_SHOP \ SPECIFIC_PRODUCTS |
| -voucher_type                         | String	   | COLLECTIBLE_VOUCHER                      | Voucher type, COLLECTIBLE_VOUCHER \ CODE_VOUCHER|
| -collect_start                        | Number	   | 1626969600000                            | The time that customers can collect the voucher|
| -display_area                         | String	   | REGULAR_CHANNEL                          | The area that customers can see the voucher\ REGULAR_CHANNEL\STORE_FOLLOWER\OFFLINE\LIVE_STREAM\SHARE_VOUCHER\CEM_SELLER|
| -period_end_time                      | Number	   | 1630339199000                            | The period end time that customers can use the voucher|
| -voucher_name                         | String	   | test voucher                             | Voucher name|
| -voucher_discount_type                | String	   | MONEY_VALUE_OFF                          | Discount type|
| -offering_money_value_off             | String	   | 1                                        | Discount details, if order value reaches criteria_over_money value, will discount money value|
| -period_start_time                    | Number	   | 1626969600000                            | The period start time that customers can use the voucher|
| -limit                                | Number	   | 1                                        | Voucher limit per customer|
| -order_used_budget                    | String	   | null                                     | Already used total|
| -currency                             | String	   | SGD                                      | Currency|
| -id                                   | Number	   | 91471121126083                           | Promotion ID|
| -issued                               | Number	   | 5                                        | Revision should be greater than the current setting|
| -max_discount_offering_money_value    | String	   | null                                     | Discount details, if order value reaches criteria_over_money value, allow maximum discount per order, just support percentage discount off type|
| -voucher_code                         | String	   | null                                     | Voucher code|
| -offering_percentage_discount_off     | String	   | null                                     | Discount details, if order value reaches criteria_over_money value, will percentage discount off value|
| -status                               | String	   | SUSPEND                                  | Promotin status, NOT_START \ ONGOING \ SUSPEND \ FINISH|
| success                               | Boolean    | true                                     | true/false |
| error_code                            | String	   | null                                     | error code |
| error_msg                             | String	   | null                                     | error message|

### Response Example
---
```
{
  "error_msg": "null",
  "code": "0",
  "data": {
    "period_end_time": "1630339199000",
    "max_discount_offering_money_value": "null",
    "criteria_over_money": "100",
    "apply": "SPECIFIC_PRODUCTS",
    "voucher_name": "test voucher",
    "voucher_code": "null",
    "offering_money_value_off": "1",
    "order_used_budget": "null",
    "offering_percentage_discount_off": "null",
    "period_start_time": "1626969600000",
    "display_area": "REGULAR_CHANNEL",
    "voucher_type": "COLLECTIBLE_VOUCHER",
    "limit": "1",
    "collect_start": "1626969600000",
    "voucher_discount_type": "MONEY_VALUE_OFF",
    "currency": "SGD",
    "id": "91471121126083",
    "issued": "5",
    "status": "SUSPEND"
  },
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
