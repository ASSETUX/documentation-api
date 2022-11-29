### FAQ
- [PAYMENTMETHOD](PAYMENT_INFO.md#paymentmethod)
- [List of currencies and supported payment methods](PAYMENT_INFO.md#paymentmethod)
- [Examples of creating an payment in different programming languages](PAYMENT_CREATE_EXAMPLE.md)
- [EmailConfig](PAYMENT_INFO.md#email-config)
- [Lang](PAYMENT_INFO.md#language)
- [Customer](PAYMENT_INFO.md#customer)

## Create payment
 - Request Method: POST
 - Request Path: /api/v4/payment/create

### Request Description

### Request

#### Headers

| Name            | Required | Description     
|-----------------|----------|-----------------
| assetux-v4-token | √        | Token                 
| Content-Type    | √        | application/json                 


#### Request Payload

 - Content-Type: application/json


```json
{
    "amountIn": number,
    "currency": string,
    "paymentMethod": PAYMENTMETHOD,
    "creditCard": string,
    "emailConfig": EmailConfig,
    "customer": {
      "firstName": string,
      "lastName": string
    },
    "email": string,
    "txnId": string,
    "lang": string
}
```

### Example Response

#### 1. Success.

 - Status Code: 200 OK
 - Content-Type: application/json; charset=utf-8


```json
{
    "success": true,
    "data": {
        "id": "acb63380-fba7-480d-a5d9-57acdc9afa61",
        "emailToMerchant": true,
        "emailToClient": true,
        "linkToPayment": "https://payment.whitebit.com/hpp/cgi_a3IcgIId3xaxnnt",
        "txnId": "s5412fz471f3vs1f27v1f357"
    }
}
```
#### 2. Check Card.

 - Status Code: 400 Bad Request
 - Content-Type: application/json; charset=utf-8


```json
{
    "success": false,
    "data": {
        "message": "Invalid parameter for creditCard Specified bin not found"
    }
}
```

#### 2. Check Card.

 - Status Code: 400 Bad Request
 - Content-Type: application/json; charset=utf-8


```json
{
    "success": false,
    "data": {
        "message": {
            "type": "MASTERCARD"
        }
    }
}
```

#### 3. Wrong payment amount

 - Status Code: 400 Bad Request
 - Content-Type: application/json; charset=utf-8


```json
{
    "success": false,
    "data": {
        "message": "Invalid amount"
    }
}
```

#### 4. Incorrect token.

 - Status Code: 401 Unauthorized
 - Content-Type: application/json; charset=utf-8


```json
{
    "success": false,
    "data": {
        "message": "Dont valid token"
    }
}
```

## CallBack
Callback url set manually, via ASSETUX support (telegram, facebook, otc...)

```
POST: custom url
```
If the response status isn't 200, send a repeat callback after 15 minutes.

signature - encrypted data to check if the request body matches the sent data. 

### Request Parameters
#### Header
| Name | Type | Desc |
| :------ | :------ | :------ |
| `signature` | `string` | `id:txnId:amount`
#### Body
| Name | Type | Desc |
| :------ | :------ | :------ |
| `email` | `string` | `Client email`
| `amount` | `number` | `Sum payment`
| `id` | `number` | `Payment id`
| `txnId` | `string` | `Transaction's client ID (assigned on the client device)`
| `currency` | `string` | `Currency of the made payment`
| `feeAmount` | `number` | `Payment fee`

### Response
Status 200 - OK
```
{}
```
