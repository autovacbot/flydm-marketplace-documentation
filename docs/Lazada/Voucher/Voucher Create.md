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

<Highlight color="#00A854">POST</Highlight>  <Highlight1 color="#EEEEEE">/promotion/voucher/create</Highlight1>

create a new seller voucher promotion

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
| criteria_over_money      | String    | <Highlight2>true</Highlight2>  | 100   |          | Discount details, if order value reaches set value, will money discount or percentage discount|
| voucher_type             | String   | <Highlight2>true</Highlight2>	| COLLECTIBLE_VOUCHER |      |  Voucher type, just set COLLECTIBLE_VOUCHER|
| apply                    | String    | <Highlight2>true</Highlight2>  | SPECIFIC_PRODUCTS   |          | apply scope: ENTIRE_SHOP \ SPECIFIC_PRODUCTS|
| collect_start            | Number   | false  | 1625649720000   |          | The time that customers can collect the voucher|
| display_area             | String    | <Highlight2>true</Highlight2>  | REGULAR_CHANNEL   |          | The area that customers can see the voucher. REGULAR_CHANNEL\STORE_FOLLOWER\OFFLINE\LIVE_STREAM\SHARE_VOUCHER\CEM_SELLER|
| period_end_time          | Number    | <Highlight2>true</Highlight2>  | 1630339199000   |          | The period end time that customers can use the voucher|
| voucher_name             | String    | <Highlight2>true</Highlight2>  | test voucher   |          | Voucher name|
| voucher_discount_type    | String    | <Highlight2>true</Highlight2>  | MONEY_VALUE_OFF   |          | Discount type, MONEY_VALUE_OFF | PERCENTAGE_DISCOUNT_OFF |
| offering_money_value_off | String    | false  | 1   |          | Discount details, if order value reaches criteria_over_money value, will discount money value|
| period_start_time       | Number    | <Highlight2>true</Highlight2>  | 1626969600000   |          | The period start time that customers can use the voucher|
| limit      | Number     | <Highlight2>true</Highlight2>  | 1   |          | 	
Voucher limit per customer|
| issued      | Number    | <Highlight2>true</Highlight2>  | 5   |          | Revision should be greater than the current setting|
| max_discount_offering_money_value      | String    | false  | 50   |          | Discount details, if order value reaches criteria_over_money value, allow maximum discount per order, just support percentage discount off type|
| offering_percentage_discount_off       | Number    | false  | 1   |          | Discount details, if order value reaches criteria_over_money value, will percentage discount off value|

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
| data                                  | Number	 | 9616200353530                            | promotion ID|
| success                               | Boolean	 | true                                     | true \ false| 
| error_code                            | Number	 | null                                     | error code
| error_msg                             | String	 | null                                     | error message| 

### Response Example
---
```
{
  "error_msg": "null",
  "code": "0",
  "data": "9616200353530",
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
| 23	                | E023: xxxx	                | business validation error| 
| 21	                | E023: Internal System Error	| Internal System Error| 
| 24	                | E024: Parameter illegal	    | Parameter illegal| 
| 25	                | E025: UMP Exception	        | UMP Exception| 
| 26	                | E026: Seller Unauthorized	    | Seller Unauthorized| 
