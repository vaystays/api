---
title: Direct API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:wes@directsoftware.com?subject=Developer%20Key%20Request'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Direct API! You can use our API to access Direct API endpoints, including information on properties, units, rates, availability, and quotes in our database. You can view code examples in the dark area to the right.

Staging: `https://staging.getdirect.io/api/public/<ORG_ID>`

Production: `https://app.getdirect.io/api/public/<ORG_ID>`

where `<ORG_ID>` is the ID of the connected organization.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> Make sure to replace `your_api_key` with your API key.

Direct uses API keys to allow access to the API. You can register a new Direct API key by emailing us at [engineering@getdirect.io](mailto:engineering@getdirect.io?subject=Developer%20Key%20Request).

Direct expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: your_api_key`

`Accept: application/vnd.direct.v1`

<aside class="notice">
You must replace <code>your_api_key</code> with your personal API key.
</aside>

# Promotions

## Get All Promotions

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/promotions"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   [
      {
         "id": 100030000042,
         "special_type": "percent",
         "amount": 30,
         "req_nights": 3,
         "travel_date_start": "2020-05-01",
         "travel_end_date": "2020-07-31",
         "promo_start_date": "2020-03-23",
         "promo_end_date": "2020-04-30",
         "days_of_week": null,
         "code_req": true,
         "coupon_code": "STAYAGAIN3N",
         "name": "30% Off 3+ Nights",
         "internal_name": "30PCT",
         "distro_list": null,
         "portfolio_id": 100030000018,
         "subportfolio_id": 100030000013,
         "created_at": "2020-03-23T19:33:11.462Z",
         "updated_at": "2020-04-21T19:34:00.294Z",
         "active": false,
         "organization_id": 3
      },
      { ... }
   ]
```

This endpoint retrieves all promotions connected to your organization.

### HTTP Request

`GET /promotions`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (optional) | Maximum number of promotions to return, up to 100. Default is 20.
_offset (optional) | Number of promotions to skip over, where the ordering is consistent but unspecified.

## Get a Specific Promotion

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/promotions/<ID>"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
      "id": 100030000042,
      "special_type": "percent",
      "amount": 30,
      "req_nights": 3,
      "travel_date_start": "2020-05-01",
      "travel_end_date": "2020-07-31",
      "promo_start_date": "2020-03-23",
      "promo_end_date": "2020-04-30",
      "days_of_week": null,
      "code_req": true,
      "coupon_code": "STAYAGAIN3N",
      "name": "30% Off 3+ Nights",
      "internal_name": "30PCT",
      "distro_list": null,
      "portfolio_id": 100030000018,
      "subportfolio_id": 100030000013,
      "created_at": "2020-03-23T19:33:11.462Z",
      "updated_at": "2020-04-21T19:34:00.294Z",
      "active": false,
      "organization_id": 3
   }
```

This endpoint retrieves a specific promotion.

### HTTP Request

`GET /promotions/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the promotion to retrieve

# Properties

## Get All Properties

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/properties"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
{
   "properties":[
      {
         "id":92,
         "name":"Westgate Resort Bella Suite",
         "updated_at":"2018-12-11T23:56:42.904Z"
      },
      {
         "id":39,
         "name":"La Palme- Sanctuary",
         "updated_at":"2018-12-11T22:39:54.001Z"
      }
   ],
   "total_count": 2
}
```

This endpoint retrieves all properties connected to your organization.

### HTTP Request

`GET /properties`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (optional) | Maximum number of properties to return, up to 100. Default is 20.
_offset (optional) | Number of properties to skip over, where the ordering is consistent but unspecified.

## Get a Specific Property

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/properties/<ID>"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
{
   "id":92,
   "name":"Westgate Resort Bella Suite",
   "updated_at":"2018-12-11T23:56:42.904Z",
   "address":{
      "addressLine1":"3000 Canyons Resort Drive",
      "addressLine2":"3704",
      "city":"Park City",
      "state":"UT",
      "country":"US",
      "postalCode":"84098",
      "lat":40.6845975,
      "lng":-111.5548417
   },
   "features":[
      "Cycling",
      "Fishing",
      ...
   ],
   "images":[
      {
         "label":"",
         "uri":"<image url>"
      }
   ],
   "units":[
      {
         "id":92,
         "active":true,
         "description":null,
         "propertyType":"PROPERTY_TYPE_CONDO",
         "currency":"USD",
         "name":"PCWG3704",
         "bathrooms":[
            {
               "id":185,
               "roomSubType":"SHOWER_INDOOR_OR_OUTDOOR",
               "amenities":[]
            }
         ],
         "bedrooms":[
            {
               "id":187,
               "roomSubType":"OTHER_SLEEPING_AREA",
               "amenities":[]
            }
         ],
         "unitFeatures":[
            "Air conditioning",
            "Elevator",
            ...
         ]
      }
   ]
}
```

This endpoint retrieves a specific property.

### HTTP Request

`GET /properties/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the property to retrieve

# Reservations

## List Reservations

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/reservations"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
      "reservations": [
        {
            "id": 951,
            "booking_code": "2VXUAWPE5-ZVCRY7",
            "updated_at": "2019-01-25T01:04:39.744Z",
            "check_in_time": "2019-04-27T15:00:00.000-05:00",
            "check_out_time": "2019-05-02T23:00:00.000-05:00",
            "unit_id": 1,
            "property_id": 1
        },
        {
            "id": 1811,
            "booking_code": "EQRMH4-L6QR1EALF",
            "updated_at": "2019-01-25T01:03:14.583Z",
            "check_in_time": "2019-03-13T15:00:00.000-05:00",
            "check_out_time": "2019-03-16T23:00:00.000-05:00",
            "unit_id": 2,
            "property_id": 1
        }
      ],
      "total_count": 2
   }
```

This endpoint retrieves all reservations connected to your organization.

### HTTP Request

`GET /reservations`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (optional) | Maximum number of reservations to return, up to 100. Default is 20.
_offset (optional) | Number of reservations to skip over, where the ordering is consistent but unspecified.

## Create Reservation

```shell
curl "https://staging.getdirect.io/api/public/990/reservations"
-d '{
    "property_id": 1,
    "unit_id": 1,
    "customer": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "john.doe@test.com",
      "phone": "1234567890",
      "address": {
        "addressLine1": "123 Main Street"
        "addressLine2": "",
        "city": "Chicago",
        "state": "IL",
        "country": "US",
        "postal_code": "60654"
      }
    },
    "reservation": {
      "check_in": "2019-04-03",
      "check_out": "2019-04-07",
      "adults": 2,
      "children": 0,
      "pets": 0
    },
    "payment": {
      "number": "4111111111111111",
      "cvv": "123",
      "expiration_month": "02",
      "expiration_year": "2020",
      "name_on_card": "John Doe"
      "billing_address": {
        "addressLine1": "123 Main Street"
        "addressLine2": "",
        "city": "Chicago",
        "state": "IL",
        "country": "US",
        "postal_code": "60654"
      }
    }
  }'
-H "Authorization: Token test_api_key"
-H "Accept: application/vnd.direct.v1"
-H "Content-Type: application/json"
-X POST
```

> The above command returns JSON structured like this:

