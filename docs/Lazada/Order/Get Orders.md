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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/orders/get</Highlight1>

Use this API to get the list of items for a range of orders1..

### Common Parameters

---
#### Common Request Parameters

| Name      | Type   | Required                      | Description                         |
| :-------- | :----- | :---------------------------- | :---------------------------------- |
| seller_id | String | <Highlight2>true</Highlight2> | Seller store id                     |
| country   | String | <Highlight2>true</Highlight2> | Seller country, Ex: MY,SG,ID,TH,etc |

### Request Parameters

---

| Name             | Type   | Required | Demo Value                | Rule                                   | Description                                                                                                                                                                                                                                                                                   |
| :--------------- | :----- | :------- | :------------------------ | :------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - update_before  | String | false    | 2018-02-10T16:00:00+08:00 |                                        | Limits the returned orders to those updated before or on the specified date, given in ISO 8601 date format. Optional.                                                                                                                                                                         |
| - sort_direction | String | false    | DESC                      |                                        | Specify the sorting type. Possible values are ASC and DESC.                                                                                                                                                                                                                                   |
| - offset         | Number | false    | 0                         | i.Default Value: ii.0 Max Length: 4500 | Number of orders to skip at the beginning of the list.                                                                                                                                                                                                                                        |
| - limit          | Number | false    | 10                        |                                        | The maximum number of orders that can be returned. The supported maximum number is 100.                                                                                                                                                                                                       |
| - update_after   | String | false    | 2017-02-10T09:00:00+08:00 |                                        | Limits the returned orders to those updated after or on the specified date, given in ISO 8601 date format. Either UpdatedAfter or CreatedAfter is mandatory.                                                                                                                                  |
| - sort_by        | String | false    | updated_at                |                                        | Allows to choose the sorting column. Possible values are created_at and updated_at.                                                                                                                                                                                                           |
| - created_before | String | false    | 2018-02-10T16:00:00+08:00 |                                        | Limits the returned orders to those updated before or on the specified date, given in ISO 8601 date format. Optional.                                                                                                                                                                         |
| - created_after  | String | false    | 2017-02-10T09:00:00+08:00 |                                        | Limits the returned orders to those updated after or on the specified date, given in ISO 8601 date format. Either UpdatedAfter or CreatedAfter is mandatory.                                                                                                                                  |
| - status         | String | false    | shipped                   |                                        | When set, limits the returned set of orders to loose orders, which return only entries which fit the status provided. Possible values are unpaid, pending, canceled, ready_to_ship, delivered, returned, shipped and failed. New Possible values are topack and toship for white list seller. |

### Common Response Parameters

---

| Name       | Type     | Description                                                                                                                                                            |
| :--------- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type       | String   | Error type. Optional values ​​are ISP (service provider error), ISV (developer error), SYSTEM (platform system error)                                                  |
| code       | String   | Error code. For example: ServiceUnavailable                                                                                                                            |
| message    | String   | Description of error details                                                                                                                                           |
| request_id | String   | Request a unique identifier                                                                                                                                            |
| detail     | Object[] | If the API call is for batch processing, when the call fails (all or part of the request failure), the response contains the error details. See the following example: |

> ```
> {
>  "detail": [
>    {
>      "field": "Product",
>      "seller_sku": "api-create-test-1",
>      "message": "SELLER_SKU_INVALID"
>    },
>    {
>      "field": "Product2",
>      "message": "SELLER_SKU_INVALID"
>    }
>  ]
> }
> ```

### Response Parameters

---

