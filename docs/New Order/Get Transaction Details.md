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

<Highlight color="#00A854">POST</Highlight> <Highlight1 color="#EEEEEE">/finance/transaction/accountTransactions/query</Highlight1>

Query Account Transactions

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

| Name                   | Type   | Required                      | Demo Value | Rule                                                    | Description                                                                                                                                               |
| :--------------------- | :----- | :---------------------------- | :--------- | :------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| - transaction_type     | String | false                         | Deposit    | Enum Values: Deposit,Withdrawal,Payment,null            | transaction type,Enumeration values for(Deposit,Withdrawal,Payment,null)                                                                                  |
| - sub_transaction_type | String | false                         | Deposit    |                                                         | sub transaction type,Enumeration values for(Settlement,Failed Payment,Returned Payment,Auto Withdrawal,Manual Withdrawal,Sponsored Solutions Top-up,null) |
| - transaction_number   | String | false                         | 1001       |                                                         | transaction number                                                                                                                                        |
| - page_size            | Number | <Highlight2>true</Highlight2> | 10         | Default Value: 10 Regular Expression: ^\+?[1-9][0-9]\*$ | page size                                                                                                                                                 |
| - start_time           | String | <Highlight2>true</Highlight2> | 20220601   | Regular Expression: ^\d{4}\d{1,2}\d{1,2}                | start time,format:yyyyMMdd                                                                                                                                |
| - end_time             | String | <Highlight2>true</Highlight2> | 20220602   | Regular Expression: ^\d{4}\d{1,2}\d{1,2}                | start time,format:yyyyMMdd                                                                                                                                |
| - page_num             | Number | <Highlight2>true</Highlight2> | 1          | Default Value: 1 Regular Expression: ^\+?[1-9][0-9]\*$  | page number                                                                                                                                               |

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

| Name                 | Type     | Demo Value              | Description                               |
| :------------------- | :------- | :---------------------- | :---------------------------------------- |
| msg                  | String   | null                    | error message                             |
| data                 | Object   | {""}                    | result                                    |
| -page_info           | Object   | {""}                    | page Info                                 |
| -page_num            | Number   | 1                       | pageNum                                   |
| --page_size          | Number   | 10                      | pageSize                                  |
| --total_page         | Number   | 100                     | totalPage                                 |
| --total_count        | Number   | 1000                    | totalCount                                |
| -transactions        | Object[] | []                      | transactions                              |
| --transaction_number | String   | 10000001                | trading serial number                     |
| --transaction_time   | String   | 2022-01-01 00:00:00     | trading occurred time                     |
| --type               | String   | Penarikan Dana          | trading type                              |
| --sub_type           | String   | Penarikan Dana Otomatis | trading sub type                          |
| --payee_account      | Object   | {""}                    | payee Account                             |
| ---account           | String   | 1001                    | payee Account                             |
| ---description       | String   | description             | description                               |
| --amount             | String   | ±0.01                   | amount                                    |
| --currency           | String   | IDR                     | currency                                  |
| --remarks            | String   | remarks                 | remarks                                   |
| --tracking_list      | Object[] | []                      | tracking list                             |
| ---name              | String   | WITHDRAWAL_INITIATED    | The name of the state                     |
| ---status            | String   | Penarikan Dana Dibuat   | Configuration of multilingual copywriting |
| ---update_time       | String   | 2022-01-01 00:00:00     | Update time                               |
| ---remark            | String   | remark                  | remark                                    |
| success              | Boolean  | true                    | success:true,fail:false                   |
| error_code           | String   | error_code              | error code                                |

### Response Example

---

```
{
  "msg": "null",
  "code": "0",
  "data": {
    "page_info": {
      "total_count": "1000",
      "total_page": "100",
      "page_num": "1",
      "page_size": "10"
    },
    "transactions": [
      {
        "payee_account": {
          "description": "description",
          "account": "1001"
        },
        "amount": "±0.01",
        "sub_type": "Penarikan Dana Otomatis",
        "transaction_number": "10000001",
        "transaction_time": "2022-01-01 00:00:00",
        "currency": "IDR",
        "tracking_list": [
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          },
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          }
        ],
        "type": "Penarikan Dana",
        "remarks": " remarks"
      },
      {
        "payee_account": {
          "description": "description",
          "account": "1001"
        },
        "amount": "±0.01",
        "sub_type": "Penarikan Dana Otomatis",
        "transaction_number": "10000001",
        "transaction_time": "2022-01-01 00:00:00",
        "currency": "IDR",
        "tracking_list": [
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          },
          {
            "update_time": "2022-01-01 00:00:00",
            "name": "WITHDRAWAL_INITIATED",
            "remark": "remark",
            "status": "Penarikan Dana Dibuat"
          }
        ],
        "type": "Penarikan Dana",
        "remarks": " remarks"
      }
    ]
  },
  "success": "true",
  "error_code": " error_code",
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
