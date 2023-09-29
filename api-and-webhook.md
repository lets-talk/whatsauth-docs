---
title: API and Webhook
layout: home
nav_order: 2
---
# API & Webhook

## Authentication

The API requests are authenticated using a Bearer token in the Authorization Header. You can get the token from an application in your account ([learn more](https://whatsauth.freshdesk.com/support/solutions/articles/151000092660-how-to-create-your-first-app-in-whatsauth-and-test-it)).

  

  

## Code Generation

To get a verification code from WhatAuth API you need to make an HTTPS request providing the API key for authorization and some parameters for customization.

### cURL Sample

The following cURL command you can try from your terminal

```bash
    curl -G \
    --location 'https://whatsauth.me/api/v1/verification_code' \
    --data-urlencode 'callback_url=https://mycompany.io/webhook/whatsauth' \
    --data-urlencode 'expires_at=10' \
    --data-urlencode 'link_message=Send this message to verify your phone in MyCompany' \
    --data-urlencode 'expiration_message=Sorry, this code is expired' \
    --data-urlencode 'failure_message=Oops! someting went wrong, please try again.' \
    --data-urlencode 'response_message=Welcome! you just verified your phone as easy as it could be.' \
    --header 'Authorization: Bearer MY_APIKEY'
```

### Parameters  

|      Parameter     |   Type  |                                                         Description                                                        |
|:------------------:|:-------:|:--------------------------------------------------------------------------------------------------------------------------:|
| expires_at         | integer | The number of minutes the verification code expires in. The minimum value is 1 minute.                                     |
| callback_url       | string  | The webhook URL will receive verification status. Must implement with HTTPS POST method.                                   |
| authorized_numbers | string  | The list of phone numbers that are allowed to validate generated code. By default any phone number is authorized.          |
| link_message       | string  | The message appears on the client's screen as a part of the message code above-generated code.                             |
| expiration_message | string  | The message is sent to the client with intent to validate the expired code.                                                |
| failure_message    | string  | The message is sent to the client when there is a failure in sending verification status via provided webhook.             |
| response_message   | string  | The Message is sent to the client as a notification of a successful validation.                                            |
| qr                 | 0 or 1  | Set this parameter to 1 in case you want to receive QR code URL in response.                                               |
| channel            | string  | The default channel is WhatsApp. You can specify "sms" if you want to receive a link that triggers an SMS validation code. |

The default channel is WhatsApp. You can specify "sms" if you want to receive a link that triggers an SMS validation code.  

You can also specify default values for each parameter at the application level and skip those in the request. If you set a **parameter in your request it will override** the one set as default.


## Customization Elements

The following examples illustrate which are the expression of the parameters

![](https://s3.amazonaws.com/cdn.freshdesk.com/data/helpdesk/attachments/production/151020508950/original/UKCuSOcA_wb9cInIaFe118ouWuzmiliWtA.png?1683919585)
**Verification success message**
{: .text-center }

![](https://s3.amazonaws.com/cdn.freshdesk.com/data/helpdesk/attachments/production/151020509006/original/Wbow66G4hhh9u6be01W0tPbZ3m1SKaBrtQ.png?1683919610)
**Expiration message**
{: .text-center }

![](https://s3.amazonaws.com/cdn.freshdesk.com/data/helpdesk/attachments/production/151020509030/original/UfMaH_Z7kjP2r9hQ585qtek0wqrPHTLz_A.png?1683919630)
**Failure message**
{: .text-center }

## Response

If the request is properly formed and authenticated you'll receive a response with a JSON like this:

```json
    {
        "code": "322c9a59dd",
        "link": "https://wa.me/+56943426553?text=%3E%3E322c9a59dd%3C%3C%0AJust%20tap%20the%20%22send%22%20button.",
        "qr": "https://api.qrserver.com/v1/create-qr-code/?data=https%3A%2F%2Fwa.me%2F%2B56943426553%3Ftext%3D%253E%253E322c9a59dd%253C%253C%250AJust%2520tap%2520the%2520%2522send%2522%2520button.&size=200x200",
        "deep_link": "whatsapp://send?text=%3E%3E322c9a59dd%3C%3C%0AJust%20tap%20the%20%22send%22%20button.&phone=+56943426553"
    }
```

| Parameter |  Type  |                                        Description                                       |
|:---------:|:------:|:----------------------------------------------------------------------------------------:|
| code      | string | Generated unique verification code.                                                      |
| link      | string | The link that takes you to WhatsApp web or mobile application with a predefined message. |
| qr        | string | URL of the generated QR code image for the WhatsApp link. When requested.                |
| deep_link | string | The deep link that takes you to WhatsApp application with a predefined message.          |

‍

## Webhook

In order to receive the updated status of the verification process you will need to implement the webhook which is a URL under HTTPS protocol and POST method. There you will receive the following information in JSON format:

```json
    {
       "id": "123e4567-e89b-12d3-a456-426614174000",
       "status": "validated",
       "verification_code": "9f76681bd4",
       "phone_number": "+56911111111",
       "profile_name": "Some Folk",
       "expires_at": "2021-01-27T01:17:13.674Z",
       "requested_at": "2021-01-26T23:17:13.674Z",
       "validated_at": "2021-01-26T23:23:17.28Z",
       "authorized_numbers": [],
       "error": null
    }
```

From here you can obtain the data required to follow up your business process.

| Attribute name     | Type            | Description                                                                                  |
|--------------------|-----------------|----------------------------------------------------------------------------------------------|
| id                 | UUID            | Verification id.                                                                             |
| status             | String          | Status of verification code. Possible values: “requested”, “validated”, “expired”, “failed”. |
| verification_code  | String          | Unique verification code associated with the process.                                        |
| phone_number       | String          | Mobile phone number which validated the code.                                                |
| profile_name       | String          | Whatsapp profile name of the person validated the code.                                      |
| requested_at       | ISO 8601 String | Time when verification code was requested.                                                   |
| validated_at       | ISO 8601 String | Time when verification code was validated by the client.                                     |
| expires_at         | ISO 8601 String | Time when verification code expires.                                                         |
| authorized_numbers | String Array    | Phone numbers authorized to validate the code.                                               |
| error              | String          | Error message in case of validation failure.                                                 |

  
{: .highlight }
The webhook request expects to have a response 200 or 204 status and Content-type `application/json`, otherwise, it will mark the validation as a failure.