```json
{
    "id": 951,
    "booking_code": "2VXUAWPE5-ZVCRY7",
    "updated_at": "2019-01-25T01:04:39.744Z",
    "cancelled": false,
    "confirmed": false,
    "archived": false,
    "num_guests": 1,
    "days_booked": 3,
    "check_in": "2019-04-03",
    "check_out": "2019-04-07",
    ...
}
```

This endpoint creates a new reservation for the requested unit.

### HTTP Request

`POST /reservations`

## Get Reservation

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/reservations/<ID>"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
{
    "id": 951,
    "booking_code": "2VXUAWPE5-ZVCRY7",
    "updated_at": "2019-01-25T01:04:39.744Z",
    "status": {
        "cancelled": false,
        "confirmed": true,
        "archived": true
    },
    "num_guests": 0,
    "days_booked": 3,
    "check_in": "2011-10-21",
    "check_out": "2011-10-23",
    "channel": "booking.com",
    "customer": {
        "name": "christopher zepf",
        "email": "ndirish1@gmail.com",
        "telephone": null,
        "location": {
          "city": "Chicago",
          "state": "IL",
          "postal_code": null,
          "country": "USA"
        }
    }
}
```

This endpoint retrieves a specific reservation.

### HTTP Request

`GET /reservations/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the reservatoion to retrieve

### Request Parameters

Parameter | Description
--------- | -----------
property_id | The unique identifier of the property being booked
unit_id | The unique identifier of the unit being booked
customer | Information about the customer making the inquiry
reservation | Information about the reservation, including stay dates and guest counts
payment | Payment information, including billing address and credit card details

## Update Reservation

```shell
curl "https://staging.getdirect.io/api/public/3/reservations/100030030467"
-d '{"door_code": "1AT9B3"}'
-H "Authorization: Token test_api_key"
-H "Accept: application/vnd.direct.v1"
-H "Content-Type: application/json"
-X PUT
```

> The above command returns JSON structured like this:

```json
   {
      "id": 100030030467,
      "booking_code": "SHBNSIAFTSZE9XVJ",
      "door_code": "1AT9B3",
      "updated_at": "2020-12-28T16:35:51.725Z",
      "property_id": 100030000002,
      "unit_id": 100030000002,
      "status": {
         "cancelled": true,
         "confirmed": true,
         "archived": true
      },
      "num_guests": 11,
      "days_booked": 26,
      "date_booked": "2019-10-04T00:00:00.000Z",
      "check_in_time": "2020-03-28T17:00:00.000+00:00",
      "check_out_time": "2020-04-22T11:00:00.000+00:00",
      "price_status": "partial",
      "stay_type": "guest",
      "rent_total": 7400,
      "extras_total": 628,
      "booking_total": 8123,
      "channel": "direct",
      "quote_line_items": [
         {
            "id": 100030475410,
            "name": "Room Rate",
            "total_cents": 740000,
            "rate": 296.0,
            "taxable": true,
            "item_type": "room_rate",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.715Z",
            "updated_at": "2020-02-24T17:47:26.715Z",
            "refundable": false,
            "optional": false,
            "additional_data": {},
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475411,
            "name": "Weekly Discount",
            "total_cents": 35520,
            "rate": 4.8,
            "taxable": true,
            "item_type": "discount",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.726Z",
            "updated_at": "2020-02-24T17:47:26.726Z",
            "refundable": false,
            "optional": false,
            "additional_data": {},
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475412,
            "name": "Management Fee",
            "total_cents": 8450,
            "rate": 1.2,
            "taxable": false,
            "item_type": "fees",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.735Z",
            "updated_at": "2020-02-24T17:47:26.735Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "frequency_at_creation": "per_stay",
               "included_in_base_rent": false,
               "los_ranges_at_creation": [],
               "default_calculation_amount": 1.2
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475413,
            "name": "Processing Fee",
            "total_cents": 27475,
            "rate": 3.9,
            "taxable": false,
            "item_type": "fees",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.744Z",
            "updated_at": "2020-02-24T17:47:26.744Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "frequency_at_creation": "per_stay",
               "included_in_base_rent": false,
               "los_ranges_at_creation": [],
               "default_calculation_amount": 3.9
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475414,
            "name": "Linen Fee",
            "total_cents": 2000,
            "rate": null,
            "taxable": false,
            "item_type": "fees",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.758Z",
            "updated_at": "2020-02-24T17:47:26.758Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "frequency_at_creation": "per_stay",
               "included_in_base_rent": false,
               "los_ranges_at_creation": [],
               "default_calculation_amount": 20.0
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475415,
            "name": "Damage Waiver",
            "total_cents": 9900,
            "rate": null,
            "taxable": false,
            "item_type": "fees",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.770Z",
            "updated_at": "2020-02-24T17:47:26.770Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "frequency_at_creation": "per_stay",
               "included_in_base_rent": false,
               "los_ranges_at_creation": [],
               "default_calculation_amount": 99.0
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475416,
            "name": "Cleaning Fee",
            "total_cents": 15000,
            "rate": null,
            "taxable": false,
            "item_type": "fees",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.786Z",
            "updated_at": "2020-02-24T17:47:26.786Z",
            "refundable": false,
            "optional": false,
            "additional_data": {
               "frequency_at_creation": "per_stay",
               "included_in_base_rent": false,
               "los_ranges_at_creation": [],
               "default_calculation_amount": 150.0
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475417,
            "name": "Additional Guest Fee",
            "total_cents": 0,
            "rate": null,
            "taxable": true,
            "item_type": "fees",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.803Z",
            "updated_at": "2020-02-24T17:47:26.803Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "frequency_at_creation": "per_stay",
               "included_in_base_rent": false,
               "additional_guest_start": 1,
               "los_ranges_at_creation": [],
               "default_calculation_amount": 0.0
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475418,
            "name": "Sales Tax",
            "total_cents": 25009,
            "rate": 3.55,
            "taxable": false,
            "item_type": "taxes",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.814Z",
            "updated_at": "2020-02-24T17:47:26.814Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "tax_type": "Sales tax"
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475419,
            "name": "City Tax",
            "total_cents": 20078,
            "rate": 2.85,
            "taxable": false,
            "item_type": "taxes",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.826Z",
            "updated_at": "2020-02-24T17:47:26.826Z",
            "refundable": true,
            "optional": false,
            "additional_data": {
               "tax_type": "City tax"
            },
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         },
         {
            "id": 100030475420,
            "name": "Booking Total",
            "total_cents": 812392,
            "rate": null,
            "taxable": true,
            "item_type": "total",
            "itemizable_type": "Quote",
            "itemizable_id": 100030030459,
            "created_at": "2020-02-24T17:47:26.837Z",
            "updated_at": "2020-02-24T17:47:26.837Z",
            "refundable": false,
            "optional": false,
            "additional_data": {},
            "organization_id": 3,
            "split": "no",
            "cancellation": false,
            "occurrence_date": null,
            "debit_account_id": null,
            "credit_account_id": null
         }
      ],
      "price_paid": "4061.96",
      "price_remaining": "4061.96",
      "date_cancelled": "2020-12-28T16:35:51.725Z",
      "customer": {
         "name": "Maryanne Nitzsche",
         "email": "amandahowe@lehnerjacobson.name",
         "telephone": "210.820.9588",
         "location": {
            "city": null,
            "state": null,
            "postal_code": null,
            "country": null
         }
      }
   }
```

