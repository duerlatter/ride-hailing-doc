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
- Host : `test.api.carzenplus.com`
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
        "signature":"702f79097da2d8b2314cae3af31bf26d",
        "access_key":"xBPbzY"
    },
    "pick_up":{
        "name":"Xiaoshan Airport",
        "latitude":30.236189,
        "longitude":120.438842,
        "address":"Hangzhou International Airport (HGH)"
    },
    "drop_off":{
        "name":"Zhejiang University",
        "latitude":30.308888,
        "longitude":120.086499,
        "address":"No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal"
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
        "categories":["ECONOMY","STANDARD"],
        "types":["SUV","SEDAN"]
    },
    "booking_time":1659507431,
    "format_booking_time":"2022-06-03 12:03:51",
    "flight_code":"CA1234",
    "transfer_type":"Airport2Point",
    "currency":"CNY"
}
```





### 3.1.7. Example HTTP response

`Response 200  code 200`

``` JSON
{
    "code": 200,
    "success": true,
    "message": "Success",
    "data": {
        "currency": "CNY",
        "transfer_type": "Airport2Point",
        "transfer_services": [
            {
                "price": 135.00,
                "description": "",
                "service_code": "BabySeat",
                "service_name": "Baby Seat",
                "max_booking_count": 10
            }
        ],
        "transfer_vehicles": [
            {
                "description": "Audi or similar",
                "price": 1425.60,
                "vehicle_name": "A6 or similar",
                "brand_name": "Audi or similar",
                "vehicle_id": 1,
                "max_passenger_quantity": 5,
                "max_luggage_quantity": 1,
                "vehicle_icon": "",
                "transfer_ticket_info": {
                    "ticket": "kdb6JNE7J9dcoV91X2YiX2jqnmJYg923",
                    "expire_time": 1659693529
                },
                "category": "STANDARD",
                "type": "SUV",
                "free_waiting_time": 60,
                "tags": [
                    {
                        "tag_name": "COVID-19 Prepared",
                        "tag_value": "COVID-19"
                    }
                ]
            },
            {
                "description": "",
                "price": 549.45,
                "vehicle_name": "Q7 or similar",
                "brand_name": "Audi or similar",
                "vehicle_id": 2,
                "max_passenger_quantity": 7,
                "max_luggage_quantity": 5,
                "vehicle_icon": "",
                "transfer_ticket_info": {
                    "ticket": "BVuCP5fSVKzPsPF5yR9TxJPf1k0nWV8b",
                    "expire_time": 1659693529
                },
                "category": "STANDARD",
                "type": "SUV",
                "free_waiting_time": 60,
                "tags": [
                    {
                        "tag_name": "COVID-19 Prepared",
                        "tag_value": "COVID-19"
                    }
                ]
            },
            {
                "description": "",
                "price": 867.24,
                "vehicle_name": "GL8 or similar",
                "brand_name": "Buick",
                "vehicle_id": 3,
                "max_passenger_quantity": 7,
                "max_luggage_quantity": 7,
                "vehicle_icon": "",
                "transfer_ticket_info": {
                    "ticket": "9rMqVpWEo5Vb2mQ10BmeXEBvCS2OXk7M",
                    "expire_time": 1659693529
                },
                "category": "STANDARD",
                "type": "SUV",
                "free_waiting_time": 60,
                "tags": [
                    {
                        "tag_name": "COVID-19 Prepared",
                        "tag_value": "COVID-19"
                    }
                ]
            }
        ],
        "provider": {
            "name": "Carzen Plus",
            "logo_url": ""
        },
        "meeting_points":[
            {
                "id":3,
                "title":"M&amp;G - San Francisco International Airport",
                "description":"1. Please switch on your phone and connect to the airport WiFi.\r\n2. Collect your luggage, and head to Arrivals\r\n3. The driver will await you there\r\n4. If you are unable to find the driver, please contact the number that is provided on your VOUCHER.",
                "picture":"https://misc-cn.carzenplus.com/upload/image/2303/2e0fee74a400000.png"
            },
            {
                "id":4,
                "title":"33333333333",
                "description":"asdasdasd\r\nasdsad\r\nasdasdasd\r\nasdasd",
                "picture":"https://misc-cn.carzenplus.com/upload/image/2303/2e1099158000000.png"
            }
        ],
        "duration_in_seconds": 3060,
        "distance_in_meters": 47310
    },
    "request_id": "37a85acdafd74882",
    "server_time": 1659691729
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
        "signature":"702f79097da2d8b2314cae3af31bf26d",
        "access_key":"xBPbzY"
    },
    "transfer_ticket":"9rMqVpWEo5Vb2mQ10BmeXEBvCS2OXk7M",
    "flight_code":"CA1234",
    "transfer_type":"Airport2Point",
    "currency":"CNY",
    "partner_order_sn":"D1344068",
    "pick_up":{
        "name":"Xiaoshan Airport",
        "latitude":30.236189,
        "longitude":120.438842,
        "address":"Hangzhou International Airport (HGH)"
    },
    "drop_off":{
        "name":"Zhejiang University",
        "latitude":30.308888,
        "longitude":120.086499,
        "address":"No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal"
    },
    "passenger_info":{
        "adults":1,
        "children":1,
        "infants":0
    },
    "passenger_contact_info":{
        "passenger_name":"Zhang San",
        "passenger_phone":"+8613888888888",
        "passenger_email":"xx@gmail.com"
    },
    "luggage_info":{
        "medium":1,
        "small":1
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
        "transfer_fee":867.24,
        "service_fee":135,
        "total_fee":1002.24
    },
    "booking_time":1659692551
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
        "order_status": "WAIT_CONFIRM",
        "order_sn": "SD2022080508361",
        "partner_order_sn": "D1344068",
        "flight_code": "CA1234",
        "transfer_type": "Airport2Point",
        "currency": "CNY",
        "remark": "remark",
        "pick_up": {
            "name": "Xiaoshan Airport",
            "latitude": 30.236189,
            "longitude": 120.438842,
            "address": "Hangzhou International Airport (HGH)"
        },
        "drop_off": {
            "name": "Zhejiang University",
            "latitude": 30.308888,
            "longitude": 120.086499,
            "address": "No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal"
        },
        "passenger_info": {
            "adults": 1,
            "children": 1,
            "infants": 0
        },
        "passenger_contact_info": {
            "passenger_name": "Zhang San",
            "passenger_phone": "+8613888888888",
            "passenger_email": "xx@gmail.com",
            "passenger_whats_app_account": null,
            "passenger_wechat_account": null
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
            "brand_name": "Buick",
            "model": "GL8 or similar"
        },
        "provider": {
            "name": "Carzen Plus",
            "logo_url": null
        },
        "price_detail": {
            "transfer_fee": 902.23,
            "service_fee": 100.01,
            "total_fee": 1002.24
        },
        "driver_info": null,
        "booking_time": 1659692551
    },
    "request_id": "32c6425721f849d9",
    "server_time": 1659692704
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


