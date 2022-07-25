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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/review/seller/reply/add</Highlight1>

submit seller reply for customers review

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
| - id          | Number   | <Highlight2>true</Highlight2>	| 11111111111  |        | review id that user wants to reply to. Can be obtain from GetProductReviewList |
| - content     | String   | <Highlight2>true</Highlight2>	| thank you for your reply |        | reply content in text, only support reply in text.max length = 500 |

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
| data                                  | Boolean    | true                                     | reply success or fail   |
| success                               | Boolean    | true                                     | reply success or fail |
| error_code                            | String	 | error                                    | error code |
| error_msg                             | String	 | error                                    | error msg|


### Response Example
---
```
{
  "error_msg": "error",
  "code": "0",
  "data": "true",
  "success": "true",
  "error_code": "error",
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
| Error Code            | 	Error Message         | Description        |
| :---                  | :---                    | :---               |
| PARAMS_VALIDATE_ERROR	| NULL_SELLERID 	      | Cannot recognize sellerid| 
| PARAMS_VALIDATE_ERROR	| NULL_ID	              | Cannot recognize id| 
| PARAMS_VALIDATE_ERROR	| NULL_CONTENT	          | Empty content| 
| PARAMS_VALIDATE_ERROR	| REPLY_ALREADY	          | Already replied. All reply needs go through quality control process.| 
| PARAMS_VALIDATE_ERROR	| NO_SUCH_REVIEW	      | No such review| 
| PARAMS_VALIDATE_ERROR	| REVIEW_STATUS_CANNOT_REPLY	| Review status cannot be replied to, review's status may be changed because of being edited or reported| 
| PARAMS_VALIDATE_ERROR	| REVIEW_TYPE_DONOT_SUPPORT_REPLY	| Review type cannot be replied to, only reply to PRODUCT_REVIEW| 
| PARAMS_VALIDATE_ERROR	| REVIEW_INFO_DONOT_SUPPORT_REPLY	| Review info cannot be replied to, review must have text content or images or video| 
| PARAMS_VALIDATE_ERROR	| REVIEW_REPORTED_CANNOT_REPLY	    | Review been reported cannot be repied to| 
| PARAMS_VALIDATE_ERROR	| REPLY_CONTENT_TOO_LONG	        | Reply too long| 
| PARAMS_VALIDATE_ERROR	| BEYOND_REPLY_PERIOD	            | Reply over due| 
| TRAFFIC_CONTROL	    | TRAFFIC_CONTROL	                | Traffic control| 