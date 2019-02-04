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

Direct uses API keys to allow access to the API. You can register a new Direct API key by emailing us at [scott@getdirect.io](mailto:scott@getdirect.io?subject=Developer%20Key%20Request).

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
   ]
}
```

This endpoint retrieves all properties connected to your organization.

### HTTP Request

`GET /properties`

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
         "dueType":"AT_BOOKING",
         "amount":50,
         "type":"percent"
      },
      {
         "dueType":"AT_CHECKIN",
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

## Get a Quote

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

# Reservations

## Get All reservations

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
            "updated_at": "2019-01-25T01:04:39.744Z"
        },
        {
            "id": 1811,
            "booking_code": "EQRMH4-L6QR1EALF",
            "updated_at": "2019-01-25T01:03:14.583Z"
        }
      ]
   }
```

This endpoint retrieves all reservations connected to your organization.

### HTTP Request

`GET /reservations`

## Get a Specific Reservation

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
    "customer": {
        "name": "christopher zepf",
        "email": "ndirish1@gmail.com",
        "telephone": null
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

