# Payment

## PaymentMethod
- QIWIVISAMASTER - for credit card
- QIWI - for phone

## Create Payment
```
POST: /api/v4/payment/create
```
Default config, emailConfig: { client: true merchant: true }.

In order to send, only set the value of the merchant to false for the client.

In order to send, only set the client to the merchant, set the value of the client to false.

The email is used to send emails about successful payment
### Request Parameters
#### Header
| Name | Type | Desc |
| :------ | :------ | :------ |
| `assetux-v4-token` | `string` | `Generic token`
#### Body
| Name | Type | Desc |
| :------ | :------ | :------ |
| `lang` | `string` | `Support ru/en`
| `emailConfig` | `Object \| undefined`
| `paymentMethod` | `string` | [`Type`](#paymentmethod)
| `email` | `string` | `Client email`
| `creditCart` | `string` | `Number Credit Card or Phone`

### Response
Status 200 - OK
```ts
{
   success: true,
   data: {
      id: String, // uuid
      emailToMerchant: boolean,
      emailToClient: boolean,
      linkToPayment: String
   }
}
```
Status 400 - Bad Request
```ts
{
   success: false,
   data: {
      message: String
   }
}
```

## CallBack
Callback url set manually, via ASSETUX support (telegram, facebook, otc...)

```
POST: custom url
```
If the response status isn't 200, send a repeat callback after 15 minutes.

### Request Parameters
#### Header
| Name | Type | Desc |
| :------ | :------ | :------ |
| `signature` | `string` | `Encrypt amount + id with callback token`
#### Body
| Name | Type | Desc |
| :------ | :------ | :------ |
| `email` | `string` | `Client email`
| `amount` | `number` | `Sum payment`
| `id` | `number` | `Payment id`

### Response
Status 200 - OK