| Name            | Description                                  | Schema                                 |
|-----------------|----------------------------------------------|----------------------------------------|
| **code**        | 200 is success, others number is error flags | integer(int32)                         |
| **success**     | true or false                                | boolean                                |
| **request_id**  | Request unique id                            | string                                 |
| **message**     | Message                                      | string                                 |
| **data**        | Response data,                               | [BookingCancelVO](#423bookingcancelvo) |
| **server_time** | Unix time                                    | integer(int64)                         |

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
        "signature":"702f79097da2d8b2314cae3af31bf26d",
        "access_key":"xBPbzY"
    },
    "reason":"Cancel Reason",
    "order_sn":"SD2022080508361"
}
```

### 3.3.7. Example HTTP response

`Response 200` `code 200`

``` JSON
{
    "code": 200,
    "success": true,
    "message": "Success",
    "data": {
        "currency": "CNY",
        "cancel_time": 1659693530,
        "order_total_price": 1002.24,
        "cancel_loss_fee": 1002.24,
        "order_sn": "SD2022080508361",
        "partner_order_sn": "D1344068",
        "cancel_type": "ALL_LOSS_CANCEL"
    },
    "request_id": "9d26b69fda6f40e1",
    "server_time": 1659693530
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
        "signature":"702f79097da2d8b2314cae3af31bf26d",
        "access_key":"xBPbzY"
    },
    "order_sn":"SD2022080508361"
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
        "order_status": "WAIT_DISPATCH",
        "order_sn": "SD2022080508361",
        "partner_order_sn": "D1344068",
        "flight_code": "CA1234",
        "transfer_type": "Airport2Point",
        "currency": "CNY",
        "remark": "remark",
        "pick_up": {
            "name": "Xiaoshan Airport",
            "latitude": 30.236189,
            "longitude": 120.438842,
            "address": "Hangzhou International Airport (HGH)"
        },
        "drop_off": {
            "name": "Zhejiang University",
            "latitude": 30.308888,
            "longitude": 120.086499,
            "address": "No. 866 Yuhangtang Road, Xihu District, Hangzhou, Zhejiang ,China Postal"
        },
        "passenger_info": {
            "adults": 1,
            "children": 1,
            "infants": 0
        },
        "passenger_contact_info": {
            "passenger_name": "Zhang San",
            "passenger_phone": "+8613888888888",
            "passenger_email": "xx@gmail.com",
            "passenger_whats_app_account": null,
            "passenger_wechat_account": null
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
            "brand_name": "Buick",
            "model": "GL8 or similar"
        },
        "provider": {
            "name": "Carzen Plus",
            "logo_url": null
        },
        "price_detail": {
            "transfer_fee": 902.23,
            "service_fee": 100.01,
            "total_fee": 1002.24
        },
        "driver_info": null,
        "booking_time": 1659692551
    },
    "request_id": "a7e3e5edc11d476b",
    "server_time": 1659692876
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


