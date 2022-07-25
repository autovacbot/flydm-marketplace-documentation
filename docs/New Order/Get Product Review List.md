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

<Highlight color="#00A854">GET</Highlight> <Highlight1 color="#EEEEEE">/review/seller/list</Highlight1>

get the review list for one seller

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

| Name             | Type   | Required                      | Demo Value                       | Rule | Description                                                                                                                                                   |
| :--------------- | :----- | :---------------------------- | :------------------------------- | :--- | :------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| - content_filter | String | false                         | WITH_CONTENT,WITH_IMAGE_OR_VIDEO |      | Filter value: WITH_IMAGE_OR_VIEDO (reviews that contains image or video) WITH_CONTENT (reviews that is not empty) Leave the field empty if no need to filter. |
| - status_filter  | String | false                         | NOT_REPLIED                      |      | Filter value: NOT_REPLIED (reviews that seller has not replied yet) Leave the field empty if no need to filter.                                               |
| - page_size      | Number | false                         | 10                               |      | The max review number returned per page. Default 10, max 50                                                                                                   |
| - current        | Number | false                         | 1                                |      | The current page, default value:1                                                                                                                             |
| - item_id        | Number | <Highlight2>true</Highlight2> | 111111111                        |      | Product Item ID                                                                                                                                               |
| - order_id       | Number | false                         | 2222222                          |      | Order ID                                                                                                                                                      |
| - start_time     | Number | false                         | 1621872000000                    |      | Start Time. The timestamp when product reviews are created after order delivered.                                                                             |
| - end_time       | Number | false                         | 1622044800000                    |      | End Time. The timestamp when product reviews are created after order delivered.                                                                               |

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

| Name                | Type     | Demo Value             | Description                                                                                    |
| :------------------ | :------- | :--------------------- | :--------------------------------------------------------------------------------------------- | --------------------- |
| data                | Object   | {}                     | response data                                                                                  |
| -data               | Object[] | []                     | review data list                                                                               |
| --order_id          | Number   | 1111111111             | Order ID                                                                                       |
| --item_id           | Number   | 2222222222             | Product Item ID                                                                                |
| --reviews           | Object[] | []                     | review info                                                                                    |
| ---id               | Number   | 3333333333             | review_id, may used in SubmitSellerReply as id                                                 |
| ---review_type      | String   | PRODUCT_REVIEW         | Value: PRODUCT_REVIEW FOLLOW_UP_REVIEW                                                         |
| ---review_content   | String   | this is a good product | review content in text                                                                         |
| ---review_images    | String[] | []                     | review image url                                                                               |
| ---review_videos    | Object[] | []                     | video list                                                                                     |
| ----video_url       | String   | http\*\*\*\*           | video url                                                                                      |
| ----video_cover_url | String   | http\*\*\*\*           |                                                                                                | video cover image url |
| ---seller_reply     | String   | thank you for your     | review seller reply in text(only support reply in text)                                        |
| ---create_time      | Number   | 1640970071000          | create time of the review in millisecond timestamp(same as start_time and end_time in request) |
| --ratings           | Object   | {}                     | review ratings []                                                                              |
| ---product_rating   | Number   | 5                      | product rating 1-5                                                                             |
| ---seller_rating    | Number   | 4                      | seller rating                                                                                  |
| ---logistics_rating | Number   | 3                      | logistics rating                                                                               |
| -current            | Number   | 1                      | current page no                                                                                |
| -page_size          | Number   | 10                     | page size                                                                                      |
| -total              | Number   | 44                     | total number                                                                                   |
| success             | Boolean  | true                   | success or fail                                                                                |
| error_code          | String   | error                  | error code                                                                                     |
| error_msg           | String   | error                  | error msg                                                                                      |

---

### Response Example

---

```
{
  "error_msg": "error",
  "code": "0",
  "data": {
    "current": "1",
    "total": "44",
    "data": [
      {
        "reviews": [
          {
            "review_images": [
              "[]",
              "[]"
            ],
            "create_time": "1640970071000",
            "review_content": "this is a good product",
            "review_videos": [
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              },
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              }
            ],
            "id": "3333333333",
            "seller_reply": "thank you for your review",
            "review_type": "PRODUCT_REVIEW"
          },
          {
            "review_images": [
              "[]",
              "[]"
            ],
            "create_time": "1640970071000",
            "review_content": "this is a good product",
            "review_videos": [
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              },
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              }
            ],
            "id": "3333333333",
            "seller_reply": "thank you for your review",
            "review_type": "PRODUCT_REVIEW"
          }
        ],
        "item_id": "2222222222",
        "ratings": {
          "seller_rating": "4",
          "product_rating": "5",
          "logistics_rating": "3"
        },
        "order_id": "1111111111"
      },
      {
        "reviews": [
          {
            "review_images": [
              "[]",
              "[]"
            ],
            "create_time": "1640970071000",
            "review_content": "this is a good product",
            "review_videos": [
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              },
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              }
            ],
            "id": "3333333333",
            "seller_reply": "thank you for your review",
            "review_type": "PRODUCT_REVIEW"
          },
          {
            "review_images": [
              "[]",
              "[]"
            ],
            "create_time": "1640970071000",
            "review_content": "this is a good product",
            "review_videos": [
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              },
              {
                "video_url": "http****",
                "video_cover_url": "http****"
              }
            ],
            "id": "3333333333",
            "seller_reply": "thank you for your review",
            "review_type": "PRODUCT_REVIEW"
          }
        ],
        "item_id": "2222222222",
        "ratings": {
          "seller_rating": "4",
          "product_rating": "5",
          "logistics_rating": "3"
        },
        "order_id": "1111111111"
      }
    ],
    "page_size": "10"
  },
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

| Error Code            | Error Message   | Description                     |
| :-------------------- | :-------------- | :------------------------------ |
| PARAMS_VALIDATE_ERROR | NULL_SELLERID   | Cannot recognize sellerid       |
| PARAMS_VALIDATE_ERROR | NULL_ITEMID     | Cannot recognize product itemid |
| TRAFFIC_CONTROL       | TRAFFIC_CONTROL | Traffic control                 |
