---
title: Direct API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:scott@getdirect.io?subject=Developer%20Key%20Request'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Direct API! You can use our API to access Direct API endpoints, including information on properties, units, rates, availability, and quotes in our database. You can view code examples in the dark area to the right.

The base URL for all endpoints in this doc is:

`https://app.getdirect.io/api/public/<ORG_ID>`

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

# Properties

## Get All Properties

```shell
curl "https://app.getdirect.io/api/public/<ORG_ID>/properties"
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
curl "https://app.getdirect.io/api/public/<ORG_ID>/properties/<ID>"
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
curl "https://app.getdirect.io/api/public/<ORG_ID>/reservations"
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
curl "https://app.getdirect.io/api/public/990/reservations"
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
curl "https://app.getdirect.io/api/public/<ORG_ID>/reservations/<ID>"
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
curl "https://app.getdirect.io/api/public/3/reservations/100030030467"
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

# Statements

## Get All Statements

```shell
curl "https://app.getdirect.io/api/public/<ORG_ID>/statements"
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
curl "https://app.getdirect.io/api/public/<ORG_ID>/statements/<ID>"
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

# Units

## Get Rates

```shell
curl "https://app.getdirect.io/api/public/<ORG_ID>/properties/<P_ID>/units/<U_ID>/rates"
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

## Get Availability

```shell
curl "https://app.getdirect.io/api/public/<ORG_ID>/properties/<P_ID>/units/<U_ID>/availability"
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
curl "https://app.getdirect.io/api/public/990/properties/92/units/92/pricing"
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
curl "https://app.getdirect.io/api/public/990/properties/92/units/92/stay-length"
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