This endpoint updates the door code for the specified reservation given.

### HTTP Request

`PUT /reservations/<R_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
R_ID | The ID of the reservation to retrieve

### Request Parameters

Parameter | Description
--------- | -----------
door_code | The code to unlock the property's door

# Reviews

## Get All Reviews

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/reviews"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   [
      {
         "id": 100030000012,
         "unit_id": 100030000053,
         "booking_id": 100030031551,
         "title": "Great luxury property for families ",
         "body": "<p>Testing the review. Great location! Super clean&nbsp;</p>\n",
         "name": "Lauren A Flaugher",
         "check_in_date": "2020-05-24T00:00:00.000Z",
         "status": "published",
         "rating": 5,
         "created_at": "2020-05-22T19:10:21.967Z",
         "updated_at": "2020-05-22T19:18:02.117Z",
         "reviewed_date": "2020-05-22T19:10:21.965Z",
         "check_out_date": "2020-05-31T00:00:00.000Z",
         "where_from": null,
         "organization_id": 3,
         "customer_id": null
      },
      { ... }
   ]
```

This endpoint retrieves all reviews connected to your organization.

### HTTP Request

`GET /reviews`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (optional) | Maximum number of reviews to return, up to 100. Default is 20.
_offset (optional) | Number of reviews to skip over, where the ordering is consistent but unspecified.

## Get a Specific Review

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/reviews/<ID>"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
      "id": 100030000012,
      "unit_id": 100030000053,
      "booking_id": 100030031551,
      "title": "Great luxury property for families ",
      "body": "<p>Testing the review. Great location! Super clean&nbsp;</p>\n",
      "name": "Lauren A Flaugher",
      "check_in_date": "2020-05-24T00:00:00.000Z",
      "status": "published",
      "rating": 5,
      "created_at": "2020-05-22T19:10:21.967Z",
      "updated_at": "2020-05-22T19:18:02.117Z",
      "reviewed_date": "2020-05-22T19:10:21.965Z",
      "check_out_date": "2020-05-31T00:00:00.000Z",
      "where_from": null,
      "organization_id": 3,
      "customer_id": null
   }
```

This endpoint retrieves a specific review.

### HTTP Request

`GET /reviews/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the review to retrieve

# Search

