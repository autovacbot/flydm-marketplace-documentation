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

<Highlight color="#00A854">GET</Highlight>  <Highlight1 color="#EEEEEE">/order/rts</Highlight1>

Use this API to mark an order item as being ready to ship.

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
| - delivery_type  | String   | <Highlight2>true</Highlight2>   | dropship | | One of the following delivery types: 'dropship' - the seller will send out the package on his own. Now only "dropship" is supported.    |
| - order_item_ids | String   | <Highlight2>true</Highlight2> | [1832590,1832592] |  | List of oder items to be marked ready to ship. Comma separated list in square brackets. Mandatory.   |
| - shipment_provider | String   | <Highlight2>true</Highlight2> | Aramax |  | Valid shipment provider as looked up via GetShipmentProviders. Mandatory for drop-shipping.   |
| - tracking_number | String   | <Highlight2>true</Highlight2> | 12345678 |  | Package tracking number. Mandatory in the case of drop-shipping.   |

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
| :---                                  | :---       | :---                                     | :---             |
| data                                  | Object     | {}                                       | Response body    |
| -order_items                          | Object[]   | []                                       | order items array          |
| --order_item_id                       | Number     | 123456                                   | order item id  |
| --purchase_order_id                   | Number     | 456789                                   | Seller Center identification.  Optional, please ignore it if your business scenario does not cover it.          |
| --purchase_order_number               | String     | ABC-123456                               | Order number in the Seller Center.  Optional, please ignore it if your business scenario does not cover it.  |

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
| 23                | E023: "%s" Invalid Order Item IDs      | The specified order item IDs are not valid. |
| 24                | E024: "%s" Invalid Delivery Type      | The specified delivery type is not valid. |
| 25                | E025: "%s" Invalid Shipping Provider      | The specified shipping provider is not valid. |
| 26	            | E026: "%s" Invalid Tracking Number	|The specified tracking number is not valid.|
| 29	            | E029: Order items must be from the same order	|The specified order items must be from the same order.
| 31	            | E031: Tracking ID incorrect. Example tracking ID: "%s"	|The specified tracking ID is not correct.
| 63	            | E063: The tracking code %s has already been used	|The specified tracking code has been used.
| 73	            | E073: All order items must have status Pending or Ready To Ship. (%s)	|The status of order items is not valid.
| 82	            | E082: All order items must have status Pending.	|The status of order items is not valid.
| 91	            | E091: You are not allowed to set the shipment provider and tracking number and the delivery type is wrong. Please use sent_to_warehous	|Error occurred due to permission issue.|
| 94	            | E094: Serial numbers specified incorrectly	|Serial numbers were not specified according to one of the accepted formats for the SerialNumber parameter.|
| 95	            | E095: Invalid serial number format (%s)	|Serial numbers must be 1 to 26 characters; only latin letters and digits are allowed.|
| 96	            | E096: Duplicate serial number among order items (%s)	|Two or more items in the order would share a serial number.|


