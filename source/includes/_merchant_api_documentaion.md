# Merchant API Documentation

## Get all applications

### HTTP Request
`GET /applications`

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    + `filter`: current_status:proposal|declined
    + `page`: 1
    + `sort`: current_status

+ Body:
    No specific body attributes needed.


### Response:

+ Status: **0**

+ Body:


## Get a single application

### HTTP Request
`GET /applications/<APPLICATION_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    
+ Url Params:
    + `include`: deposits,application_histories,language

+ Body:
    No specific body attributes needed.

***



## Create an application

### HTTP Request
`POST /applications`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:

> The Above returns Json Like this:

```json
{
    "token": "example-token-sdihudsh98ds",
    "event": "application_store",
    "merchant_finance_id": "F4CA2E40A-B544-F75F-825A-FFF7613E7230",
    "merchant_channel_id": "C368EC936-60B5-CD0A-5FCB-7F3867B8FA9D",
    "finalisation_required": false,
    "deposit_percentage": 0.02,
    "age": 40,
    "country_id": "GB",
    "currency_id": "GBP",
    "language_id": "en",
    "form_data": {
        "firstName": "ann",
        "middleNames": "",
        "lastName": "heselden",
        "phoneNumber": "07512345678"
    },
    "order": {
        "items": [
            {
                "sku": "",
                "name": "Tax",
                "quantity": 1,
                "price": 4.94,
                "vat": 0,
                "unit": "",
                "image": "",
                "attributes": null
            },
            {
                "sku": "",
                "name": "Shipping Total",
                "quantity": 1,
                "price": 8.05,
                "vat": 0,
                "unit": "",
                "image": "",
                "attributes": null
            }
        ]
    },
    "amount": 10000,
    "deposit_percantage": 0.1,
    "deposit_amount": 10000,
    "metadata": {
        "foo": "bar"
    },
    "merchant_reference": "made-up-referefce",
    "merchant_redirect_url": "http://example.com",
    "merchant_checkout_url": "http://example.com",
    "merchant_response_url": "http://example.com"
}
```

***



## Update an application

### HTTP Request
`PUT /applications/<APPLICATION_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get all activations 

### HTTP Request
`GET /applications/<APPLICATION_ID>/activations`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get a specific activation

### HTTP Request
`GET /applications/<APPLICATION_ID>/activations/<ACTIVATION_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Create an activation

### HTTP Request
`POST /applications/<APPLICATION_ID>/activations`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get all cancellations

### HTTP Request
`GET /applications/<APPLICATION_ID>/cancellations`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get a specific cancellation

### HTTP Request
`GET /applications/<APPLICATION_ID>/cancellations/<CANCELLATION_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Create a cancellation

### HTTP Request
`POST /applications/<APPLICATION_ID>/cancellations`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get all refunds 

### HTTP Request
`GET /applications/<APPLICATION_ID>/refunds`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get a specific refund

### HTTP Request
`GET /applications/<APPLICATION_ID>/refunds/<REFUND_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Create a Refund

### HTTP Request
`POST /applications/<APPLICATION_ID>/refunds`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get all finanace Plans

### HTTP Request
`GET /finance-plans`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***

### Response:

+ Status: **0**

+ Body:

***

## Service Healthcheck
### HTTP Request
`GET /health`

**

### Request:

+ Headers:
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***



## Get all settlements

### HTTP Request
`GET /settlements`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    + `sort`: currency

+ Body:
    No specific body attributes needed.

***



## Retrieve a settlement
### HTTP Request
`GET /settlements/<SETTLEMENT_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    + `Accept`: application/json
    
+ Url Params:
    No specific query parameters needed.

+ Body:
    No specific body attributes needed.

***