# Chapter 1. Overview

This document is intended for any transfer Partners considering connecting Carzenplus as a transfer service provider, The current document gives the partner platform all the needed information to kick-off the integration of Carzenplus Transfers Connectors.
Carzenplus airport transfer APIs are designed using a RESTful architecture, which relies on predictable, resource-oriented URLs, and HTTP response codes to indicate errors. It uses built-in HTTP features, like HTTP authentication and HTTP verbs, supported by most HTTP clients.
Please also note that our current API version is 1, and all endpoints described in this document will begin with /v1/.
For online tests, please visit This Url. If you need an AccessKey ID, or AccessKey secret, please contact us.

## 1.1 Version information
> Version : v1

## 1.2. Contact information

> Contact : Carzenplus
> Contact Email : it.group@carzenplus.com

## 1.3 URI scheme
- Host : `api.carzenplus.com`
- BasePath : `/v1`
- Schemes : `HTTPS`

# Chapter 2. Security

## 2.1 AccessKey Pair


An AccessKey pair (AccessKey ID and AccessKey secret) is a set of security credentials for you to access the API of Carzenplus. The owner of an AccessKey pair has full access to the current account. Keep your AccessKey pair confidential.

```
signature = MD5 (AccessKey ID + AccessKey secret)
```

# Chapter 3. Paths

## 3.1. Query transfer products

```
POST /transfer/query
```

### 3.1.1. Description

The Query resource is the one used to search for available transfer solutions and to get the details and prices for each solution.

### 3.1.2. Parameters