## Get Listings

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/search"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
      "results": [
         {
            "average_default_nightly_price": 296,
            "bookable_nightly_price": 296,
            "currency": "usd",
            "property": {
               "id": 100030000171,
               "name": "The Pointe Resort",
               "active": true,
               "multi_unit": true,
               "summary_accommodations": null,
               "summary_description": "<p style=\"text-align:left;\"><span style=\"color: rgb(42,42,42);background-color: rgb(255,255,255);font-size: 15px;font-family: webfontregular, Arial, Helvetica, sans-serif;\">A spacious luxury condominium spanning 2000+ square feet, The Pointe 3-bedroom allows you to come together with friends and family in an expansive open floor plan with kitchen, dining, and living room, while still providing tranquil personal space with each of the three bedrooms. </span></p>\n<p style=\"text-align:left;\"><span style=\"color: rgb(42,42,42);background-color: rgb(255,255,255);font-size: 15px;font-family: webfontregular, Arial, Helvetica, sans-serif;\">Between poolside relaxing and beach dreaming, use the stainless steel kitchen to prepare small bites, full meals, or cocktails and enjoy around the kitchen island, curl up on the modern plush couch to indulge in the upcoming sporting event, or just kick back on one of the three balconies with wood trellis accents.</span></p>\n<p style=\"text-align:left;\"><span style=\"color: rgb(42,42,42);background-color: rgb(255,255,255);font-size: 15px;font-family: webfontregular, Arial, Helvetica, sans-serif;\">The master bedroom comes with an office nook if you are inclined to do some work while visiting The Pointe, and if you’d rather relax, this bedroom is equipped with a flat screen television, bathroom with bathtub and separate shower, and entrance onto its private balcony or patio.</span></p>\n<p style=\"text-align:left;\"><span style=\"color: rgb(42,42,42);background-color: rgb(255,255,255);font-size: 15px;font-family: webfontregular, Arial, Helvetica, sans-serif;\">The bedroom off of the living room is discretely tucked away by closing off the sleek farm doors, and features a bathroom with separate bathtub and shower, dual sinks, and water closet.</span></p>\n<p><span style=\"color: rgb(42,42,42);background-color: rgb(255,255,255);font-size: 15px;font-family: webfontregular, Arial, Helvetica, sans-serif;\">The final bedroom includes two double beds, flat screen tv, office space, bathroom, and entry to its own private balcony or patio.</span></p>\n<p style=\"text-align:left;\"><span style=\"color: rgb(42,42,42);background-color: rgb(255,255,255);font-size: 15px;font-family: webfontregular, Arial, Helvetica, sans-serif;\">Each 3-bedroom comes with washer and dryer, so you can feel productive while doing some poolside lounging.</span></p>\n",
               "summary_headline": "The Pointe - Three Bedroom with Plunge Pool",
               "summary_rules": null,
               "features_adventure": {
                  "SPORTS_BASKETBALL_COURT": {
                     "label": "Basketball court",
                     "value": true
                  },
                  { ... }
               },
               "features_attractions": {
                  "ATTRACTIONS_ARBORETUM": {
                     "label": "Arboretum",
                     "value": true
                  },
                  { ... }
               },
               "features_car": {
                  "CAR_NECESSARY": {
                     "label": "Necessary",
                     "value": false
                  },
                  { ... }
               },
               "features_leisure": {
                  "LEISURE_ANTIQUING": {
                     "label": "Antiquing",
                     "value": true
                  },
                  { ... }
               },
               "features_local": {
                  "LOCAL_ATM_BANK": {
                     "label": "ATM",
                     "value": false
                  },
                  { ... }
               },
               "features_location": {
                  "LOCATION_TYPE_BEACH": {
                     "label": "Beach",
                     "value": true
                  },
                  { ... }
               },
               "property_type": "condo_hotel",
               "organization_id": 3,
               "created_at": "2019-03-26T17:31:39.052Z",
               "updated_at": "2021-01-19T21:48:31.103Z",
               "manager_info_visible": false,
               "registration_id": "",
               "external_id": null,
               "extra": {},
               "unit_code": "",
               "features_cleaning": {}
            },
            "location": {
               "id": 100030000258,
               "adr_street": "10711 E COUNTY HWY 30A ",
               "adr_unit": "",
               "adr_city": "Rosemary Beach",
               "adr_state": "FL",
               "adr_country": "United States",
               "adr_postal_code": "32461",
               "geo_latitude": 30.27991669999999,
               "geo_longitude": -86.0110212,
               "locationable_type": "Property",
               "locationable_id": 100030000171,
               "created_at": "2019-03-26T17:31:39.065Z",
               "updated_at": "2020-03-05T16:58:14.327Z",
               "organization_id": 3,
               "exact": false
            },
            "distance": 1298.3491129728013,
            "listings": [
               {
                  "listing": {
                     "id": 100030000206,
                     "currency": "usd",
                     "unit_id": 100030000182,
                     "tax_rate": 5.0,
                     "brand_id": 100030000048,
                     "instant_booking": true,
                     "refund_policy": null,
                     "refund_policy_custom": null,
                     "featured": false,
                     "created_at": "2019-03-26T17:34:19.547Z",
                     "updated_at": "2021-01-19T21:48:30.803Z",
                     "enabled_distribution_homeaway": false,
                     "enabled_distribution_booking": false,
                     "enabled_distribution_airbnb": false,
                     "airbnb_refund_policy": null,
                     "booking_dot_com_refund_policy": null,
                     "homeaway_refund_policy": null,
                     "adj_tax": 0.0,
                     "max_night_with_tax_rate": 0,
                     "exclude_tax": false,
                     "tax_adjustable": false,
                     "organization_id": 3,
                     "slug": "the-pointe-resort",
                     "is_multi_unit": true,
                     "is_room_type": true,
                     "rate_inflator": null
                  },
                  "unit": {
                     "id": 100030000182,
                     "name": "Three Bedroom with Plunge Pool",
                     "active": true,
                     "summary_description": null,
                     "features_accommodations": {
                        "ACCOMMODATIONS_TYPE_BED_AND_BREAKFAST": {
                           "label": "Bed and breakfast",
                           "value": false
                        },
                        { ... }
                     },
                     "features_amenities": {
                        "AMENITIES_AIR_CONDITIONING": {
                           "label": "Air conditioning",
                           "value": true
                        },
                        { ... }
                     },
                     "features_dining": {
                        "KITCHEN_DINING_AREA": {
                           "label": "Dining area",
                           "value": false
                        },
                        { ... }
                     },
                     "features_entertainment": {
                        "ENTERTAINMENT_BOOKS": {
                           "label": "Books",
                           "value": false
                        },
                        { ... }
                     },
                     "features_outdoor": {
                        "OUTDOOR_BALCONY": {
                           "label": "Balcony",
                           "value": false
                        },
                        { ... }
                     },
                     "features_spa": {
                        "POOL_SPA_COMMUNAL_POOL": {
                           "label": "Communal pool",
                           "value": false
                        },
                        { ... }
                     },
                     "features_suitability": {
                        "SUITABILITY_CHILDREN_WELCOME": {
                           "label": "Children welcome",
                           "value": false
                        },
                        { ... }
                     },
                     "features_themes": {
                        "THEMES_ADVENTURE": {
                           "label": "Adventure",
                           "value": false
                        },
                        { ... }
                     },
                     "num_bathrooms": 3.0,
                     "num_bedrooms": 4,
                     "num_lounge": null,
                     "num_sleep": 6,
                     "num_sleep_in_beds": 6,
                     "unit_type": "condo",
                     "property_id": 100030000171,
                     "created_at": "2019-03-26T17:34:16.398Z",
                     "updated_at": "2021-01-19T21:48:30.805Z",
                     "check_in_instructions": {},
                     "emergency_contact_phone": null,
                     "emergency_contact_first_name": null,
                     "emergency_contact_last_name": null,
                     "portfolio_id": 100030000018,
                     "external_id": null,
                     "external_contract_id": 100030000015,
                     "airbnb_headline": "Three Bedroom with Plunge Pool",
                     "pointcentral_customer_id": null,
                     "organization_id": 3,
                     "extra": {},
                     "subportfolio_id": 100030000013,
                     "unit_group_id": 100030000021,
                     "rate_group_id": 100030000060,
                     "size": null,
                     "measurement_type": "sq_feet",
                     "minimum_age": null,
                     "features_safety": {
                        "SMOKE_DETECTOR": {
                           "label": "Smoke Detector",
                           "value": false
                        },
                        { ... }
                     },
                     "guest_controls_description": null,
                     "unit_code": "RRCDD",
                     "enabled_on_kaba": false,
                     "room_type_id": 100030000001
                  },
                  "pricing": {
                     "id": 100030000298,
                     "default_nightly_weekday": "425.0",
                     "default_nightly_weekend": "630.0",
                     "discount_full_week": "5.0",
                     "discount_full_month": "15.0",
                     "pricing_calendar": {
                        "17-05-2021": {
                           "note": "unit range 100030000303 has updated this pricing",
                           "weekly": "1.0",
                           "monthly": "5.0",
                           "range_type": "high",
                           "nightlyWeekday": "600.0",
                           "nightlyWeekend": "600.0"
                        },
                        { ... }
                     },
                     "unit_listing_id": 100030000206,
                     "created_at": "2020-02-04T19:05:31.120Z",
                     "updated_at": "2020-11-11T20:56:23.782Z",
                     "organization_id": 3,
                     "unit_id": 100030000182,
                     "additional_guest_amount_cents": null,
                     "additional_guest_start": 1
                  },
                  "average_default_nightly_price": 483.57,
                  "bookable_nightly_price": 660.0,
                  "can_fit_guests": true,
                  "num_bathrooms": 3.0,
                  "num_bedrooms": 4,
                  "bookable": true,
                  "can_stay": true,
                  "bookable_nightly_price_before_promotion": 660.0,
                  "available": true,
                  "booked": false,
                  "changeover": [
                     "any",
                     "any"
                  ],
                  "instant_booking": true
               },
               {
                  "listing": {
                     "id": 100030000249,
                     "currency": "usd",
                     "unit_id": 100030000183,
                     "tax_rate": 5.0,
                     "brand_id": 100030000048,
                     "instant_booking": true,
                     "refund_policy": "day30",
                     "refund_policy_custom": "",
                     "featured": false,
                     "created_at": "2020-02-04T19:13:04.952Z",
                     "updated_at": "2021-01-19T21:48:31.098Z",
                     "enabled_distribution_homeaway": true,
                     "enabled_distribution_booking": true,
                     "enabled_distribution_airbnb": true,
                     "airbnb_refund_policy": "moderate",
                     "booking_dot_com_refund_policy": "day30",
                     "homeaway_refund_policy": "strict",
                     "adj_tax": 0.0,
                     "max_night_with_tax_rate": 0,
                     "exclude_tax": false,
                     "tax_adjustable": false,
                     "organization_id": 3,
                     "slug": "the-pointe-resort",
                     "is_multi_unit": true,
                     "is_room_type": true,
                     "rate_inflator": null
                  },
                  "unit": {
                     "id": 100030000183,
                     "name": "Three Bedroom with Plunge Pool",
                     "active": true,
                     "summary_description": "<p style=\"text-align:start;\"><span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">Condo | 2,000+ Square Feet</span></p>\n<p style=\"text-align:start;\"><span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">Sleeps:</span> <span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">6</span></p>\n<p style=\"text-align:start;\"><span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">Bathrooms:</span> <span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">3 | Bedrooms:</span> <span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">3</span></p>\n<p style=\"text-align:start;\"><span style=\"color: rgb(26,25,25);background-color: rgb(255,255,255);font-size: 14px;font-family: inherit;\">Pool View</span></p>\n",
                     "features_accommodations": {
                        "ACCOMMODATIONS_TYPE_BED_AND_BREAKFAST": {
                           "label": "Bed and breakfast",
                           "value": false
                        },
                        { ... }
                     },
                     "features_amenities": {
                        "AMENITIES_AIR_CONDITIONING": {
                           "label": "Air conditioning",
                           "value": true
                        },
                        { ... }
                     },
                     "features_dining": {
                        "KITCHEN_DINING_AREA": {
                           "label": "Dining area",
                           "value": false
                        },
                        { ... }
                     },
                     "features_entertainment": {
                        "ENTERTAINMENT_BOOKS": {
                           "label": "Books",
                           "value": false
                        },
                        { ... }
                     },
                     "features_outdoor": {
                        "OUTDOOR_BALCONY": {
                           "label": "Balcony",
                           "value": false
                        },
                        { ... }
                     },
                     "features_spa": {
                        "POOL_SPA_COMMUNAL_POOL": {
                           "label": "Communal pool",
                           "value": false
                        },
                        { ... }
                     },
                     "features_suitability": {
                        "SUITABILITY_CHILDREN_WELCOME": {
                           "label": "Children welcome",
                           "value": false
                        },
                        { ... }
                     },
                     "features_themes": {
                        "THEMES_ADVENTURE": {
                           "label": "Adventure",
                           "value": false
                        },
                        { ... }
                     },
                     "num_bathrooms": 3.0,
                     "num_bedrooms": 4,
                     "num_lounge": null,
                     "num_sleep": 6,
                     "num_sleep_in_beds": 6,
                     "unit_type": "condo",
                     "property_id": 100030000171,
                     "created_at": "2019-03-26T17:36:25.261Z",
                     "updated_at": "2021-01-19T21:48:31.099Z",
                     "check_in_instructions": {},
                     "emergency_contact_phone": null,
                     "emergency_contact_first_name": null,
                     "emergency_contact_last_name": null,
                     "portfolio_id": 100030000018,
                     "external_id": null,
                     "external_contract_id": 100030000015,
                     "airbnb_headline": "Three Bedroom with Plunge Pool",
                     "pointcentral_customer_id": null,
                     "organization_id": 3,
                     "extra": {},
                     "subportfolio_id": 100030000013,
                     "unit_group_id": 100030000021,
                     "rate_group_id": 100030000060,
                     "size": null,
                     "measurement_type": "sq_feet",
                     "minimum_age": null,
                     "features_safety": {
                        "SMOKE_DETECTOR": {
                           "label": "Smoke Detector",
                           "value": false
                        },
                        { ... }
                     },
                     "guest_controls_description": null,
                     "unit_code": null,
                     "enabled_on_kaba": false,
                     "room_type_id": 100030000001
                  },
                  "pricing": {
                     "id": 100030000299,
                     "default_nightly_weekday": "275.0",
                     "default_nightly_weekend": "350.0",
                     "discount_full_week": "3.0",
                     "discount_full_month": "5.0",
                     "pricing_calendar": {
                        "09-01-2021": {
                           "note": "unit range 100030000302 has updated this pricing",
                           "weekly": "1.0",
                           "monthly": "5.0",
                           "range_type": "high",
                           "nightlyWeekday": "600.0",
                           "nightlyWeekend": "600.0"
                        },
                        { ... }
                     },
                     "unit_listing_id": null,
                     "created_at": "2020-02-04T19:05:31.160Z",
                     "updated_at": "2020-11-11T20:56:24.874Z",
                     "organization_id": 3,
                     "unit_id": 100030000183,
                     "additional_guest_amount_cents": null,
                     "additional_guest_start": 1
                  },
                  "average_default_nightly_price": 296.43,
                  "bookable_nightly_price": 660.0,
                  "can_fit_guests": true,
                  "num_bathrooms": 3.0,
                  "num_bedrooms": 4,
                  "bookable": true,
                  "can_stay": true,
                  "bookable_nightly_price_before_promotion": 660.0,
                  "available": true,
                  "booked": false,
                  "changeover": [
                     "any",
                     "any"
                  ],
                  "instant_booking": true
               }
            ],
            "bookable": true,
            "featured": false,
            "num_bathrooms": 3,
            "num_bedrooms": 4,
            "name": "The Pointe Resort",
            "multi_unit": true,
            "room_type_property": true,
            "default_unit_id": 100030000182,
            "featured_image": {
               "id": 100030000739,
               "image": {
                  "url": "https://versailles.s3.amazonaws.com/production/tenant/blackrock-beach-properties/property/171/property_image/image/739/The-Pointe-August-afternoon-_28-1-1024x683.jpg?X-Amz-Expires=86400&X-Amz-Date=20210420T164224Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7VTIL5G2JOQOLMA%2F20210420%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=c8c8061fae336b1e4efbd5f2f59ced44303380e6442148524889fef6e639061e",
                  "tiny": {
                     "url": "https://versailles.s3.amazonaws.com/production/tenant/blackrock-beach-properties/property/171/property_image/image/739/tiny_The-Pointe-August-afternoon-_28-1-1024x683.jpg?X-Amz-Expires=86400&X-Amz-Date=20210420T164224Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7VTIL5G2JOQOLMA%2F20210420%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=82321b1a8f742353f8fedd9f8a77c5ca8cc3d068dfbca100c70e80d1f32a0e3b"
                  },
                  "small": {
                     "url": "https://versailles.s3.amazonaws.com/production/tenant/blackrock-beach-properties/property/171/property_image/image/739/small_The-Pointe-August-afternoon-_28-1-1024x683.jpg?X-Amz-Expires=86400&X-Amz-Date=20210420T164224Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7VTIL5G2JOQOLMA%2F20210420%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=c399b0f0a7c60da1f94ec4c1f0c41444d1912f9335cac14183bb2c4c72cdc83a"
                  },
                  "medium": {
                     "url": "https://versailles.s3.amazonaws.com/production/tenant/blackrock-beach-properties/property/171/property_image/image/739/medium_The-Pointe-August-afternoon-_28-1-1024x683.jpg?X-Amz-Expires=86400&X-Amz-Date=20210420T164224Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7VTIL5G2JOQOLMA%2F20210420%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=9c3c7a5a086a9f0b71230f087954b1445a64399e961d94b8810e0f138390bfb5"
                  },
                  "large": {
                     "url": "https://versailles.s3.amazonaws.com/production/tenant/blackrock-beach-properties/property/171/property_image/image/739/large_The-Pointe-August-afternoon-_28-1-1024x683.jpg?X-Amz-Expires=86400&X-Amz-Date=20210420T164224Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7VTIL5G2JOQOLMA%2F20210420%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=9158641e75c8492ee6589f00b11e53cf93e44711884c0aadf774c35b370e2140"
                  },
                  "xlarge": {
                     "url": "https://versailles.s3.amazonaws.com/production/tenant/blackrock-beach-properties/property/171/property_image/image/739/xlarge_The-Pointe-August-afternoon-_28-1-1024x683.jpg?X-Amz-Expires=86400&X-Amz-Date=20210420T164224Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAI7VTIL5G2JOQOLMA%2F20210420%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=b18f957dc2825bf537d668d10ef7fca8d8827cfa8e38d6019f7a69ec4ce577c1"
                  }
               },
               "image_processing": false,
               "label": "",
               "order": 0,
               "property_id": 100030000171,
               "created_at": "2020-03-05T16:55:26.899Z",
               "updated_at": "2020-03-05T16:55:33.172Z",
               "height": 683,
               "width": 1024,
               "organization_id": 3
            },
            "search_type": "dated",
            "slug": "the-pointe-resort",
            "can_fit_guests": true,
            "instant_booking": true,
            "review_count": 0,
            "review_average": null,
            "bookable_nightly_price_before_promotion": 0
         }
      ],
      "min_price": 10,
      "max_price": 999,
      "total_pages": 1,
      "total_properties": 1,
      "max_bedrooms": 4,
      "max_baths": 3.0,
      "max_guests": 6
   }
