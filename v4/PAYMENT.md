## Create payment
 - Request Method: POST
 - Request Path: /api/ecommerce/payment/

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
   "tokenAddress": "0x55d398326f99059fF775485246999027B3197955", // Token's address in blockchain
   "currency": "USD", // Only USD available now
   "amount": 1200, // Amount of USD
   "chainId": 56, // Token's chain ID
   "cryptoAddress": "0xdeadbeef", // Your wallet's public address
   "email": "test@test.com", // Your email
   "method": "VISAMASTER" // Only VISAMASTER available now
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
        "fiat": "USD",
        "amountFiat": 1200,
        "amountCrypto": 1190,
        "status": "CREATED",
        "chainId": 56,
        "url": "https://payment.link/",
        "cryptoAddress": "0xdeadbeef",
        "email": "test@test.com",
        "rate": null,
        "paymentData": {
            ...
        }
    }
}
```

#### 2. Incorrect API KEY

 - Status Code: 403 Forbidden
 - Content-Type: application/json; charset=utf-8

```json
{
    "success": false,
    "data": {
        "message": "Forbidden Incorrect API key"
    }
}
```

## Successful CallBack
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
| `data.id` | `number` | `Payment id`
| `data.amountFiat` | `number` | `Sum payment`
| `data.amountCrypto` | `number` | `Amount of crypto`
| `data.currency` | `string` | `Currency of the made payment`

### Response
Status 200 - OK
```
{}
```

## Canceled Callback
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
| `signature` | `string` | `id:txnId`
#### Body
| Name | Type | Desc |
| :------ | :------ | :------ |
| `data.id` | `number` | `Payment id`
| `data.txnId` | `string` | `Transaction's client ID (assigned on the client device)`
| `data.code` | `string` | `Status code of payment`

### Response
Status 200 - OK
```
{}
```
