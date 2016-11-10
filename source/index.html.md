---
title: EasyPNR API Version 3.0

language_tabs:
  - curl

toc_footers:
  - <a href="https://easypnr.com/signup" target="_blank">Sign up to use this API</a>
  #- <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
#  - errors

search: true
---

# Introduction

> API Endpoint Version 3

```
http://api.easypnr.com/v3/
```

Welcome to the **EasyPNR API** documentation! Following the further instructions you will be able to decode Amadeus, Sabre and Galileo PNRs directly on your application.

The **EasyPNR API** is a REST Server available at the endpoint [http://api.easypnr.com/v3](http://api.easypnr.com/v3/).

The API is pretty simple, anyway, in case of problems, contact us on [support@easypnr.com](mailto:support@easypnr.com) or using the form available on the [website](http://www.easypnr.com/contact).


# Authentication

> To use the Web Services, you must pass your API Token on all requests:

```curl
# Example of a request using an API Key
curl -i -X POST -d "api_key=mySecretKey" https://api.easypnr.com/v3/ping
```

To use the Web Services, you must have an active account on the [www.easypnr.com](http://www.easypnr.com) and obtain your **API Key** on the account page.

Once you have your API Key, you must use it in all Web Service calls, passing your key in an *HTTP Header* named **"api_key"**.

# decode

```curl
# Request
curl -i -X POST -d "encodedPNR=1.JOHNSON/BRIAN MR  2.JOHNSON/BRENDA MRS \n 2 QR 905 E 06MAR 4 DOHMEL HK1 1  0005 0810+1 *1A/E*"  -H "Content-Type: application/json" -H "api_key: mySecretKey" https://api.easypnr.com/v3/decode
```

> The above command returns JSON structured like this:

```json
{
   "persons":[
      {
         "firstName":"BRIAN",
         "lastName":"JOHNSON",
         "title":"MR",
         "rawData":"JOHNSON/BRIAN MR"
      },
      {
         "firstName":"BRENDA",
         "lastName":"JOHNSON",
         "title":"MRS",
         "rawData":"JOHNSON/BRENDA MRS \\n"
      }
   ],
   "others":null,
   "flightInfo":{
      "flights":[
         {
            "company":{
               "iataCode":"QR",
               "description":"Qatar Airways"
            },
            "departureTime":"2016-03-06 00:05:00",
            "landingTime":"2016-03-07 08:10:00",
            "departureAirport":{
               "iataCode":"DOH",
               "description":"Hamad International Airport - Doha, Qatar"
            },
            "flight":"905",
            "landingAirport":{
               "iataCode":"MEL",
               "description":"Melbourne Airport - Melbourne, Victoria, Australia"
            }
         }
      ]
   },
   "hotelInfo":{
      "hotels":[

      ]
   },
   "trainInfo":{
      "trains":[

      ],
      "stationNames":{

      }
   }
}
```

Decode a PNR.

### HTTP Request

`POST https://api.easypnr.com/v2/decode`

### Query Parameters

Parameter  | Required |Default | Description
---------  | ---------|------- | -----------
encodedPNR | true     |false   | The PNR that will be decoded.


<!-- aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside-->