```

This endpoint retrieves all reviews connected to your organization.

### HTTP Request

`GET /search`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (required) | Maximum number of reviews to return, up to 100. Default is 20.
_booking_range (required) | A stringified json object of the booking range days.
_brand_id (required) | The unique ID of the Direct brand.
_amenities (optional) | A stringified json object of amenities to filter by.
_num_bathrooms (optional) | Filter by listings with a minimum number of bathrooms.
_num_bedrooms (optional) | Filter by listings with a minimum number of bedrooms.
_num_guests (optional) | Filter by listings with a minimum number of guests.
_page (optional) | Set the page of results returned.

# Statements

## Get All Statements

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/statements"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
      "statements": [
        {
            "id": 100030003979,
            "document_id": null,
            "name": "Statement for Dia Osinski: 02/01/20 - 02/29/20",
            "end_balance_cents": 597850,
            "start_balance_cents": 0,
            "start_date": "2020-02-01",
            "end_date": "2020-02-29",
            "processed_at": "2020-03-06T22:54:33.757Z",
            "payee_type": "Employee",
            "payee_id": 100030002763,
            "optional_id": "123",
            "optional_note": "123",
            "current_balance_cents": -1432288,
            "visibility_status": "visible",
            "payee_role": "property_contact",
            "deferred_balance": 0
        },
        {
            "id": 100030003980,
            "document_id": null,
            "name": "Statement for Prince Moore: 02/01/20 - 02/29/20",
            "end_balance_cents": -16563,
            "start_balance_cents": 0,
            "start_date": "2020-02-01",
            "end_date": "2020-02-29",
            "processed_at": null,
            "payee_type": "Employee",
            "payee_id": 100030002764,
            "optional_id": null,
            "optional_note": null,
            "current_balance_cents": -16563,
            "visibility_status": "visible",
            "payee_role": "property_contact",
            "deferred_balance": 0
        }
      ],
      "total_count": 2
   }
```

