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

<Highlight color="#00A854">POST</Highlight>  <Highlight1 color="#EEEEEE">/product/price_quantity/update</Highlight1>

Use this API to update the price and quantity of one or more existing products. The maximum number of products that can be updated is 50, but 20 is recommended.

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
| - payload     | Payload   | <Highlight2>true</Highlight2> | [Preview](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4jzTrKR#?nodeId=10557&docId=108251) |          | [Parameter description](https://open.lazada.com/doc/doc.htm?spm=a2o9m.11193535.0.0.2d4938e4jzTrKR#?nodeId=10557&docId=108251) |


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
| data                                  | Object     | {}                                       | Response body   |



### Response Example
---
```
{
  "code": "0",
  "data": {},
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
| 200	            | E200: Empty SellerSku	            | Empty Item Id and Seller Sku.|
| 5	    | E005: Invalid Request Format	| The request format is not valid.| 
| 6	    | E006: Unexpected internal error	| Unexpected internal error.| 
| 30	| E030: Empty Request	| The request URL is not complete.| 
| 204	| E204: Too many SKU in one request	| The number of SKUs exceeds the limit.| 
| 501	| E501: Update product failed	| Failed to update the product price or stock.| 
| 901	| E901: The request is too frequent, or the requested functionality is temporarily disabled.	| Failed to return the requested data due to high calling frequency or disabled functionality. Please try again later.| 
| 1000	| Internal Application Error	| Internal system error.| 
| 4104	| BIZ_CHECK_PRICE_PRECISION_INVALID	| Price accuracy check failed| 
| 4105	| BIZ_CHECK_SELLER_SKU_DUPLICATE	| SellerSku repeat| 
| 4106	| CHK_CATPROP_CPV_INPUT_SIZE_LIMIT	| Item customization attributes exceeded the limit| 
| 4107	| CHECK_CAT_PROP_INVALID_NUMBER	| The category attribute value is invalid| 
| 4108	| CHK_BASIC_REQUIRED	| Basic attributes Mandatory verification| 
| 4109	| CHK_SKU_PROPS_NOT_MATCH_SALE_PROP	| Sku sales attributes do not match| 
| 4110	| BIZ_CHECK_CAT_PROP_MANDATORY	| Category attribute This parameter is mandatory| 
| 4111	| CHK_CATPROP_CPV_TEXT_REPEAT	| Category attribute content repeats| 
| 4112	| CHK_SKU_PROPS_DUPLICATE	| Duplicate Sku attributes| 
| 4113	| CHK_SKU_PROPS_NOT_IDENTICAL	| Sales attribute is not filled in| 
| 4114	| BIZ_CHECK_PRICE_SAMPLE_NON_ZERO	| The sample price is 0| 
| 4115	| CHK_CATPROP_CPV_NOT_ENUM	| The CPV attribute is not one of the options provided by the category| 
| 4116	| BIZ_CHECK_MAIN_IMAGE_DUPLICATE	| Repeat check of master diagram| 
| 4117	| BIZ_CHECK_SPECIAL_PRICE_FROM_DATE_AFTER_TO_DATE	| Special offer date check| 
| 4118	| BIZ_CHECK_PRICE_IS_ZERO	| Price is not 0 check| 
| 4119	| BIZ_CHECK_SPECIAL_PRICE_RATE_OUT_OF_RANGE	| Special price range check| 
| 4120	| CHK_CATPROP_CPV_MAX_LEGNTH	| Verify the maximum CPV value of a category| 
| 4121	| BIZ_CHECK_SPECIAL_PRICE_PRECISION_INVALID	| Special accuracy check does not pass| 
| 4122	| BIZ_CHECK_VIRTUAL_BUNDLE_SKU_SUB_OVER_LIMIT	| virtual bundle sku relation skuc over limit| 
| 4123	| BIZ_CHECK_MANGROVE_RULE	| Restricted publication check| 
| 4124	| BIZ_CHECK_MANGROVE_RULE_QC	| MANGROVE rule verification| 
| 4125	| THD_IC_F_IC_DOMAIN_PROPERTY_002	| IC Verification category Attribute This parameter is mandatory| 
| 4126	| THD_IC_F_IC_INFRA_PRODUCT_036	| SellerSku repeat| 
| 4127	| THD_IC_F_IC_SCENE_PUBLISH_012	| ProductId repeat| 
| 4128	| THD_IC_F_IC_DOMAIN_ACTOR_006	| Seller lock cannot be edited| 
| 4129	| BIZ_CHECK_PROP_SPECIAL_CHAR	| Containssymbol/characterthatisnotallowed:"<".Pleaseremovethenre-upload| 
| 4130	| BIZ_CHECK_OFFICIAL_STORE_BRAND_UNAUTHORIZED	| Uncertified brand| 
| 4131	| BIZ_CHECK_CAT_PROP_SENSITIVE_WORDS	| description has sensitive words New brand| 
| 4132	| Invalid Request Format	| Invalid Request Format| 
| 4133	| Invalid variation	| Invalid variation| 
