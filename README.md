# Open Banking Postman collections for EU
Postman collections for Mastercard Open Banking Europe.

<p align="center">
<img src="images/header.png" width="250px"/>
</p>

## Overview

These are the [Postman](https://www.postman.com/) collections for [Mastercard Open Banking Europe APIs](https://aiia.eu).

## Collections

### For unlicenced customers
Our PSD2 compliant service is an out of the box ready, no license required, no hassle. You can get started with one line of code.

#### Aiia Data and Aiia Pay
Compliant and reliable Open Banking Payments & Data services from day one. 
[Pay & Data Collection JSON ⤓](./openbanking-eu.postman_collection.json)

[Pay & Data Environment - Sandbox JSON ⤓](./openbanking-eu.postman_environment-sandbox.json)

#### Insights
Verify Account Balance and Account Owner through our simple API. 

[Insights Collection JSON ⤓](./insights.postman_collection.json)

[Insights Environment - Sandbox JSON ⤓](./insights.postman_environment-sandbox.json)

### For licenced customers
If you already hold an Open Banking license, you can also use our solutions tailored for your use cases. You can get started with one line of code.

#### Aiia Enterprise
Aiia Enterprise - soon

#### Insights for Enterprise
Verify Account Balance, Account Owner and Account Income through our simple API. 

[Enterprise Insights Collection JSON ⤓](./enterprise-insights.postman_collection.json)

[Enterprise Insights Environment - Sandbox JSON ⤓](./enterprise-insights.postman_environment-sandbox.json)

## Run the Collection
### Things to Know :point_down:

1. Fire up a browser and go to [our developer portal](https://portal.aiia.eu)

2. Click on the “Sign up (or log in)” button

3. Log in with your username/password or either a GitHub or Google account. If you don't have an account, don't worry. Click “Sign up” and create one for free.

4. Create an app on the client portal

5. Go to your newly created app

6. Take note of your `Client ID` and `Client Secret`

> **Notice** <br>Please be aware that these credentials will only give you access to the sandbox environment and will therefore only expose _Test banks_. When you're ready to go live, go to the <a href="https://docs.aiia.eu/#/production/access" target="_blank">Production access</a> section of our documentation to learn how to get access to actual production data. 🚀

### Import or Fork the Collection
1. Click here: [<img src=https://run.pstmn.io/button.svg alt="Run In Postman" style="width: 128px; height: 32px;">](https://god.gw.postman.com/run-collection/26779181-558ad9cb-2a75-4d35-a7d6-615ba148bb66?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D26779181-558ad9cb-2a75-4d35-a7d6-615ba148bb66%26entityType%3Dcollection%26workspaceId%3Ddc9c22f1-d88f-417d-8a88-662dba528689#?env%5BMastercard%20Open%20Banking%20EU%20Environment%20-%20Aiia%20Demo%5D=W3sia2V5IjoiYmFzZV91cmwiLCJ2YWx1ZSI6Imh0dHBzOi8vYXBpLXNhbmRib3guYWlpYS5ldSIsInR5cGUiOiJ0ZXh0IiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJjbGllbnRfaWQiLCJ2YWx1ZSI6IiIsInR5cGUiOiJ0ZXh0IiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJjbGllbnRfc2VjcmV0IiwidmFsdWUiOiIiLCJ0eXBlIjoidGV4dCIsImVuYWJsZWQiOnRydWV9LHsia2V5IjoiY2xpZW50X3JlZGlyZWN0X3VyaSIsInZhbHVlIjoiIiwidHlwZSI6InRleHQiLCJlbmFibGVkIjp0cnVlfV0=)
2. Select the environment (top right) and update `client_id`, `client_secret` and `client_redirect_uri` variables. We'll talk about these in more detail in the next section.
3. Click _Send_ on individual requests
4. Explore the various folders and update the collection as you wish

## Onboard your first user

Time to test connecting your first user to your service. 

### Step 1 – Start the connect flow

First, you need to find your `Client ID` and `Client Secret` that we noted down earlier. These are located within your app(s), which you can find in the [apps section](https://portal.aiia.eu/apps).

Found them? Great! Make sure you add them to your Postman Environment on the top right.

Now it’s time to connect your first user. In this example, the user is asked to share accounts and transaction data with you, as indicated by the [scope](https://docs.aiia.eu/#/auth/scopes/). You should send the following request in Postman:

```
  Connect / OAuth2 Connect
```

The `redirect_uri` is where the user will be redirected to after finishing the log-in flow. This needs to match one of the redirects you specified when you created your application on the [developer portal](https://portal.aiia.eu/). For more details on how to onboard users and what functionality you can request, please check out [connect flow](https://docs.aiia.eu/#/auth/flow/) and [scopes](https://docs.aiia.eu/#/auth/scopes/).

> **Notice** <br>Connect flow is very similar to the OAuth flow, which you might be familiar with. To access your end users' transaction data, we need to get their consent. We also need an additional consent to pass that data on to you.

The response will be a `302 (Found or Moved Temporarily)` that you'll need to follow in order to redirect the user. Please look in the location header to figure out where you should redirect the user to.

```
    Header / Location: https://app-sandbox.aiia.eu/#/one-time?sessionId=fada3b2f-5e57-4a41-9156-b43ed32148fe&closeUrl=https%3A%2F%2Fhttpbin.org&culture=en
```

### Step 2 – Register users

After navigating the user to the connect URL, the user signs up and connects their accounts. This consists of the following steps:

1. Enter email address

2. Enter the verification code from the email received

3. Accept consent if presented

4. Log in to `Test bank with data #1 DKK`. It'll accept any username and any numeric password.

5. Choose one or more accounts

6. Accept consent to pass data on to your app

![Login flow](images/connect-flow.png)

After completing the flow, the user will be redirected back to the provided `redirect_uri` with a `code` that you'll use in the next step.

Here's an example of what a `redirect_uri` looks like:

```
https://httpbin.org/anything?code=ygAAAAVDaXBoZXJ0ZXh0AJAAAAAAoy734oFjfPFDa9TmOtOAYwcTMKcWZ2782qTQEnjFtW1FsEjone0S6UrXUnD87WrEvidMfCleZgm6K3ysf0eG9hwjylyqUzehya7SIssvR9QwUjtXHCSDPUQV8mYbubbIUGOacfSjqe%2Fnkeop4N37k786234wDrBwW1zJeFZb4af6Ljk7wuzmIR5DzYlutM66vsqCMmNBUl2ABAAAAAAuhPflJ4fuLP45FJmAp4FkBBLZXlJ7923AAAAAAAA%3D%3D
```

Take note of the `code`. You'll use it in the next step to get your session and log-in tokens.

> **Notice** <br>We have an array of [test banks](https://docs.aiia.eu/#/production/provider-support) that can test different configurations.

### Step 3 – Exchange the code for tokens

Use the `code` from Step 2 to get an access token for the user. Please notice that the `code` may be URL encoded if you received it in your browser. Therefore, you must remember to decode it if you're walking through this guide step by step. You can use [this](https://www.urldecoder.org) or any other URL decoder to do the magic. Make sure use the decoded URL in the `code`.

The `redirect_uri` should be automatically filled in by the postman environment.

Now make the following request from Postman:

```
    Connect / Code Exchange
```

> **Notice** <br>A `code` can only be used once and expires after one minute.

The response contains two tokens: `access_token` and `refresh_token`. This is an example of a successful response:

```json
{
  "access_token": "eyJhbGciOiJIUzI1Ni978juanR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJmYTE4OTI3MS1mOTY1LTRmNWMtOTlmOS1lNDViNzNiYzI4MzkiLCJjbGllbnRJZCI6InZpaWEtZnBwIiwicm9sZSI6IkNsaWVudFVzZXIiLCJzZ67623aW9uSWQiOiJlZmE1NWU0ZS0xZTUxLTQ1YWMtYWEyYy01OThhNjFjMTZlOTYiLCJuYmYiOjE1Njc0MTQxNzMsImV4cCI6MTU2NzQxNzc3MywiaWF0IjoxNTY3NDE0MTczfQ.7QD6zGcdonYy79384buXOqsykWrbWa3L6LW4d9uzb-zA",
  "expires_in": 3600,
  "redirect_uri": "https://httpbin.org/anything",
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI687234pXVCJ9.eyJ1c2VySWQiOiJmYTE4OTI3MS1mOTY1LTRmNWMtOTlmOS1lNDViNzNiYzI4MzkiLCJjbGllbnRJZCI6InZpaWEtZnBwIiwiY29uc2VudElkIjoiYTYyODExYWYtNzUxMS00ZWQ0LoyiauasiYTEtMjAwNzc2NGQ1MTIwIiwic2Vzc2lvbklkIjoiZWZhNTVlNGUtMWU1MS00NWFjLWFhMmMtNTk4YTYxYzE2ZTk2Iiwicm9sZSI6IlJlZnJlc2hUb2tlbiIsIm5iZiI6MTU2NzQxNDE3MywiZXhwIjoxNTY4NjIzNzczLCJpYXQiOjE1Njc0MTQxNzN9.5-x0NNg5lMxPnZRYtu983764q0sbPcSb7U9b23e3Zwx0Ss9I",
  "token_type": "bearer"
}
```

The `access_token` you have received will now automatically get populated into your Postman Environment. You'll be using it in the next step to get a list of all the accounts that the end user has given you access to.

### Step 4 – Access accounts

Now you're all set to access the user's data.  You do so by sending the following request in Postman:

```
    Data / List Accounts
```

This endpoint will produce a response that contains an overview of the user's accounts.

```json
{
  "accounts": [
    {
        "accountProvider": {
            "id": "TestDataBank1",
            "name": "Test bank with data #1 DKK"
        },
        "available": null,
        "availableBalance": null,
        "booked": {
            "currency": "DKK",
            "value": 6439.15
        },
        "bookedBalance": 6439.15,
        "currency": "DKK",
        "id": "ZmExODkyNzEtZjk2NS00ZjVjLTk5ZjktZTQ1YjczYmMyODM5fFRlc3REYXRhQmFuazF6823DZ0NFBrOXVORGdpejdKQ0tjSzN2aXM5ZFIzd0gzLWhSNWJhY21nSEZCdy4x",
        "lastSynchronized": "2019-09-02T08:52:16.5816944Z",
        "nagApiAccountId": "T6t4Pk9uNDgiz7JCKcK3vis9dR3wH3-hR5bacmgHFBw.1",
        "name": "Direct Debit",
        "number": {
            "bban": "0001-245787654",
            "bbanParsed": {
                "accountNumber": "245787654",
                "bankCode": "0001"
            },
            "bbanType": "0001-245787654",
            "card": null,
            "iban": null
        },
        "owner": "Christian Thomsen",
        "type": "Consumption"
    },
    ]
}
```

Now that you've gotten account access, you can either proceed to access transactions from those accounts or to make payments. Please take note of the `id` of one of the accounts, as you will need it when proceeding.

Read on to learn about accessing transactions or jump straight to our [documentation on payments](https://docs.aiia.eu/#/payments/intro).

### Step 5 - Access transactions

By using the `id` of an account from Step 4, we can start pulling out user transactions by sending the following request on Postman:

```
    Data / List Transactions
``` 

This will produce a response with a list of transactions (default: 50 transactions) that looks like this:

```json
{
    "pagingToken": "...",
    "transactions": [
        {
            "accountId": "ZmExODkyNzEtZjk2NS00ZjVjLTk5Z6782tZTQ1YjczYmMyODM5fFRlc3REYXRhQmFuazF8bkx5dXRxZlYwdnkwaElSSW9wNnRDakVHenllUFMyem43UVl2LUpWT3YwUS4w",
            "amount": -291.0,
            "balance": {
                "currency": "DKK",
                "value": -3954.0
            },
            "creationDate": "0001-01-01T00:00:00",
            "currency": "DKK",  
            "date": "2019-09-02",
            "detail": { // You need to contact sales to get this info, otherwise it's just null
                "currencyConversion": null,
                "destination": {
                    "account": null,
                    "address": null,
                    "merchantCategoryCode": null,
                    "merchantCategoryName": null,
                    "name": "DSB Kastrup AUT    23228"
                },
                "executionDate": null,
                "identifiers": {
                    "creditorReference": null,
                    "document": null,
                    "endToEndId": null,
                    "reference": "0130Y9C6LY212",
                    "sequenceNumber": null,
                    "terminal": null
                },
                "message": null,
                "reward": null,
                "source": {
                    "account": {
                        "bban": null,
                        "bbanParsed": null,
                        "bbanType": null,
                        "card": {
                            "cardHolder": "Henrik Madsen",
                            "expireMonth": null,
                            "expireYear": null,
                            "maskedPan": "0524 XXXX XXXX 3413"
                        },
                        "iban": null
                    },
                    "address": null,
                    "merchantCategoryCode": null,
                    "merchantCategoryName": null,
                    "name": null
                },
                "valueDate": null
            },
            "id": "8f6b6b78-6e97-73ba-a6de-4a732fcff09bd",
            "nagApiTransactionId": null,
            "originalText": "DSB Kastrup AUT    23228",
            "state": "Booked",
            "text": "DSB Kastrup AUT",
            "transactionAmount": {
                "currency": "DKK",
                "value": -291.0
            },
            "type": "Card"
        }
    ]
}
```

Congratulations! You've successfully started your journey with Mastercard Open Banking Europe. 

## What's next?

Now that you've connected an account, you're all set to explore our API further 🚀
* [Access account information](https://docs.aiia.eu/#/accounts/information) – See more details on how to use accounts and transactions 🧭

* [Payments](https://docs.aiia.eu/#/payments/intro) – Discover our payment products and see how to get started 🧭

* [Event notifications](https://docs.aiia.eu/#/webhooks/introduction) – Explore how you can start receiving notifications. They'll give you a real-time experience by notifying you of any changes. They can be used for accounts, transactions and payments 🧭

* [API Reference](https://api.aiia.eu/latest/index.html) – Explore our API reference to see all the amazing things our API exposes to you 🧭

* [Sample projects](https://docs.aiia.eu/#/other/samples) – You can find several sample applications here to view the endless capabilities of Mastercard Open Banking Europe ✈️