This endpoint retrieves all statements connected to your organization.

### HTTP Request

`GET /statements`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (optional) | Maximum number of statements to return, up to 100. Default is 20.
_offset (optional) | Number of statements to skip over, where the ordering is consistent but unspecified.

## Get a Specific Statement

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/statements/<ID>"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
      "id": 100030003979,
      "document_id": null,
      "name": "Statement for Dia Osinski: 02/01/20 - 02/29/20",
      "end_balance_cents": 597850,
      "start_balance_cents": 0,
      "start_date": "2020-02-01",
      "end_date": "2020-02-29",
      "processed_at": "2020-03-06T22:54:33.757Z",
      "payee_type": "Employee",
      "payee_id": 100030002763,
      "optional_id": "123",
      "optional_note": "123",
      "current_balance_cents": -1432288,
      "visibility_status": "visible",
      "payee_role": "property_contact",
      "deferred_balance": 0,
      "payouts": [
         {
            "unit_name": "Full Property: Francisco Villa - ",
            "payout_id": 100030032337,
            "booking_code": "5ZJUGQFLIEEPDJ0R",
            "guest_name": "Benton Schmitt",
            "nights": 10,
            "gross_revenue": 2807.66,
            "mgmt_fee": 561.53,
            "deductions": 0.0,
            "adjustments": 0.0,
            "net_to_owner": 2246.13
         },
         {
            "unit_name": "Full Property: Casa Barbara - ",
            "payout_id": 100030032329,
            "booking_code": "VSHWQ88X1HEGT1SS",
            "guest_name": "Wiley Frami I",
            "nights": 5,
            "gross_revenue": 5097.5,
            "mgmt_fee": 1019.5,
            "deductions": 0.0,
            "adjustments": 0.0,
            "net_to_owner": 4078.0
         }
      ],
      "payouts_subtotal": 632413,
      "unit_expenses": [
         {
            "id": 100030000052,
            "unit_name": "Casa Barbara",
            "dashboard_url": "/dashboard/blackrock-beach-properties/properties/100030000047",
            "gross_report_totals": 12037,
            "work_reports": [
               {
                  "id": 100030002342,
                  "service_date": "2020-02-07T00:00:00.000Z",
                  "invoice": null,
                  "total_cents": 6616,
                  "description": "Yardwork",
                  "vendor_name": "Armando Connelly III",
                  "deductions": [
                     {
                        "id": 100030002484,
                        "amount_cents": 6616,
                        "note": "Yardwork",
                        "reason": "exceeded_scope",
                        "deduction_type": null,
                        "deductable_type": "WorkReport",
                        "deductable_id": 100030002342,
                        "employee_id": 100030002763,
                        "created_at": "2020-02-24T18:10:14.239Z",
                        "updated_at": "2020-02-24T18:10:14.239Z",
                        "organization_id": 3
                     }
                  ]
               },
               {
                  "id": 100030002399,
                  "service_date": "2020-02-24T00:00:00.000Z",
                  "invoice": null,
                  "total_cents": 5421,
                  "description": "Bought new door knobs",
                  "vendor_name": "Gerard Maggio IV",
                  "deductions": [
                     {
                        "id": 100030002538,
                        "amount_cents": 5421,
                        "note": "Bought new door knobs",
                        "reason": "purchase_required",
                        "deduction_type": null,
                        "deductable_type": "WorkReport",
                        "deductable_id": 100030002399,
                        "employee_id": 100030002763,
                        "created_at": "2020-02-24T18:10:17.080Z",
                        "updated_at": "2020-02-24T18:10:17.080Z",
                        "organization_id": 3
                     }
                  ]
               }
            ]
         },
         {
            "id": 100030000164,
            "unit_name": "Francisco Villa",
            "dashboard_url": "/dashboard/blackrock-beach-properties/properties/100030000157",
            "gross_report_totals": 22526,
            "work_reports": [
               {
                  "id": 100030002413,
                  "service_date": "2020-02-24T00:00:00.000Z",
                  "invoice": null,
                  "total_cents": 12237,
                  "description": "Fixed pool heater",
                  "vendor_name": "Gerard Maggio IV",
                  "deductions": [
                     {
                        "id": 100030002552,
                        "amount_cents": 12237,
                        "note": "Fixed pool heater",
                        "reason": "purchase_required",
                        "deduction_type": null,
                        "deductable_type": "WorkReport",
                        "deductable_id": 100030002413,
                        "employee_id": 100030002763,
                        "created_at": "2020-02-24T18:10:17.826Z",
                        "updated_at": "2020-02-24T18:10:17.826Z",
                        "organization_id": 3
                     },
                     {
                        "id": 100030002653,
                        "amount_cents": 0,
                        "note": "<p>This is the adjustment notes</p>\n",
                        "reason": null,
                        "deduction_type": null,
                        "deductable_type": "WorkReport",
                        "deductable_id": 100030002413,
                        "employee_id": 100030002763,
                        "created_at": "2020-03-06T22:53:58.032Z",
                        "updated_at": "2020-03-06T22:53:58.032Z",
                        "organization_id": 3
                     }
                  ]
               },
               {
                  "id": 100030002315,
                  "service_date": "2020-02-01T11:00:00.000Z",
                  "invoice": null,
                  "total_cents": 10289,
                  "description": "Replaced door knobs",
                  "vendor_name": "Fixit Team",
                  "deductions": [
                     {
                        "id": 100030002463,
                        "amount_cents": 10289,
                        "note": "Replaced door knobs",
                        "reason": "purchase_required",
                        "deduction_type": null,
                        "deductable_type": "WorkReport",
                        "deductable_id": 100030002315,
                        "employee_id": 100030002763,
                        "created_at": "2020-02-24T18:10:13.068Z",
                        "updated_at": "2020-02-24T18:10:13.068Z",
                        "organization_id": 3
                     }
                  ]
               }
            ]
         }
      ],
      "expenses_subtotal": 345.63
   }
