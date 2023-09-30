### FAQ
- [PAYMENTMETHOD](PAYMENT_INFO.md#paymentmethod)
- [List of currencies and supported payment methods](PAYMENT_INFO.md#paymentmethod)
- [Examples of creating an payment in different programming languages](PAYMENT_CREATE_EXAMPLE.md)
- [EmailConfig](PAYMENT_INFO.md#email-config)
- [Lang](PAYMENT_INFO.md#language)
- [Customer](PAYMENT_INFO.md#customer)
- [Redirect Link](PAYMENT_INFO.md#redirect-link)
- [Status code](PAYMENT_INFO.md#status-code)

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
        fiat: "USD";
        amountFiat: number;
        amountCrypto: number;
        status: StatusEcommercePayment;      // ['CREATED' | 'PENDING' | 'EXPIRED' | 'COMPLETE' | 'ERROR']
        chainId: number;
        url: string;                         // payment link
        cryptoAddress: string;
        email: string;
        rate: number;
        paymentData: {
            ...;
        };
        user: {
            ...;
        };
        token: {
            ...;
        };
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
#### 5. Incorrect API KEY

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