| Name                                     | Description                                                      | Scheme                                                                                                                                                                                                                                                                       |
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **authentication** <br> required         | Authentication parameter                                         | [TransferAuthenticationInfo](#42transferauthenticationinfo)                                                                                                                                                                                                                  |
| **pick_up** <br> required                | Starting point information (address , name, latitude, longitude) | [TransferPointInfo](#43transferpointinfo)                                                                                                                                                                                                                                    |
| **drop_off** <br> required               | End point information (address , name, latitude, longitude)      | [TransferPointInfo](#43transferpointinfo)                                                                                                                                                                                                                                    |
| **passenger_info** <br> required         | Number of passenger, include adults, children,infants            | [PassengerInfo](#44passengerinfo)                                                                                                                                                                                                                                            |
| **luggage_info** <br> optional           | Requirements to luggage space to be supported by the vehicle     | [LuggageInfo](#45luggageinfo)                                                                                                                                                                                                                                                |
| **vehicle_info** <br> optional           | Vehicle information                                              | [TransferVehicleInfo](#46transfervehicleinfo)                                                                                                                                                                                                                                |
| **booking_time** <br> optional           | The booking time. unix timestamp                                 | integer  (int64)      <br>  **There are two fields: booking_time and format_booking_time, can choose either one, but must ensure that the selected field has a value.**                                                                                                      |
| **format_booking_time** <br> optional    | The booking Date Time. format yyyy-MM-dd HH:mm:ss                | string    <br>   **There are two fields: booking_time and format_booking_time, can choose either one, but must ensure that the selected field has a value.**    <br> The default time zone for the format_booking_time parameter should be the time zone of the pickup city  |
| **flight_code** <br> optional            | The numeric flight number.                                       | string                                                                                                                                                                                                                                                                       |
| **transfer_type** <br> required          | The type of transfer.                                            | enum <br>Airport2Point <br> Point2Airport <br> Point2Point                                                                                                                                                                                                                   |
| **currency** <br> required               | TheCurrency code in ISO 4217 format.                             | string                                                                                                                                                                                                                                                                       |


## 4.2.TransferAuthenticationInfo


| Name                           | Description                           | Scheme   |
|--------------------------------|---------------------------------------|----------|
| **access_key** <br> required   | AccessKey ID                          | string   |
| **signature** <br> required    | MD5 (AccessKey ID + AccessKey secret) | string   |



## 4.3.TransferPointInfo

| Name                              | Description           | Scheme          |
|-----------------------------------|-----------------------|-----------------|
| **name** <br> optional            | Point name            | string          |
| **address** <br> optional         | Point address details | string          |
| **latitude** <br> optional        | Latitude              | number (double) |
| **longitude** <br> optional       | Longitude             | number (double) |

- `address` , `latitude longitude` must be provided at least one.


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

| Name                           | Description        | Scheme                                                               |
|--------------------------------|--------------------|----------------------------------------------------------------------|
| **categories** <br> optional   | Vehicle category   | array enum <br>ECONOMY<br>STANDARD<br> BUSINESS_CLASS<br>FIRST_CLASS |
| **types** <br> optional        | Vehicle type       | array enum <br>SUV<br>SEDAN<br> VAN<br>BUS<br>LIMO                   |

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

| Name                                     | Description                                                             | Scheme                                                                                                                                                                                                                                                                      |
|------------------------------------------|-------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **authentication** <br> required         | Authentication parameter                                                | [TransferAuthenticationInfo](#42transferauthenticationinfo)                                                                                                                                                                                                                 |
| **transfer_ticket** <br> required        | `/transfer/query` > transfer_vehicles > transfer_ticket_info > ticket   | string                                                                                                                                                                                                                                                                      |
| **flight_code** <br> optional            | The numeric flight number.                                              | string                                                                                                                                                                                                                                                                      |
| **transfer_type** <br> required          | The type of transfer.                                                   | enum <br>Airport2Point <br> Point2Airport <br> Point2Point                                                                                                                                                                                                                  |
| **currency** <br> required               | TheCurrency code in ISO 4217 format.                                    | string                                                                                                                                                                                                                                                                      |
| **remark** <br> optional                 | Customer remark.                                                        | string                                                                                                                                                                                                                                                                      |
| **partner_order_sn** <br> required       | Partner order number.                                                   | string                                                                                                                                                                                                                                                                      |
| **pick_up** <br> required                | Starting point information (address , name, latitude, longitude)        | [TransferPointInfo](#43transferpointinfo)                                                                                                                                                                                                                                   |
| **drop_off** <br> required               | End point information (address , name, latitude, longitude)             | [TransferPointInfo](#43transferpointinfo)                                                                                                                                                                                                                                   |
| **passenger_info** <br> required         | Number of passenger, include adults, children,infants                   | [PassengerInfo](#44passengerinfo)                                                                                                                                                                                                                                           |
| **luggage_info** <br> optional           | Requirements to luggage space to be supported by the vehicle            | [LuggageInfo](#45luggageinfo)                                                                                                                                                                                                                                               |
| **passenger_contact_info** <br> required | Passengers’ information. Information about “main” passenger is required | [PassengerContactInfo](#49passengercontactinfo)                                                                                                                                                                                                                             |
| **transfer_services** <br> required      | Platform model information, need to contact us to bind                  | <[TransferServiceItem](#410transferserviceitem)> array                                                                                                                                                                                                                      |
| **price_detail** <br> required           | Payment detail                                                          | [OrderPriceDetail](#411orderpricedetail)                                                                                                                                                                                                                                    |
| **booking_time** <br> optional           | The booking time. unix timestamp                                        | integer  (int64)      <br>  **There are two fields: booking_time and format_booking_time, can choose either one, but must ensure that the selected field has a value.**                                                                                                     |
| **format_booking_time** <br> optional    | The booking Date Time. format yyyy-MM-dd HH:mm:ss                       | string    <br>   **There are two fields: booking_time and format_booking_time, can choose either one, but must ensure that the selected field has a value.**    <br> The default time zone for the format_booking_time parameter should be the time zone of the pickup city |



## 4.9.PassengerContactInfo


| Name                                          | Description                   | Schema  |
|-----------------------------------------------|-------------------------------|---------|
| **passenger_name** <br> required              | Name of passenger             | string  |
| **passenger_phone** <br> required             | Mobile phone of passenger     | string  |
| **passenger_email** <br> optional             | Email address of passenger    | string  |
| **passenger_whats_app_account** <br> optional | WhatsApp account of passenger | string  |
| **passenger_wechat_account** <br> optional    | Wechat account of passenger   | string  |


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

| Name                                     | Description                                                             | Schema                                                             |
|------------------------------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------|
| **order_status** <br> required           | OrderStatus                                                             | enum <br> [OrderStatusEnum](#426orderstatusenum)                   |
| **order_sn** <br> required               | Order number of Carzenplus                                              | string                                                             |
| **booking_time** <br> required           | The booking time. unix timestamp                                        | integer  (int64)                                                   |
| **partner_order_sn** <br> required       | Partner order number.                                                   | string                                                             |
| **flight_code** <br> required            | The flight number including airline code                                | string                                                             |
| **transfer_type** <br> required          | The type of transfer.                                                   | enum <br>Airport2Point <br> Point2Airport <br> Point2Point         |
| **currency** <br> required               | TheCurrency code in ISO 4217 format.                                    | string                                                             |
| **remark** <br> required                 | Customer remark..                                                       | string                                                             |
| **pick_up** <br> required                | Starting point information (address , name, latitude, longitude)        | [TransferPointInfo](#43transferpointinfo)                          |
| **drop_off** <br> required               | End point information (address , name, latitude, longitude)             | [TransferPointInfo](#43transferpointinfo)                          |
| **passenger_info** <br> required         | Number of passenger, include adults, children,infants                   | [PassengerInfo](#44passengerinfo)                                  |
| **luggage_info** <br> optional           | Requirements to luggage space to be supported by the vehicle            | [LuggageInfo](#45luggageinfo)                                      |
| **passenger_contact_info** <br> required | Passengers’ information. Information about “main” passenger is required | [PassengerContactInfo](#49passengercontactinfo)                    |
| **transfer_services** <br> optional      | Support service                                                         | <[BookingTransferServiceVO](#413bookingtransferservicevo)><br> arr |
| **transfer_vehicle** <br> optional       | Vehicle info                                                            | [BookingVehicleVO](#414bookingvehiclevo)                           |
| **provider** <br> optional               | Provider Info                                                           | [PlatformProviderVO](#415platformprovidervo)                       |
| **price_detail** <br> required           | Payment detail                                                          | [BookingPriceDetailVO](#411orderpricedetail)                       |
| **driver_info** <br> optional            | Driver information                                                      | [BookingDriverVO](#416bookingdrivervo)                             |



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

| Name                                  | Description                       | Schema                                                     |
|---------------------------------------|-----------------------------------|------------------------------------------------------------|
| **transfer_type** <br> required       | The type of transfer.             | enum <br>Airport2Point <br> Point2Airport <br> Point2Point |
| **price** <br> required               | Itinerary price.                  | number (double)                                            |
| **currency** <br> required            | Currency code in ISO 4217 format. | string                                                     |
| **transfer_services** <br> required   | Transfer Services.                | <[TransferServiceVO](#419transferservicevo)><br>array      |
| **transfer_vehicles** <br> required   | Vehicle information               | <[TransferVehicleVO](#420transfervehiclevo)> <br>array     |
| **provider** <br> optional            | Provider Info                     | [PlatformProviderVO](#415platformprovidervo)               |
| **duration_in_seconds** <br> required | The numeric duration, in seconds. | integer (int64)                                            |
| **distance_in_meters** <br> required  | The numeric distance, in meters.  | integer  (int64)                                           |
| **meeting_points** <br> optional      | Meeting point                     | <[MeetingPointVO](#425meetingpointvo)> <br>array           |


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

| Name                                     | Description                        | Schema                                                         |
|------------------------------------------|------------------------------------|----------------------------------------------------------------|
| **transfer_ticket_info** <br> required   | Book order ticket                  | [TransferTicket](#418transferticket)                           |
| **vehicle_name** <br> optional           | Vehicle model. e.g. A6             | string                                                         |
| **brand_name** <br> optional             | Vehicle brand. e.g. Audi           | string                                                         |
| **vehicle_id** <br> optional             | Vehicle ID                         | integer (int64)                                                |
| **max_passenger_quantity** <br> required | Max seat count,without driver seat | integer (int32)                                                |
| **max_luggage_quantity** <br> required   | Max luggage count                  | integer (int32)                                                |
| **description** <br> optional            | Vehicle descriptions               | string                                                         |
| **vehicle_icon** <br> optional           | Vehicle picture url                | string                                                         |
| **price** <br> required                  | equal to TransferFee               | number (double)                                                |
| **category** <br> required               | Vehicle category                   | enum <br>ECONOMY<br>STANDARD<br> BUSINESS_CLASS<br>FIRST_CLASS |
| **type** <br> required                   | Vehicle type                       | enum <br>SUV<br>SEDAN<br> VAN<br>BUS<br>LIMO                   |
| **free_waiting_time** <br> optional      | Free Waiting Time  unit : minute   | integer (int32)                                                |
| **tags** <br> optional                   | Vehicle Tag                        | <[TransferTagVO](#424transfertagvo)><br>array                  |


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

## 4.23.BookingCancelVO


| Name                                | Description                          | Schema                                                                             |
|-------------------------------------|--------------------------------------|------------------------------------------------------------------------------------|
| **currency** <br> required          | Currency code in ISO 4217 format     | string                                                                             |
| **cancel_time** <br> required       | Cancel Unix timespan,unit:Second     | integer (int64)                                                                    |
| **order_total_price** <br> required | Order total price                    | number (double)                                                                    |
| **cancel_loss_fee** <br> required   | Cancel loss fees                     | number (double)                                                                    |

## 4.24.TransferTagVO

| Name                           | Description | Schema      |
|--------------------------------|-------------|-------------|
| **tag_name** <br> required     | Tag Name    | string      |
| **tag_value** <br> required    | Tag Value   | string      |      

## 4.25.MeetingPointVO

| Name                          | Description                     | Schema             |
|-------------------------------|---------------------------------|--------------------|
| **id** <br> optional          | Meeting point id                | integer (int64)    |
| **title** <br> optional       | Meeting point title             | string             |   
| **description** <br> optional | Meeting point title description | string             |   
| **picture** <br> optional     | Meeting point picture           | string             |   

## 4.26.OrderStatusEnum
| Value               | Description              |
|---------------------|--------------------------|
| **WAIT_CONFIRM**    | Booking Pending          |
| **WAIT_DISPATCH**   | Booking Accepted         |
| **WAIT_ASSIGN**     | Driver Pending           |
| **WAIT_SERVICE**    | On Proceed               |
| **DEPARTED**        | On the way to pickup     |
| **ARRIVED**         | Arrived the pickup Point |
| **SERVING**         | Pick on board            |
| **COMPLETED**       | Job completed            |
| **CANCELLED**       | Booking Canceled         |