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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/sof/delivered</Highlight1>

Use this API to cancel a single order item.

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
| - order_item_ids | String   | <Highlight2>true</Highlight2>   | [1832590,1832592] | | List of oder items to be marked delivered. Comma separated list in square brackets. Mandatory. |

### Common Response Parameters 
---

| Name        | Type        | Description        |
| :---         | :---         | :---                |
| type        | String      | Error type. Optional values ​​are ISP (service provider error), ISV (developer error), SYSTEM (platform system error)               |
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
| data                                  | Object     | {}                                       | Response body   |
| -order_items                          | Object[]   | []                                       | order items array   |
| --order_item_id                       | Number     | 123456                                   | order item id   |
| --purchase_order_id                   | Number     | 456789                                   | Seller Center identification.  Optional, please ignore it if your business scenario does not cover it.   |
| --purchase_order_number               | String     | ABC-123456                               | Order number in the Seller Center.  Optional, please ignore it if your business scenario does not cover it.   |


### Response Example
---
```
{
  "code": "0",
  "data": {
    "order_items": [
      {
        "order_item_id": "123456",
        "purchase_order_id": "456789",
        "purchase_order_number": "ABC-123456"
      },
      {
        "order_item_id": "123456",
        "purchase_order_id": "456789",
        "purchase_order_number": "ABC-123456"
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
| Error Code        | 	Error Message                   | Description        |
| :---              | :---                              | :---               |
| 20                | E020: "%s" Invalid Order Item ID  | The specified order item ID is not valid. |
| 21                | E021: OMS Api Error Occurred      | Internal system error. |
| 23	              | E023: "%s" Invalid Order Item IDs	| The specified order item IDs are not valid. |
| 29	              | E029: Order items must be from the same order	| The specified order items must be from the same order. |
| 1007	            | E1007: %s not SOF Order Item ID	  | The specified order items must be SOF Order Item ID |
| 1008	            | E1008: %s order item status is not ready_to_ship	| The specified order items must have status Ready To Ship |