```

This endpoint retrieves a specific statement.

### HTTP Request

`GET /statements/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the statement to retrieve

# Transactions
## Get All Transactions

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/transactions"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   {
    "transactions": [
        {
            "post_date": "2020-07-31",
            "je_id": "JE-3AE425",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Cleaning Fee - City Tax",
            "amount": 19.999
        },
        {
            "post_date": "2020-07-31",
            "je_id": "JE-3AE425",
            "id": 100030031640,
            "general_ledger_account_number": 2308,
            "account_name": "City Tax",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Cleaning Fee - City Tax",
            "amount": 19.999
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-0E90AD",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Damage Waiver - City Tax",
            "amount": 9.9
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-0E90AD",
            "id": 100030031640,
            "general_ledger_account_number": 2308,
            "account_name": "City Tax",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Damage Waiver - City Tax",
            "amount": 9.9
        },
        {
            "post_date": "2020-07-29",
            "je_id": "JE-08B396",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Room Rate - City Tax",
            "amount": 187.615
        },
        {
            "post_date": "2020-07-29",
            "je_id": "JE-08B396",
            "id": 100030031640,
            "general_ledger_account_number": 2308,
            "account_name": "City Tax",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Room Rate - City Tax",
            "amount": 187.615
        },
        {
            "post_date": "2020-07-31",
            "je_id": "JE-7B0435",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Cleaning Fee - Sales Tax",
            "amount": 9.9995
        },
        {
            "post_date": "2020-07-31",
            "je_id": "JE-7B0435",
            "id": 100030031640,
            "general_ledger_account_number": 2306,
            "account_name": "Sales Tax",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Cleaning Fee - Sales Tax",
            "amount": 9.9995
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-E81844",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Damage Waiver - Sales Tax",
            "amount": 4.95
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-E81844",
            "id": 100030031640,
            "general_ledger_account_number": 2306,
            "account_name": "Sales Tax",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Damage Waiver - Sales Tax",
            "amount": 4.95
        },
        {
            "post_date": "2020-07-29",
            "je_id": "JE-4D1B2D",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Room Rate - Sales Tax",
            "amount": 93.8075
        },
        {
            "post_date": "2020-07-29",
            "je_id": "JE-4D1B2D",
            "id": 100030031640,
            "general_ledger_account_number": 2306,
            "account_name": "Sales Tax",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Room Rate - Sales Tax",
            "amount": 93.8075
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-554848",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Management Fee",
            "amount": 23.88
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-554848",
            "id": 100030031640,
            "general_ledger_account_number": 2115,
            "account_name": "Miscellaneous Fees/Charges - Guests",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Management Fee",
            "amount": 23.88
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-554847",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Processing Fee",
            "amount": 77.61
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-554847",
            "id": 100030031640,
            "general_ledger_account_number": 2117,
            "account_name": "Payment Processing Fees Paid",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Processing Fee",
            "amount": 77.61
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-554846",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Damage Waiver",
            "amount": 99.0
        },
        {
            "post_date": "2020-07-01",
            "je_id": "JE-554846",
            "id": 100030031640,
            "general_ledger_account_number": 2108,
            "account_name": "Damage Waiver Fees - Guests",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Damage Waiver",
            "amount": 99.0
        },
        {
            "post_date": "2020-07-31",
            "je_id": "JE-554845",
            "id": 100030031640,
            "general_ledger_account_number": 2002,
            "account_name": "Advance Reservations Deposits",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Cleaning Fee",
            "amount": 199.99
        },
        {
            "post_date": "2020-07-31",
            "je_id": "JE-554845",
            "id": 100030031640,
            "general_ledger_account_number": 2102,
            "account_name": "Amenity Fees - Guests",
            "unit_id": 100030000004,
            "portfolio": null,
            "subportfolio": "Hammock Beach",
            "unit_group": "Lodge: Three Bedroom Oceanview",
            "type": "Trust",
            "description": "Cleaning Fee",
            "amount": 199.99
        }
    ],
    "total_count": 75690
}
```

This endpoint retrieves all transactions connected to your organization.

### HTTP Request

`GET /transactions`

### URL Parameters

Parameter | Description
--------- | -----------
_limit (optional) | Maximum number of transactions to return, up to 100. Default is 20.
_offset (optional) | Number of transactions to skip over, where the ordering is consistent but unspecified.


# Units

## Get Promotions

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/properties/<P_ID>/units/<U_ID>/promotions"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   [
      {
         "id": 100030000045,
         "special_type": "percent",
         "amount": 10,
         "req_nights": 2,
         "travel_date_start": "2020-05-01",
         "travel_end_date": "2020-05-31",
         "promo_start_date": "2020-03-26",
         "promo_end_date": "2020-04-30",
         "days_of_week": null,
         "code_req": null,
         "coupon_code": null,
         "name": "winter special",
         "internal_name": "winter",
         "distro_list": null,
         "portfolio_id": 100030000018,
         "subportfolio_id": null,
         "created_at": "2020-03-26T15:09:32.313Z",
         "updated_at": "2020-03-26T15:09:32.313Z",
         "active": true,
         "organization_id": 3
      },
      { ... }
   ]
```

This endpoint retrieves a particular unit's promotions.

### HTTP Request

`GET /properties/<P_ID>/units/<U_ID>/promotions`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