| Name                                                                                                                                     | Type     | Demo Value                 | Description                                                                                                                                                    |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :------- | :------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data                                                                                                                                     | Object   | {}                         | Responsebody body                                                                                                                                              |
| -countTotal                                                                                                                              | Number   | 500                        | Displayed in the Head section, this number tells the complete number of all orders for the current filter set in the database.                                 |
| -count                                                                                                                                   | Number   | 10                         | Displayed in the Head section, this number tells the complete number of all orders for the current filter set in the database(included offset and limit).      |
| -orders                                                                                                                                  | Object[] | []                         | Order details                                                                                                                                                  |
| --branch_number                                                                                                                          | String   | 2222                       | (For Thailand only) The tax branch code for corporate customers, provided by the customer when placing the order.                                              |
| --tax_code                                                                                                                               | String   | 562562                     | (For Thailand and Vietnam only) The customer's VAT tax code, provided by the customer when placing the order.                                                  |
| --extra_attributes                                                                                                                       | String   | null                       | Extra attributes which were passed to the Seller Center on getMarketPlaceOrders call.                                                                          |
| --address_updated_at                                                                                                                     | String   | null                       | Address updated at                                                                                                                                             |
| --shipping_fee                                                                                                                           | String   | 0.54                       | Total shipping fee for this order.                                                                                                                             |
| --customer_first_name [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)          | String   | Ha Hung                    | Customer first name                                                                                                                                            |
| --payment_method                                                                                                                         | String   | COD                        | The method of the payment. For details, see Payment method options.                                                                                            |
| --statuses                                                                                                                               | String[] | unpaid,pending,shipped     | An array of unique status of the items in the order. You can find all of the different status codes in the response example.                                   |
| --remarks                                                                                                                                | String   | remarks                    | Remarks                                                                                                                                                        |
| --order_number                                                                                                                           | String   | 303147148                  | The human-readable order number.                                                                                                                               |
| --order_id                                                                                                                               | String   | 1895464                    | Identifier of this order as assigned by the Seller Center.                                                                                                     |
| --voucher                                                                                                                                | String   | 0.00                       | Total voucher for this order.                                                                                                                                  |
| --national_registration_number [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297) | String   | 1                          | National registration number. Required in some countries.                                                                                                      |
| --promised_shipping_times                                                                                                                | String   | shipping_time              | Target shipping time for the soonest order item if they are available.                                                                                         |
| --items_count                                                                                                                            | Number   | 2                          | Number of items in order.                                                                                                                                      |
| --voucher_platform                                                                                                                       | String   | 0.00                       | The voucher that is issued by Lazada                                                                                                                           |
| --voucher_seller                                                                                                                         | String   | 0.00                       | The voucher that is issued by the seller                                                                                                                       |
| --created_at                                                                                                                             | String   | 2018-02-09T22:44:30+08:00  | Date and time when the order was placed.                                                                                                                       |
| --price                                                                                                                                  | String   | 106.00                     | Total amount for this order.                                                                                                                                   |
| --address_billing                                                                                                                        | Object   | {}                         | Node that contains additional nodes, which makes up the billing address: FirstName, LastName, Phone, Phone2, Address1, Address2, City, PostCode, and Country.  |
| ---address1 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | 1 CHANGI VILLAGE ROAD, 11  | Detailed address                                                                                                                                               |
| ---phone2 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                      | String   | 61\*\*\*\*7                | Backup phone number                                                                                                                                            |
| ---first_name                                                                                                                            | String   | Ha Hung                    | Customer first name                                                                                                                                            |
| ---phone [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                       | String   | 61\*\*\*\*7                | Phone number                                                                                                                                                   |
| ---address5 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address5                   | Third-level address                                                                                                                                            |
| ---post_code                                                                                                                             | String   | 500001                     | Post code; Note: This value will not be used in Lazada ID                                                                                                      |
| ---address4 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address4                   | City name                                                                                                                                                      |
| ---last_name [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                   | String   | last_name                  | Customer last name                                                                                                                                             |
| ---country                                                                                                                               | String   | Singapore                  | Country                                                                                                                                                        |
| ---address3 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address3                   | State name                                                                                                                                                     |
| ---address2 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address2                   | Not used for now                                                                                                                                               |
| ---city                                                                                                                                  | String   | Singapore-Singapore-500001 | City name                                                                                                                                                      |
| --warehouse_code                                                                                                                         | String   | dropshipping               | Warehouse Code of multi-wh sellers                                                                                                                             |
| --shipping_fee_original                                                                                                                  | String   | 0.00                       | the original shipping fee which are supposed to be charged to the customer, before any type of shipping fee promotion                                          |
| --shipping_fee_discount_seller                                                                                                           | String   | 0.00                       | shipping fee discount from seller                                                                                                                              |
| --shipping_fee_discount_platform                                                                                                         | String   | 0.00                       | shipping fee discount from platform                                                                                                                            |
| --address_shipping                                                                                                                       | Object   | {}                         | Node that contains additional nodes, which makes up the shipping address: FirstName, LastName, Phone, Phone2, Address1, Address2, City, PostCode, and Country. |
| ---address1 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | 1 CHANGI VILLAGE ROAD, 11  | Detailed address                                                                                                                                               |
| ---phone2 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                      | String   | 61\*\*\*\*7                | Backup phone number                                                                                                                                            |
| ---first_name                                                                                                                            | String   | Ha Hung                    | Customer first name                                                                                                                                            |
| ---phone [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                       | String   | 61\*\*\*\*7                | Phone number                                                                                                                                                   |
| ---address5 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address5                   | Third-level address                                                                                                                                            |
| ---post_code                                                                                                                             | String   | 500001                     | Post code; Note: This value will not be used in Lazada ID                                                                                                      |
| ---address4 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address4                   | City name                                                                                                                                                      |
| ---last_name [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                   | String   | last_name                  | Customer last name                                                                                                                                             |
| ---country                                                                                                                               | String   | Singapore                  | Country                                                                                                                                                        |
| ---address3 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address3                   | State name                                                                                                                                                     |
| ---address2 [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)                    | String   | address2                   | Not used for now                                                                                                                                               |
| ---city                                                                                                                                  | String   | Singapore-Singapore-500001 | City name                                                                                                                                                      |
| --customer_last_name [C](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4s5pgkx#?nodeId=10784&docId=108297)           | String   | last_name                  | Empty for now. See cutomer_first_name.                                                                                                                         |
| --gift_option                                                                                                                            | String   | false                      | 1 if item is a gift, and 0 if it is not.                                                                                                                       |
| --voucher_code                                                                                                                           | String   | 1234                       | Voucher code                                                                                                                                                   |
| --updated_at                                                                                                                             | String   | 2018-02-09T22:44:30+08:00  | Date and time of the last change to the order.                                                                                                                 |
| --delivery_info                                                                                                                          | String   | delivery                   | Delivery information                                                                                                                                           |
| --gift_message                                                                                                                           | String   | 1                          | Gift message as specified by the customer.                                                                                                                     |

### Response Example

---

```
{
  "code": "0",
  "data": {
    "count": "10",
    "countTotal": "500",
    "orders": [
      {
        "voucher_platform": "0.00",
        "voucher": "0.00",
        "warehouse_code": "dropshipping",
        "order_number": "303147148",
        "voucher_seller": "0.00",
        "created_at": "2018-02-09T22:44:30+08:00",
        "voucher_code": "1234",
        "gift_option": "false",
        "shipping_fee_discount_platform": "0.00",
        "customer_last_name": "last_name",
        "promised_shipping_times": "shipping_time",
        "updated_at": "2018-02-09T22:44:30+08:00",
        "price": "106.00",
        "national_registration_number": "1",
        "shipping_fee_original": "0.00",
        "payment_method": "COD",
        "address_updated_at": "null",
        "customer_first_name": "Ha Hung",
        "shipping_fee_discount_seller": "0.00",
        "shipping_fee": "0.54",
        "branch_number": "2222",
        "tax_code": "562562",
        "items_count": "2",
        "delivery_info": "delivery",
        "statuses": [
          "unpaid,pending,shipped",
          "unpaid,pending,shipped"
        ],
        "address_billing": {
          "country": "Singapore",
          "address3": "address3",
          "phone": "61****7",
          "address2": "address2",
          "city": "Singapore-Singapore-500001",
          "address1": "1 CHANGI VILLAGE ROAD, 11",
          "post_code": "500001",
          "phone2": "61****7",
          "last_name": "last_name",
          "address5": "address5",
          "address4": "address4",
          "first_name": "Ha Hung"
        },
        "extra_attributes": "null",
        "order_id": "1895464",
        "remarks": "remarks",
        "gift_message": "1",
        "address_shipping": {
          "country": "Singapore",
          "address3": "address3",
          "phone": "6****67",
          "address2": "address2",
          "city": "Singapore-Singapore-500001",
          "address1": "1 CHANGI VILLAGE ROAD, 11",
          "post_code": "500001",
          "phone2": "4***456",
          "last_name": "last_name",
          "address5": "address5",
          "address4": "address4",
          "first_name": "Ha Hung"
        }
      },
      {
        "voucher_platform": "0.00",
        "voucher": "0.00",
        "warehouse_code": "dropshipping",
        "order_number": "303147148",
        "voucher_seller": "0.00",
        "created_at": "2018-02-09T22:44:30+08:00",
        "voucher_code": "1234",
        "gift_option": "false",
        "shipping_fee_discount_platform": "0.00",
        "customer_last_name": "last_name",
        "promised_shipping_times": "shipping_time",
        "updated_at": "2018-02-09T22:44:30+08:00",
        "price": "106.00",
        "national_registration_number": "1",
        "shipping_fee_original": "0.00",
        "payment_method": "COD",
        "address_updated_at": "null",
        "customer_first_name": "Ha Hung",
        "shipping_fee_discount_seller": "0.00",
        "shipping_fee": "0.54",
        "branch_number": "2222",
        "tax_code": "562562",
        "items_count": "2",
        "delivery_info": "delivery",
        "statuses": [
          "unpaid,pending,shipped",
          "unpaid,pending,shipped"
        ],
        "address_billing": {
          "country": "Singapore",
          "address3": "address3",
          "phone": "61****7",
          "address2": "address2",
          "city": "Singapore-Singapore-500001",
          "address1": "1 CHANGI VILLAGE ROAD, 11",
          "post_code": "500001",
          "phone2": "61****7",
          "last_name": "last_name",
          "address5": "address5",
          "address4": "address4",
          "first_name": "Ha Hung"
        },
        "extra_attributes": "null",
        "order_id": "1895464",
        "remarks": "remarks",
        "gift_message": "1",
        "address_shipping": {
          "country": "Singapore",
          "address3": "address3",
          "phone": "6****67",
          "address2": "address2",
          "city": "Singapore-Singapore-500001",
          "address1": "1 CHANGI VILLAGE ROAD, 11",
          "post_code": "500001",
          "phone2": "4***456",
          "last_name": "last_name",
          "address5": "address5",
          "address4": "address4",
          "first_name": "Ha Hung"
        }
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

| Error Code | Error Message                  | Description                                     |
| :--------- | :----------------------------- | :---------------------------------------------- |
| 14         | E014: "%s" Invalid Offset      | The specified order ID is not valid.            |
| 17         | E017: "%s" Invalid Date Format | The date format is not valid.                   |
| 19         | E019: "%s" Invalid Limit       | The value for the limit parameter is not valid. |
| 36         | E036: Invalid status filter    | The specified status filter is not valid.       |
| 74         | E074: Invalid sort direction.  | The specified sort direction is not valid.      |
| 75         | E075: Invalid sort filter.     | The specified sort filter is not valid.         |