| Type  | Name                     | Description   | Schema                                     |
|-------|--------------------------|---------------|--------------------------------------------|
| Body  | **model** <br> required  | Query model   | [TransferQueryInfo](#41transferqueryinfo)  |


### 3.1.3. Responses


| Name            | Description                                    | Schema                                 |
|-----------------|------------------------------------------------|----------------------------------------|
| **code**        | 200 is success, others number is error flags   | integer(int32)                         |
| **success**     | true or false                                  | boolean                                |
| **request_id**  | Request unique id                              | string                                 |
| **message**     | Message                                        | string                                 |
| **data**        | Response data,                                 | [TransferQueryVO](#417transferqueryvo) |
| **server_time** | Unix time                                      | integer(int64)                         |

## 3.1.4. Consumes

-  `application/json`
-  `text/json`

## 3.1.5. Produces

-  `application/json`
-  `text/json`

## 3.1.6. Example HTTP request

`Request body`

``` JSON
{
    "authentication":{
        "signature":"2b277d2ed7a72af8c4ef840e32c0260d",
        "access_key":"dylGLg"
    },
    "pick_up":{
        "name":"Xiaoshan Airport",
        "latitude":30.236189,
        "longitude":120.438842,
        "address":"Hangzhou International Airport (HGH)",
        "google_place_id":"ChIJeZr5cP6TTDQROhcfDB7aCh4"
    },
    "drop_off":{
        "name":"Zhejiang University",
        "latitude":30.308888,
        "longitude":120.086499,
        "address":"No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal",
        "google_place_id":"ChIJc9VHk-ViSzQRoIFvkzZfGsc"
    },
    "passenger_info":{
        "adults":1,
        "children":1,
        "infants":0
    },
    "luggage_info":{
        "medium":1,
        "small":1
    },
    "vehicle_info":{
        "vehicle_name":"MPV 4pax"
    },
    "duration_in_seconds":"2998",
    "distance_in_meters":"47310",
    "booking_time":1657173773,
    "flight_code":"CA1234",
    "transfer_type":"Airport2Point",
    "currency":"CNY"
}
```





### 3.1.7. Example HTTP response

`Response 200  code 200`

``` JSON
{
    "code":200,
    "success":true,
    "request_id":"25618f7199074c29",
    "message":"Success",
    "data":{
        "price":757.12,
        "currency":"CNY",
        "transfer_ticket_info":{
            "ticket":"VJTs8MZEcLzxwCOAX8QvhQpQ3BwCIUcL",
            "expire_time":1657090172
        },
        "transfer_type":"Airport2Point",
        "transfer_services":[
            {
                "code":"BabySeat",
                "name":"Baby Seat",
                "price":134,
                "description":"description",
                "max_booking_count":10
            }
        ],
        "transfer_vehicle": {
            "description": "",
            "vehicle_name": "Q7 or similar",
            "brand_name": "Audi or similar",
            "vehicle_id": 2,
            "max_passenger_quantity": 5,
            "max_luggage_quantity": 5,
            "vehicle_icon": "https://misc-cn.carzenplus.com/car-model/2.png"
        },
        "provider":{
            "name":"Carzenplus",
            "logo_url":"logo_url"
        },
        "duration_in_seconds":3000,
        "distance_in_meters":47318
    },
    "server_time":1657088372
}


```

`Response 200 code 201`

``` JSON
{
    "code": 201,
    "success": false,
    "message": "transfer_type is null",
    "request_id": "cc2c661180c04ae3",
    "server_time": 1657096186
}
```

## 3.2. Make a Booking

```
POST /transfer/create
```

### 3.2.1. Description

The Booking resource is used to reserve a Transfer and to get from the provider a confirmation
number for the reservation.

Make a booking based on submitted criteria.

Before making a reservation, you must query first.

### 3.2.2. Parameters

| Type   | Name                      | Description   | Schema                                          |
|--------|---------------------------|---------------|-------------------------------------------------|
| Body   | **model** <br> required   | Query model   | [BookingCreateRequest](#48bookingcreaterequest) |

### 3.2.3. Responses


| Name            | Description                                    | Schema                     |
|-----------------|------------------------------------------------|----------------------------|
| **code**        | 200 is success, others number is error flags   | integer(int32)             |
| **success**     | true or false                                  | boolean                    |
| **request_id**  | Request unique id                              | string                     |
| **message**     | Message                                        | string                     |
| **data**        | Response data,                                 | [BookingVO](#412bookingvo) |
| **server_time** | Unix time                                      | integer(int64)             |

### 3.2.4. Consumes

- `application/json`
- `text/json`

### 3.2.5. Produces

- `application/json`
- `text/json`

### 3.2.6. Example HTTP request

`Request body`


``` JSON

{
    "remark":"remark",
    "authentication":{
        "signature":"2b277d2ed7a72af8c4ef840e32c0260d",
        "access_key":"dylGLg"
    },
    "transfer_ticket":"VJTs8MZEcLzxwCOAX8QvhQpQ3BwCIUcL",
    "flight_code":"CA1234",
    "transfer_type":"Airport2Point",
    "currency":"CNY",
    "partner_order_sn":"D1344067",
    "pick_up":{
        "name":"Xiaoshan Airport",
        "latitude":30.236189,
        "longitude":120.438842,
        "address":"Hangzhou International Airport (HGH)",
        "google_place_id":"ChIJeZr5cP6TTDQROhcfDB7aCh4"
    },
    "drop_off":{
        "name":"Zhejiang University",
        "latitude":30.308888,
        "longitude":120.086499,
        "address":"No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal",
        "google_place_id":"ChIJc9VHk-ViSzQRoIFvkzZfGsc"
    },
    "passenger_info":{
        "adults":1,
        "children":1,
        "infants":0
    },
    "passenger_contact_info":{
        "passenger_name":"Zhang San",
        "passenger_phone":"+8613888888888",
        "passenger_email":"xx@gmail.com",
        "passenger_whats_app_account": "",
        "passenger_wechat_account": ""
    },
    "luggage_info":{
        "medium":1,
        "small":1
    },
    "vehicle_info":{
        "vehicle_name":"MPV 4pax"
    },
    "transfer_services":[
        {
            "quantity":1,
            "code":"BabySeat",
            "price":100.01,
            "total_price":100.01
        }
    ],
    "price_detail":{
        "transfer_fee":99,
        "service_fee":100.01,
        "total_fee":199.01
    },
    "duration_in_seconds":"2998",
    "distance_in_meters":"47310",
    "booking_time":1657193584
}

```

### 3.2.7. Example HTTP response

`Response 200` `code 200`

``` JSON

{
    "code": 200,
    "success": true,
    "message": "Success",
    "data": {
        "order_status": "WAIT_DISPATCH",
        "order_sn": "SD2022070708342",
        "partner_order_sn": "D1344067",
        "flight_code": "CA1234",
        "transfer_type": "Airport2Point",
        "currency": "CNY",
        "remark": "remark",
        "pick_up": {
            "name": "Xiaoshan Airport",
            "latitude": 30.236189,
            "longitude": 120.438842,
            "address": "Hangzhou International Airport (HGH)",
            "google_place_id": null
        },
        "drop_off": {
            "name": "Zhejiang University",
            "latitude": 30.308888,
            "longitude": 120.086499,
            "address": "No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal",
            "google_place_id": null
        },
        "passenger_info": {
            "adults": 1,
            "children": 1,
            "infants": 0
        },
        "passenger_contact_info": {
            "passenger_name": "Zhang San",
            "passenger_phone": "+8613888888888",
            "passenger_email": "",
            "passenger_whats_app_account": "",
            "passenger_wechat_account": ""
        },
        "luggage_info": {
            "medium": 1,
            "small": 1
        },
        "transfer_services": [
            {
                "service_code": "BabySeat",
                "service_name": "Baby Seat",
                "price": 100.01,
                "quantity": 1
            }
        ],
        "transfer_vehicle": {
            "color": null,
            "plate_number": null,
            "brand_name": "Audi or similar",
            "model": "Q7 or similar"
        },
        "provider": {
            "name": "Carzenplus",
            "logo_url": null
        },
        "price_detail": {
            "transfer_fee": 99.00,
            "service_fee": 100.01,
            "total_fee": 199.01
        },
        "driver_info": null
    },
    "request_id": "bb1f196ca78f4dd8",
    "server_time": 1657194049
}

```

`Response 200` `code 201`

``` JSON
{
    "code": 201,
    "success": false,
    "message": "Transfer ticket is expired",
    "request_id": "b47f25d1209b4e14",
    "server_time": 1657193743
}
```

`Response 200` `code 201`

``` JSON
{
    "code": 201,
    "success": false,
    "message": "Transfer already exists.",
    "request_id": "baae7f3059f64307",
    "server_time": 1657194291
}

```

## 3.3 Cancel a transfer order

```
POST /transfer/cancel
```

### 3.3.1. Description

The Cancellation resource is used to cancel a Transfer reservation and to get from Provider a cancel confirmation.

### 3.3.2. Parameters

| Type   | Name                      | Description     | Schema                                        |
|--------|---------------------------|-----------------|-----------------------------------------------|
| Body   | **model** <br> required   | Cancel model    | [BookingCancelInfo](#48bookingcreaterequest)  |

### 3.3.3. Responses


| Name            | Description                                   | Schema           |
|-----------------|-----------------------------------------------|------------------|
| **code**        | 200 is success, others number is error flags  | integer(int32)   |
| **success**     | true or false                                 | boolean          |
| **request_id**  | Request unique id                             | string           |
| **message**     | Message                                       | string           |
| **data**        | Void,                                         | none             |
| **server_time** | Unix time                                     | integer(int64)   |

### 3.3.4. Consumes

- `application/json`
- `text/json`

### 3.3.5. Produces

- `application/json`
- `text/json`

### 3.3.6. Example HTTP request

`Request body`

``` JSON
{
    "authentication":{
        "signature":"2b277d2ed7a72af8c4ef840e32c0260d",
        "access_key":"dylGLg"
    },
    "order_sn":"SD2022070708342",
    "reason":"Cancel Reason"
}
```

### 3.3.7. Example HTTP response

`Response 200` `code 200`

``` JSON
{
    "code": 200,
    "success": true,
    "message": "Success",
    "request_id": "d269af6e0f924628",
    "server_time": 1657242643
}
```

`Response 200` `code 201`

``` JSON
{
    "code": 201,
    "success": false,
    "message": "Booking not allow cancel.",
    "request_id": "4592f48413f64e97",
    "server_time": 1657242783
}
```

## 3.4 Get a transfer order details by order number

```
POST /transfer/detail
```

### 3.4.1. Description

The Detail resource is used to view a Transfer order details.

### 3.4.2. Parameters

| Type   | Name                      | Description    | Schema                                      |
|--------|---------------------------|----------------|---------------------------------------------|
| Body   | **model** <br> required   | Detail model   | [BookingDetailInfo](#422-bookingdetailinfo) |

### 3.4.3. Responses


| Name            | Description                                    | Schema                     |
|-----------------|------------------------------------------------|----------------------------|
| **code**        | 200 is success, others number is error flags   | integer(int32)             |
| **success**     | true or false                                  | boolean                    |
| **request_id**  | Request unique id                              | string                     |
| **message**     | Message                                        | string                     |
| **data**        | Response data,                                 | [BookingVO](#412bookingvo) |
| **server_time** | Unix time                                      | integer(int64)             |

### 3.4.4. Consumes

- `application/json`
- `text/json`

### 3.4.5. Produces

- `application/json`
- `text/json`

### 3.4.6. Example HTTP request

`Request body`

``` JSON
{
    "authentication":{
        "signature":"2b277d2ed7a72af8c4ef840e32c0260d",
        "access_key":"dylGLg"
    },
    "order_sn":"SD2022070708342"
}
```

### 3.4.7. Example HTTP response

`Response 200 code 200`

``` JSON
{
    "code": 200,
    "success": true,
    "message": "Success",
    "data": {
        "order_status": "CANCELLED",
        "order_sn": "SD2022070708342",
        "partner_order_sn": "D1344067",
        "flight_code": "CA1234",
        "transfer_type": "Airport2Point",
        "currency": "CNY",
        "remark": "remark",
        "pick_up": {
            "name": "Xiaoshan Airport",
            "latitude": 30.236189,
            "longitude": 120.438842,
            "address": "Hangzhou International Airport (HGH)",
            "google_place_id": null
        },
        "drop_off": {
            "name": "Zhejiang University",
            "latitude": 30.308888,
            "longitude": 120.086499,
            "address": "No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal",
            "google_place_id": null
        },
        "passenger_info": {
            "adults": 1,
            "children": 1,
            "infants": 0
        },
        "passenger_contact_info": {
            "passenger_name": "Zhang San",
            "passenger_phone": "+8613888888888",
            "passenger_email": "",
            "passenger_whats_app_account": "",
            "passenger_wechat_account": ""
        },
        "luggage_info": {
            "medium": 1,
            "small": 1
        },
        "transfer_services": [
            {
                "price": 100.01,
                "quantity": 1,
                "service_code": "BabySeat",
                "service_name": "Baby Seat"
            }
        ],
        "transfer_vehicle": {
            "color": null,
            "plate_number": null,
            "brand_name": "Audi or similar",
            "model": "Q7 or similar"
        },
        "provider": {
            "name": "Carzenplus ",
            "logo_url": null
        },
        "price_detail": {
            "transfer_fee": 99.00,
            "service_fee": 100.01,
            "total_fee": 199.01
        },
        "driver_info": null
    },
    "request_id": "3a940f658da44e60",
    "server_time": 1657244829
}

```

`Response 200 code 201`

``` JSON
{
    "code": 201,
    "success": false,
    "message": "Booking not found.",
    "request_id": "c5325fd4993647d2",
    "server_time": 1657244947
}
```


# Chapter 4. Definitions

## 4.1.TransferQueryInfo


| Name                                  | Description                                                      | Scheme                                                      |
|---------------------------------------|------------------------------------------------------------------|-------------------------------------------------------------|
| **authentication** <br> required      | Authentication parameter                                         | [TransferAuthenticationInfo](#42transferauthenticationinfo) |
| **pick_up** <br> required             | Starting point information (address , name, latitude, longitude) | [TransferPointInfo](#43transferpointinfo)                   |
| **drop_off** <br> required            | End point information (address , name, latitude, longitude)      | [TransferPointInfo](#43transferpointinfo)                   |
| **passenger_info** <br> required      | Number of passenger, include adults, children,infants            | [PassengerInfo](#44passengerinfo)                           |
| **luggage_info** <br> optional        | Requirements to luggage space to be supported by the vehicle     | [LuggageInfo](#45luggageinfo)                               |
| **vehicle_info** <br> required        | Platform model information, need to contact us to bind           | [TransferVehicleInfo](#46transfervehicleinfo)               |
| **duration_in_seconds** <br> required | The numeric duration, in seconds.                                | integer (int64)                                             |
| **distance_in_meters** <br> required  | The numeric distance, in meters.                                 | integer  (int64)                                            |
| **booking_time** <br> required        | The booking time. unix timestamp                                 | integer  (int64)                                            |
| **flight_code** <br> optional         | The numeric flight number.                                       | string                                                      |
| **transfer_type** <br> required       | The type of transfer.                                            | enum <br>Airport2Point <br> Point2Airport <br> Point2Point  |
| **currency** <br> required            | TheCurrency code in ISO 4217 format.                             | string                                                      |


## 4.2.TransferAuthenticationInfo


| Name                           | Description                           | Scheme   |
|--------------------------------|---------------------------------------|----------|
| **access_key** <br> required   | AccessKey ID                          | string   |
| **signature** <br> required    | MD5 (AccessKey ID + AccessKey secret) | string   |



## 4.3.TransferPointInfo

| Name                              | Description           | Scheme          |
|-----------------------------------|-----------------------|-----------------|
| **name** <br> required            | Point name            | string          |
| **google_place_id** <br> required | Google map placeId    | string          |
| **address** <br> required         | Point address details | string          |
| **latitude** <br> required        | Latitude              | number (double) |
| **longitude** <br> required       | Longitude             | number (double) |


## 4.4.PassengerInfo

| Name                       | Description       | Scheme           |
|----------------------------|-------------------|------------------|
| **adults** <br> required   | Adult Quantity    | integer(int32)   |
| **children** <br> optional | Children Quantity | integer(int32)   |
| **infants** <br> optional  | Infants Quantity  | integer(int32)   |

## 4.5.LuggageInfo

| Name                      | Description              | Scheme          |
|---------------------------|--------------------------|-----------------|
| **medium** <br> optional  | Medium Luggage Quantity  | integer(int32)  |
| **small** <br> optional   | Small Luggage Quantity   | integer(int32)  |

## 4.6.TransferVehicleInfo

| Name                           | Description                             | Scheme         |
|--------------------------------|-----------------------------------------|----------------|
| **vehicle_id** <br> optional   | Require vehicle ID and/or vehicle name  | integer(int32) |
| **vehicle_name** <br> optional | Require vehicle ID and/or vehicle name  | integer(int32) |

## 4.7.ResultModel


| Name            | Description                                    | Schema           |
|-----------------|------------------------------------------------|------------------|
| **code**        | 200 is success, others number is error flags   | integer(int32)   |
| **success**     | true or false                                  | boolean          |
| **request_id**  | Request unique id                              | string           |
| **message**     | Message                                        | string           |
| **data**        | Response data,                                 | <?>              |
| **server_time** | Unix time                                      | integer(int64)   |

## 4.8.BookingCreateRequest

| Name                                     | Description                                                             | Scheme                                                      |
|------------------------------------------|-------------------------------------------------------------------------|-------------------------------------------------------------|
| **authentication** <br> required         | Authentication parameter                                                | [TransferAuthenticationInfo](#42transferauthenticationinfo) |
| **transfer_ticket** <br> required        | `/transfer/query` > transfer_ticket_info > ticket                       | string                                                      |
| **flight_code** <br> optional            | The numeric flight number.                                              | string                                                      |
| **transfer_type** <br> required          | The type of transfer.                                                   | enum <br>Airport2Point <br> Point2Airport <br> Point2Point  |
| **currency** <br> required               | TheCurrency code in ISO 4217 format.                                    | string                                                      |
| **remark** <br> optional                 | Customer remark.                                                        | string                                                      |
| **partner_order_sn** <br> required       | Partner order number.                                                   | string                                                      |
| **pick_up** <br> required                | Starting point information (address , name, latitude, longitude)        | [TransferPointInfo](#43transferpointinfo)                   |
| **drop_off** <br> required               | End point information (address , name, latitude, longitude)             | [TransferPointInfo](#43transferpointinfo)                   |
| **passenger_info** <br> required         | Number of passenger, include adults, children,infants                   | [PassengerInfo](#44passengerinfo)                           |
| **luggage_info** <br> optional           | Requirements to luggage space to be supported by the vehicle            | [LuggageInfo](#45luggageinfo)                               |
| **passenger_contact_info** <br> required | Passengers’ information. Information about “main” passenger is required | [PassengerContactInfo](#49passengercontactinfo)             |
| **vehicle_info** <br> required           | Platform model information, need to contact us to bind                  | [TransferVehicleInfo](#46transfervehicleinfo)               |
| **transfer_services** <br> required      | Platform model information, need to contact us to bind                  | <[TransferServiceItem](#410transferserviceitem)> array      |
| **price_detail** <br> required           | Payment detail                                                          | [OrderPriceDetail](#411orderpricedetail)                    |
| **duration_in_seconds** <br> required    | The numeric duration, in seconds.                                       | integer (int32)                                             |
| **distance_in_meters** <br> required     | The numeric distance, in meters.                                        | integer  (int64)                                            |
| **booking_time** <br> required           | The booking time. unix timestamp                                        | integer  (int64)                                            |


## 4.9.PassengerContactInfo


| Name                                          | Description                | Schema  |
|-----------------------------------------------|----------------------------|---------|
| **passenger_name** <br> required              | Name of passenger          | string  |
| **passenger_phone** <br> required             | Mobile phone of passenger  | string  |
| **passenger_email** <br> optional             | Email address of passenger | string  |
| **passenger_whats_app_account** <br> optional | WhatsApp account of passenger | string  |
| **passenger_wechat_account** <br> optional    | Wechat account of passenger | string  |


## 4.10.TransferServiceItem

| Name                          | Description                           | Schema           |
|-------------------------------|---------------------------------------|------------------|
| **quantity** <br> required    | Number of equipement/goods requested  | integer (int32)  |
| **code** <br> required        | service code                          | string           |
| **price** <br> required       | price per unit                        | number (double)  |
| **total_price** <br> required | TotalPrice                            | number (double)  |


## 4.11.OrderPriceDetail

| Name                            | Description                          | Schema          |
|---------------------------------|--------------------------------------|-----------------|
| **transfer_fee** <br> required  | Base fee from Query Transfer Price   | number (double) |
| **service_fee** <br> required   | Additional Services Fee              | number (double) |
| **total_price** <br> required   | transfer_fee + service_fee           | number (double) |

## 4.12.BookingVO

| Name                                     | Description                                                             | Schema                                                                                                           |
|------------------------------------------|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| **order_status** <br> required           | OrderStatus                                                             | enum(<br>WAIT_CONFIRM <br>WAIT_DISPATCH<br>WAIT_ASSIGN<br>WAIT_SERVICE<br>SERVING<br>COMPLETED<br>CANCELLED<br>) |
| **order_sn** <br> required               | Order number of Carzenplus                                              | string                                                                                                           |
| **partner_order_sn** <br> required       | Partner order number.                                                   | string                                                                                                           |
| **flight_code** <br> required            | The flight number including airline code                                | string                                                                                                           |
| **transfer_type** <br> required          | The type of transfer.                                                   | enum <br>Airport2Point <br> Point2Airport <br> Point2Point                                                       |
| **currency** <br> required               | TheCurrency code in ISO 4217 format.                                    | string                                                                                                           |
| **remark** <br> required                 | Customer remark..                                                       | string                                                                                                           |
| **pick_up** <br> required                | Starting point information (address , name, latitude, longitude)        | [TransferPointInfo](#43transferpointinfo)                                                                        |
| **drop_off** <br> required               | End point information (address , name, latitude, longitude)             | [TransferPointInfo](#43transferpointinfo)                                                                        |
| **passenger_info** <br> required         | Number of passenger, include adults, children,infants                   | [PassengerInfo](#44passengerinfo)                                                                                |
| **luggage_info** <br> optional           | Requirements to luggage space to be supported by the vehicle            | [LuggageInfo](#45luggageinfo)                                                                                    |
| **passenger_contact_info** <br> required | Passengers’ information. Information about “main” passenger is required | [PassengerContactInfo](#49passengercontactinfo)                                                                  |
| **transfer_services** <br> optional      | Support service                                                         | <[BookingTransferServiceVO](#413bookingtransferservicevo)><br> arr                                               |
| **transfer_vehicle** <br> optional       | Vehicle info                                                            | [BookingVehicleVO](#414bookingvehiclevo)                                                                         |
| **provider** <br> optional               | Provider Info                                                           | [PlatformProviderVO](#415platformprovidervo)                                                                     |
| **price_detail** <br> required           | Payment detail                                                          | [BookingPriceDetailVO](#411orderpricedetail)                                                                     |
| **driver_info** <br> optional            | Driver information                                                      | [BookingDriverVO](#416bookingdrivervo)                                                                           |



## 4.13.BookingTransferServiceVO

| Name                            | Description     | Schema          |
|---------------------------------|-----------------|-----------------|
| **service_code** <br> optional  | service code    | string          |
| **service_name** <br> optional  | service names   | string          |
| **price** <br> optional         | price per unit  | number (double) |
| **quantity** <br> optional      | Quantity        | integer (int32) |

## 4.14.BookingVehicleVO

| Name                            | Description              | Schema  |
|---------------------------------|--------------------------|---------|
| **plate_number** <br> optional  | Vehicle plate number     | string  |
| **brand_name** <br> optional    | Vehicle brand. e.g. Audi | string  |
| **color** <br> optional         | Vehicle color            | string  |
| **model** <br> optional         | Vehicle model. e.g. A6   | string  |

## 4.15.PlatformProviderVO
| Name                       | Description       | Schema  |
|----------------------------|-------------------|---------|
| **name** <br> optional     | Provider name     | string  |
| **logo_url** <br> optional | Provider logo url | string  |

## 4.16.BookingDriverVO

| Name                       | Description               | Schema   |
|----------------------------|---------------------------|----------|
| **phone** <br> optional    | Driver’s phone number     | string   |
| **name** <br> optional     | Driver’s name             | string   |
| **wechat** <br> optional   | Driver’s Wechat.          | string   |
| **whatsapp** <br> optional | Driver’s Whatsapp etc.    | string   |

## 4.17.TransferQueryVO

| Name                                    | Description                       | Schema                                                     |
|-----------------------------------------|-----------------------------------|------------------------------------------------------------|
| **transfer_ticket_info** <br> required  | Book order ticket                 | [TransferTicket](#418transferticket)                       |
| **transfer_type** <br> required         | The type of transfer.             | enum <br>Airport2Point <br> Point2Airport <br> Point2Point |
| **price** <br> required                 | Itinerary price.                  | number (double)                                            |
| **currency** <br> required              | Currency code in ISO 4217 format. | string                                                     |
| **transfer_services** <br> required     | Transfer Services.                | [TransferServiceVO](#419transferservicevo)                 |
| **transfer_vehicle** <br> required      | Vehicle information               | [TransferServiceVO](#420transfervehiclevo)                 |
| **provider** <br> optional              | Provider Info                     | [PlatformProviderVO](#415platformprovidervo)               |
| **duration_in_seconds** <br> required   | The numeric duration, in seconds. | integer (int64)                                            |
| **distance_in_meters** <br> required    | The numeric distance, in meters.  | integer  (int64)                                           |


## 4.18.TransferTicket

| Name                          | Description                         | Schema          |
|-------------------------------|-------------------------------------|-----------------|
| **ticket** <br> required      | Book order ticket                   | string          |
| **expire_time** <br> optional | Ticket validity time, unix timespan | integer (int64) |

## 4.19.TransferServiceVO

| Name                                | Description          | Schema          |
|-------------------------------------|----------------------|-----------------|
| **service_code** <br> optional      | service code         | string          |
| **service_name** <br> optional      | service names        | string          |
| **price** <br> optional             | price per unit       | number (double) |
| **max_booking_count** <br> required | max book count       | integer (int32) |
| **description** <br> optional       | service descriptions | string          |

## 4.20.TransferVehicleVO

| Name                                     | Description                        | Schema          |
|------------------------------------------|------------------------------------|-----------------|
| **vehicle_name** <br> optional           | Vehicle model. e.g. A6             | string          |
| **brand_name** <br> optional             | Vehicle brand. e.g. Audi           | string          |
| **vehicle_id** <br> optional             | Vehicle ID                         | integer (int32) |
| **max_passenger_quantity** <br> required | Max seat count,without driver seat | integer (int32) |
| **max_luggage_quantity** <br> required   | Max luggage count                  | integer (int32) |
| **description** <br> optional            | Vehicle descriptions               | string          |
| **vehicle_icon** <br> optional           | Vehicle picture url                | string          |


## 4.21.BookingCancelInfo

| Name                              | Description                         | Schema                                                       |
|-----------------------------------|-------------------------------------|--------------------------------------------------------------|
| **authentication** <br> required  | Authentication parameter            | [TransferAuthenticationInfo](#42transferauthenticationinfo)  |
| **order_sn** <br> required        | Order number of Carzenplus          | string                                                       |
| **reason** <br> required          | Cancel reason <br> Length : 0 - 200 | string                                                       |

## 4.22 BookingDetailInfo

| Name                              | Description                | Schema                                                       |
|-----------------------------------|----------------------------|--------------------------------------------------------------|
| **authentication** <br> required  | Authentication parameter   | [TransferAuthenticationInfo](#42transferauthenticationinfo)  |
| **order_sn** <br> required        | Order number of Carzenplus | string                                                       |
