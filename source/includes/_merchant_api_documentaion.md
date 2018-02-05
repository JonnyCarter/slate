# Merchant API Documentation

# API ENDPOINTS

To use the Divido API to query data, you will need to send a request to the correct endpoint. Request endpoints should depend on whether you wish to query the live or sandbox environment:
Sandbox: https://merchant-api.api.dev.divido.net
Live: https://merchant-api.api.divido.net

## HTTP RESPONSE CODES

You may encounter the following response codes. Any unsuccessful response codes will contain more information to help you identify the cause of the problem.
+ 200 The request has succeeded.

+ 201 The request has been fulfilled and resulted in a new resource being created. The newly created resource can be referenced by the URI(s) returned in the entity of the response, with the most specific URI for the resource given by a Location header field.

+ 404 Not Found. The requested resource was not found. The response body will explain which resource was not found.

+ 500 Internal Server Error. The server encountered an error while processing your request and failed. Please report this to the Divido support team.


## Get all applications

Returns all applications for the merchant

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
    + `include`: merchant_channel
    + `apiKey`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c

+ Body:
    No specific body attributes needed.


### Response:

> A typical Json response would look like this:

```json
{
  "meta": {
    "count": 25,
    "current_page": 1,
    "first_item": 1,
    "has_more_pages": true,
    "last_item": 25,
    "last_page": 77,
    "per_page": 25,
    "total": 1905
  },
  "links": {
    "self": "http:\/\/127.0.0.1:8004\/applications?page=1",
    "next": "http:\/\/127.0.0.1:8004\/applications?page=2"
  },
  "data": [
    {
      "type": "applications",
      "id": "2de1acad-748e-4249-85a4-a5ea54e72d84",
      "attributes": {
        "token": "7d81dd1790b23b4e21ac290b5c57024a",
        "finalised": 0,
        "finalisation_required": 0,
        "current_status": "PROPOSAL",
        "lender_reference": "",
        "lender_loan_reference": "",
        "form_data": {
          "first_name": "Ann",
          "middle_names": "",
          "last_name": "Heselden",
          "phone_number": "02012312312",
          "email": "hallsten@me.com"
        },
        "order": {
          "product_data": [
            {
              "sku": "",
              "name": "Goods",
              "quantity": 1,
              "price": 1000,
              "vat": 0,
              "unit": "",
              "image": "",
              "attributes": "1"
            }
          ],
          "refunds": [],
          "activations": [],
          "cancellations": []
        },
        "amounts": {
          "activatable_amount": 65000,
          "activated_amount": 0,
          "cancelable_amount": 65000,
          "cancelled_amount": 0,
          "original_credit_amount": 65000,
          "current_credit_amount": -34000,
          "deposit_amount": 35000,
          "monthly_payment_amount": 5417,
          "purchase_price_amount": 1000,
          "refundable_amount": 0,
          "refunded_amount": 0,
          "total_repayable_amount": 100000
        },
        "metadata": [],
        "activation_status": "AWAITING-ACTIVATION",
        "deposit_status": "UNPAID",
        "merchant_reference": "",
        "urls": {
          "merchant_redirect_url": "",
          "merchant_checkout_url": "",
          "merchant_notification_url": "",
          "application_url": "todo"
        },
        "created_at": "2017-12-20T11:02:24+00:00",
        "updated_at": "2017-12-20T11:02:24+00:00"
      },
      "relationships": {
        "country": {
          "data": {
            "type": "countries",
            "id": "GB"
          }
        },
        "currency": {
          "data": {
            "type": "currencies",
            "id": "GBP"
          }
        },
        "deposits": {
          "data": []
        },
        "application_histories": {
          "data": [
            {
              "type": "application-histories",
              "id": "2c012aeb-cce7-489a-a8c7-16db9d8cbf7a"
            }
          ]
        },
        "language": {
          "data": {
            "type": "languages",
            "id": "en"
          }
        },
        "merchant": {
          "data": {
            "type": "merchants",
            "id": "M9B458218-0C86-6121-1315-897A84A60E54"
          }
        },
        "merchant_channel": {
          "data": {
            "type": "merchant-channels",
            "id": "CFAD1A99F-E377-5C4E-B4E7-20E48E3F8D41"
          }
        },
        "finance_plan": {
          "data": {
            "type": "finance-plans",
            "id": "FBB4B79B2-6C98-127C-8119-66516B188E9B"
          }
        }
      },
      "links": {
        "self": "http:\/\/127.0.0.1:8004\/applications\/2de1acad-748e-4249-85a4-a5ea54e72d84"
      }
    },
    ...
```

## Get a single application

Returns a single applicaiton
### HTTP Request
`GET /applications/<APPLICATION_ID>`

**

### Request:

+ Headers:
    + `X-DIVIDO-API-KEY`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c
    
+ Url Params:
    + `include`: deposits,application_histories,language
    + `apiKey`: sandbox_pk_c82185fa3.c423e2ace9177c856b51401f86c3fc2c


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