## Get Rates

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/properties/<P_ID>/units/<U_ID>/rates"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
{
   "currency":"USD",
   "updated_at":"2018-12-11T23:56:43.268Z",
   "default_nightly_weekend":99.0,
   "default_nightly_weekday":99.0,
   "tax_rate":10.42,
   "discounts":[],
   "fees":[
      {
         "id":322,
         "name":"Processing Fee",
         "calculation_type":"percent",
         "calculation_amount":2.0,
         "taxable":false,
         "is_addon":"false"
      },
      {
         "id":49,
         "name":"Cleaning Fee",
         "calculation_type":"flat",
         "calculation_amount":100.0,
         "taxable":true,
         "is_addon":"false"
      }
   ],
   "security_deposit":[],
   "nightlyOverrides":[
      {
         "amount":219.0,
         "nights":[
            {
               "min":"2019-01-02",
               "max":"2019-01-03"
            }
         ]
      }
   ],
   "paymentSchedule":[
      {
         "days":null,
         "dueType":"AT_BOOKING",
         "amount":50,
         "type":"percent"
      },
      {
         "days": 7
         "dueType":"BEFORE_CHECKIN",
         "amount":null,
         "type":"remainder"
      }
   ]
}
```

This endpoint retrieves a particular unit's rates.

### HTTP Request

`GET /properties/<P_ID>/units/<U_ID>/rates`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

<aside class="notice">
  The <code>nightlyOverrides</code> block returns price variants for ranges of dates. Each item in the response contains an "amount" and "nights", which is an array of date ranges to which the amount should apply.
</aside>

## Get Reviews

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/properties/<P_ID>/units/<U_ID>/reviews"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
   [
      {
         "id": 100030000012,
         "unit_id": 100030000053,
         "booking_id": 100030031551,
         "title": "Great luxury property for families ",
         "body": "<p>Testing the review. Great location! Super clean&nbsp;</p>\n",
         "name": "Lauren A Flaugher",
         "check_in_date": "2020-05-24T00:00:00.000Z",
         "status": "published",
         "rating": 5,
         "created_at": "2020-05-22T19:10:21.967Z",
         "updated_at": "2020-05-22T19:18:02.117Z",
         "reviewed_date": "2020-05-22T19:10:21.965Z",
         "check_out_date": "2020-05-31T00:00:00.000Z",
         "where_from": null,
         "organization_id": 3,
         "customer_id": null
      },
      { ... }
   ]
```

This endpoint retrieves a particular unit's reviews.

### HTTP Request

`GET /properties/<P_ID>/units/<U_ID>/reviews`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

## Get Availability

```shell
curl "https://staging.getdirect.io/api/public/<ORG_ID>/properties/<P_ID>/units/<U_ID>/availability"
  -H "Authorization: Token your_api_key"
  -H "Accept: application/vnd.direct.v1"
```

> The above command returns JSON structured like this:

```json
{
   "availabilityDefault":"Y",
   "stayIncrementDefault":"D",
   "changeOverDefault":"C",
   "availableUnitCountDefault":1,
   "updated_at":"2018-12-11T23:56:42.917Z",
   "default_stay_min":2,
   "default_stay_max":30,
   "default_prior_notify_min":1,
   "dateRange":{
      "beginDate":"2019-01-02",
      "endDate":"2022-01-01"
   },
   "availability":"YN...",
   "changeOver":"CC...",
   "maxStay":"30,30,...",
   "minPriorNotify":"1,1,...",
   "minStay":"5,5,...",
   "stayIncrement":"DD..."
}
```

This endpoint retrieves a particular unit's availability.

### HTTP Request

`GET /properties/<P_ID>/units/<U_ID>/availability`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

<aside class="notice">
  The response format for all non-default values is a string composed of each date's value in the provided range. For example, <code>availability</code> returns "YN..." where "Y" corresponds to the first date, "N" the second date, and so on.
</aside>

### Availability Response Values

Key | Values
--- | ---
availability | Y (available) or N (not available)
changeOver | C (any), I (check in), O (check out), or X (none)
stayIncrement | D (day) or W (week)

## Create a Quote

```shell
curl "http://www.lvh.me:5100/api/public/990/properties/92/units/92/quotes"
-d '{"check_in": "2019-02-01", "check_out": "2019-02-05", "adults": 1, "children": 0, "pets": 0}'
-H "Authorization: Token test_api_key"
-H "Accept: application/vnd.direct.v1"
-H "Content-Type: application/json"
-X POST
```

> The above command returns JSON structured like this:

```json
{
   "orderItems":[
      {
         "feeType":"RENTAL",
         "name":"Rent",
         "preTaxAmount":892.0,
         "totalAmount":1001.51,
         "isAddOn":null
      },
      {
         "feeType":"MISC",
         "name":"Non-Refundable Damage Waiver Fee",
         "preTaxAmount":59.0,
         "totalAmount":59.0,
         "isAddOn":"false"
      },
      {
         "feeType":"MISC",
         "name":"Processing Fee",
         "preTaxAmount":17.84,
         "totalAmount":17.84,
         "isAddOn":"false"
      },
      {
         "feeType":"MISC",
         "name":"Cleaning Fee",
         "preTaxAmount":100.0,
         "totalAmount":100.0,
         "isAddOn":"false"
      },
      {
         "feeType":"MISC",
         "name":"Resort Fee",
         "preTaxAmount":20.0,
         "totalAmount":20.0,
         "isAddOn":"false"
      }
   ],
   "paymentSchedule":[
      {
         "amount":1198.35,
         "dueDate":"2019-01-02"
      }
   ],
   "rentalAgreement":"<url to PDF>"
}
```

This endpoint retrieves a quote for the specified unit given check in date, check out date, number of adults, number of children (optional) and number of pets (optional).

### HTTP Request

`POST /properties/<P_ID>/units/<U_ID>/quotes`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

### Request Parameters

Parameter | Description
--------- | -----------
check_in | The check in date ("YYYY-MM-DD")
check_out | The check out date ("YYYY-MM-DD")
adults | The number of adult guests
children | The number of child guests (optional, default to 0)
pets | The number of pets (optional, default to 0)

## Update Pricing

```shell
curl "https://staging.getdirect.io/api/public/990/properties/92/units/92/pricing"
-d '{"pricing_array":
      [
         {"date":"2019-04-03", "recommended_price":"440", "reason":"High demand"},
         {"date":"2019-04-04", "recommended_price":"244", "reason":"Low demand"}
      ]
   }'
-H "Authorization: Token test_api_key"
-H "Accept: application/vnd.direct.v1"
-H "Content-Type: application/json"
-X POST
```

> The above command returns JSON structured like this:

```json
{
   "status": "Success"
}
```

This endpoint updates the nightly price for the specified unit given and dates found in the json.

### HTTP Request

`POST /properties/<P_ID>/units/<U_ID>/pricing`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

### Request Parameters

Parameter | Description
--------- | -----------
pricing_array | An array of pricing objects to process
date | The date you wish to update ("YYYY-MM-DD")
recommended_price | The price to set on the specified date
reason | The reason for the updated price

## Update Minimum Night Stay

```shell
curl "https://staging.getdirect.io/api/public/990/properties/92/units/92/stay-length"
-d '{"availability_array":
      [
         {"date":"2019-04-03", "min_nights":"5", "reason":"High demand"},
         {"date":"2019-04-04", "min_nights":"3", "reason":"Low demand"}
      ]
   }'
-H "Authorization: Token test_api_key"
-H "Accept: application/vnd.direct.v1"
-H "Content-Type: application/json"
-X POST
```

> The above command returns JSON structured like this:

```json
{
   "status": "Success"
}
```

This endpoint updates the minimum night stay for the speceified unit given and dates found in the json.

### HTTP Request

`POST /properties/<P_ID>/units/<U_ID>/stay-length`

### URL Parameters

Parameter | Description
--------- | -----------
P_ID | The ID of the property to retrieve
U_ID | The ID of the unit to retrieve

### Request Parameters

Parameter | Description
--------- | -----------
availability_array | An array of availability objects to process
date | The date you wish to update ("YYYY-MM-DD")
min_nights | The minimum nights to set on the specified date
reason | The reason for the updated