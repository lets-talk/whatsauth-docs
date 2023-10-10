---
layout: default
title: How to keep your endpoint secure
parent: Guides
---
# How to use WhatsAuth while keeping your endpoint secured

While developing the integration with WhatsAuth you might think that is a risk to enable an endpoint in your system to receive the webhooks.
In order mitigate that risk our recomended solution is to implement a key based access control polocy in your endpoint.
This way you will be able to reject all the request that don't provide the right key and only accept the ones properly authenticated.

{: .highlight }
This suggested solutions relays in your system capacity of authenticating request based on a `apiKey` parameter in the query string.

## How to set an API Key

If ypu check the [API specs]({% link api-and-webhook.md %}) you'll see that every request to get a verification code allow the speceficiation of a `callback_url`, for instance: https://mycompany.io/webhook/whatsauth, here you can add some convinient parameters in that URL, not just the host and path. Just like we suggest in the [WhatsApp Login Guide]({% link guides/whatsapp-login.md %}) you can include an `apiKey` param in the URL:

https://mycompany.io/webhook/whatsauth?apiKey=MY-SUPER-SECRET-KEY

This way when WhatsAuth notify your system about the status of the validation it will make a PSOT request to your endpoint including the MY-SUPER-SECRET-KEY value as `apiKey` and you could rest assured that the request is authenticated.

## What if the Key is Compromised or Revoked

In the unpleaseant event of a key being leaked you should inmidiatly revoked that key in your system and set a new key e.g. NEW-MEGA-SECRET-KEY and also start request the verification code with a new `apiKey` param in the `callback_url`:

https://mycompany.io/webhook/whatsauth?apiKey=NEW-MEGA-SECRET-KEY

And you will start receiving authenticated webhook again


{: .highlight }
Architenture Tip: keep the `apiKey` as variable in your code to be able to change it rapidly and easy when required.