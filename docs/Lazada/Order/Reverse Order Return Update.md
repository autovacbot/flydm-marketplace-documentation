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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/reverse/return/update</Highlight1>

Seller can use this API to action on return and refund related.

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
| action        | String   | <Highlight2>true</Highlight2>  | instantRefund | instantRefund;agreeReturn;refuseReturn;agreeRefund;refuseRefund;confirmDelivery |
| reverse_order_id | Number | <Highlight2>true</Highlight2> | 0 | reverse order id | 
| reverse_order_item_ids | Number[] | <Highlight2>true</Highlight2> | [] | reverse order item id list |
| reason_id     | Number   | false | 0 | reason id | 
| comment       | String   | false | comment | comment | 
| image_info    | Object[] | false | [] | image_info |
| -name         | String   | false | name | image name
| -url          | String   | false | url | image url

### Common Response Parameters 
---

| Name        | Type        | Description        |
| :---        | :---        | :---                |
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
| data                                  | Object     | {}                                       | data |
| -reverse_order_line                   | Object[]   | []                                       | reverse order line |
| --reverse_order_line_id               | Number     | 0                                        | reverse order line id |
| --reason_source                       | String     | reason_source                            | reason source |
| --reason_type                         | String     | reason_type                              | reason type |
| --reason_id                           | Number     | 0                                        | reason id |
| --reason_name                         | String     | out of stock                             | reason name |
| --reason_desc                         | String     | stock is 0                               | reason desc |
| --refund_amount                       | Number     | 0                                        | refund amount |
| --is_cancel                           | Boolean	 | true                                     | cancel or not|
| --order_id                            | Number     | 0                                        | order id |
| --seller_sku                          | String     | 0                                        | seller sku |
| --paid_price                          | Number     | 0                                        | paid price |
| --apply_reason                        | String     | out of stock                             | apply reason |
| --order_line_id                       | Number     | 0                                        | order line id |
| -reverse_order_id                     | Number     | 0                                        | reverse orde id |
| -reason_info                          | Object[]   | []                                       | reason info |
| --reason_id                           | Number     | 0                                        | reason id |
| --reason_name                         | String     | out of stock                             | reason name |
| -total_refund                         | String     | 0                                        | total refund amount |


### Response Example
---
```
{
  "code": "0",
  "data": {
    "reason_info": [
      {
        "reason_name": "out of stock",
        "reason_id": "0"
      },
      {
        "reason_name": "out of stock",
        "reason_id": "0"
      }
    ],
    "reverse_order_id": "0",
    "total_refund": "0",
    "reverse_order_line": [
      {
        "paid_price": "0",
        "is_cancel": "true",
        "reason_id": "0",
        "reason_source": "reason_source",
        "reason_desc": "stock is 0",
        "apply_reason": "out of stock",
        "reason_type": "reason_type",
        "seller_sku": "0",
        "refund_amount": "0",
        "order_line_id": "0",
        "reason_name": "out of stock",
        "order_id": "0",
        "reverse_order_line_id": "0"
      },
      {
        "paid_price": "0",
        "is_cancel": "true",
        "reason_id": "0",
        "reason_source": "reason_source",
        "reason_desc": "stock is 0",
        "apply_reason": "out of stock",
        "reason_type": "reason_type",
        "seller_sku": "0",
        "refund_amount": "0",
        "order_line_id": "0",
        "reason_name": "out of stock",
        "order_id": "0",
        "reverse_order_line_id": "0"
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
| Error Code            | 	Error Message                               | Description        |
| :---                  | :---                                          | :---               |
| 100	                | E0100: reverse order list is empty	        | E0100: reverse order list is empty |
| 106	                | E0106: ROC internal error	                    | E0106: ROC internal error |
| 107	                | E0107: invalid action	                        | E0107: invalid action |
| 108	                | E0108: reason can't be empty if you want to refuse return or refund	| E0108: reason can't be empty if you want to refuse return or refund |
| 109	                | E0109: comment can't be empty if you want to refuse return or refund	| E0109: comment can't be empty if you want to refuse return or refund |
| 110	                | E0110: image can't be empty if you want to refuse refund	| E0110: image can't be empty if you want to refuse refund |
| 111	                | E0111: do not support massive reverse order line operation if you want to refuse return or refund	| E0111: do not support massive reverse order line operation if you want to refuse return or refund |
| 112	                | E0112: no reverse order found	                | E0112: no reverse order found |
| 113	                | E0113: reverse order line have unknown status	| E0113: reverse order line have unknown status |
| 114	                | E0114: this reverse does not support this action	| E0114: this reverse does not support this action |
| 116	                | E0116: no seller id	                        | E0116: no seller id |
| 117	                | E0117: no user id	                            | E0117: no user id |
| 118	                | E0118: no user email	                        | E0118: no user email |
| 125	                | E0125: invalid reverse id	                    | E0125: invalid reverse id |
| 126	                | E0126: invalid reverse order lines	        | E0126: invalid reverse order lines |
| 127	                | E0127: invalid seller id for this reverse order line	| E0127: invalid seller id for this reverse order line |  