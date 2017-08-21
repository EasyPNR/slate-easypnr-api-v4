---
title: EasyPNR API Version 4.0

language_tabs: # must be one of https://git.io/vQNgJ
  - curl

toc_footers:
  - <a href="https://easypnr.com/signup" target="_blank">Sign up to use this API</a>
  #- <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
#  - errors

search: true
---

# Introduction

> API Endpoint Version 4

```
http://api.easypnr.com/v4/
```

Welcome to the **EasyPNR API v4** documentation! Following the further instructions you will be able to decode Amadeus, Sabre and Galileo PNRs directly on your application.

The **EasyPNR API** is a REST Server available at the endpoint [http://api.easypnr.com/v4](http://api.easypnr.com/v4/).

The API is pretty simple, anyway, in case of problems, contact us on [support@easypnr.com](mailto:support@easypnr.com) or using the form available on the [website](http://www.easypnr.com/contact).

## What's new in Version 4?

 - Included a Map with "extraInfo" on the JSON objects of the /decode method response. This was made to ensure more flexibility, not being necessary to create a new API version each time the server evolves, per example, when some new data field is being decoded.
 - Sabre Record Locator being decoded.
 - Amadeus fare being decoded.

## Older versions

The Protocol Version 3 documentation can be found here  [http://docs.easypnr.com/api/v3](http://docs.easypnr.com/api/v3/).

# Authentication

> To use the Web Services, you must pass your API Token on all requests:

```curl
# Example of a request using an API Key
curl -i -X POST -h "X-Api-Key: mySecretKey" https://api.easypnr.com/v4/ping
```

To use the Web Services, you must have an active account on the [www.easypnr.com](http://www.easypnr.com) and obtain your **API Key** on the account page. You can manage your API keys in the main website.

Once you have your API Key, you must use it in all Web Service calls, passing your key in an *HTTP Header* named **"X-Api-Key"**.

Your API keys carry many privileges, so be sure to keep them secret! Do not share your secret API keys in publicly accessible areas such GitHub, client-side code, and so forth.

# Available methods

## /decode

```curl
# Request
curl -i -X POST -H "X-Api-Key: mySecretKey" \
 -d $'1.JOHNSON/BRIAN MR  2.JOHNSON/BRENDA MRS                             
   2  EK 262 Y 08MAR 6 GRUDXB HK1       2  0125 2255   77W E 0 M               
      ADD ADVANCE PASSENGER INFORMATION IN SSR DOCS                            
      ADD SSR PCTC TO PROVIDE PAX CONTACT                                      
      SEE RTSVC                                                                
   4 TRN 2C  87    6628 AF 26NOV 4 FRLPD FRPLY HK1   1800  2007                 
     FRLPD/LYON PART DIEU//FRPLY/PARIS GARE LYON     /TGD *
   5 HTL 1A HK4 CVF 30NOV-01DEC/HOTEL LES ANCOLIES/RUE DES                      
       GRAVELLES 73120 COURCHEVEL/T-04.79.08.27.66/CF-AATRIP/                     
   ' \
 -H "Content-Type: application/json"   https://api.easypnr.com/v4/decode
```


> The above command returns JSON structured like this:

```json
{
  "persons": [
    {
      "firstName": "BRIAN",
      "lastName": "JOHNSON",
      "title": "MR",
      "rawData": "JOHNSON/BRIAN MR"
    },
    {
      "firstName": "BRENDA",
      "lastName": "JOHNSON",
      "title": "MRS",
      "rawData": "JOHNSON/BRENDA MRS"
    }
  ],
  "flightInfo": {
    "flights": [
      {
        "company": {
          "iataCode": "EK",
          "description": "Emirates"
        },
        "departureTime": "2018-03-08 01:25:00",
        "landingTime": "2018-03-08 22:55:00",
        "flight": "262",
        "departureAirport": {
          "iataCode": "GRU",
          "description": "Guarulhos International Airport - Guarulhos, São Paulo, Brazil"
        },
        "extraInfo": {},
        "seatInfo": [],
        "landingAirport": {
          "iataCode": "DXB",
          "description": "Dubai International Airport - Dubai, United Arab Emirates"
        }
      }
    ],
    "extraInfo": null
  },
  "hotelInfo": {
    "hotels": [
      {
        "extraInfo": null,
        "name": "HOTEL LES ANCOLIES",
        "address": "RUE DES GRAVELLES 73120 COURCHEVEL",
        "checkIn": "2017-11-30",
        "checkOut": "2017-12-01"
      }
    ],
    "extraInfo": null
  },
  "trainInfo": {
    "extraInfo": null,
    "trains": [
      {
        "departureTime": "2017-11-26 18:00",
        "arrivingTime": "2017-11-26 20:07",
        "departureStationCode": "FRLPD",
        "arrivingStationCode": "FRPLY",
        "number": "6628"
      }
    ],
    "stationNames": {
      "FRLPD": "LYON PART DIEU",
      "FRPLY": "PARIS GARE LYON"
    }
  },
  "extraInfo": null
}
```

Decode the PNR.

### Request

`POST https://api.easypnr.com/v4/decode`

At the `BODY` of the `POST` submit your encoded PNR as plain text.

### Response

The response is the decoded PNR.

<!-- aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside-->

## /ping

```curl
# Request
curl -i -X GET -H "X-Api-Key: mySecretKey"  https://api.easypnr.com/v4/ping
```

```text
# Response
pong 1478969148631
```
Ping the server.

### Request

`GET https://api.easypnr.com/v4/ping`

### Response
The above command returns a 'pong' followed by the server timestamp.
