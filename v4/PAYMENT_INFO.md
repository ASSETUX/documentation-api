### PAYMENTMETHOD
- QIWI - to pay with a phone number 
- QIWIVISAMASTER - to pay with a card 
### List of currencies and supported payment methods
* RUB - QIWI, QIWIVISAMASTER
* KZT - QIWIVISAMASTER
* EUR - QIWIVISAMASTER
* USD - QIWIVISAMASTER
* UAH - QIWIVISAMASTER

## Email config
This is the configuration object for sending emails.

If you want us to send emails, set all values to true.

This is the object :
```json
{
  emailToClient: boolean,
  emailToMerchant: boolean
}
```

## Customer
Customer, this is the data from the Card Holder. This field is required for such currencies as: EUR, USD.
Transmitted in the format:
```json
{
  "customer": {
    "firstName": "FIRST",
    "lastName": "LAST"
  }
}
```

## Language
Supported language:
* ru
* en

## Check card
The card is checked by bin number.

Only 3 answers: VISA and MASTERCARD, Unsupported. They mean that payment by card from the country of card being issued is not supported for the specified currency.

If the specified bin does not exist, an error will be thrown: "Invalid parameter for creditCard Specified bin not found."

#### Rules

List of countries we do not work with on Visa (EURO & USD):
Afghanistan, Central African Republic, Republic of Congo, Democratic Republic of Congo, Libya, Mali, Myanmar, Pakistan, North Korea, Palestine, Sudan, South Sudan, Somalia, Syria, Venezuela, Yemen, Zimbabwe, Trinidad and Tobago, Bahamas, Mongolia, Ghana, Algeria, Bolivia, Ecuador, Egypt, Morocco, Nepal, Qatar, United Arab Emirates, Western Sahara, USA, Turkey, China, Puerto Rico, Russia, Belarus.

List of countries we work with on Mastercard (EURO & USD):
Austria, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Ireland, Italy, Latvia, Liechtenstein, Lithuania, Luxembourg, Malta, Netherlands, Poland, Portugal, Romania, Slovakia, Slovenia, Spain, Sweden, Ukraine, UK

KZT: Deposits are supported only from cards of banks issued in Kazakhstan

RUB: deposits are supported only with the cards of banks of the payment system "MIR" issued in Russia

UAH: deposits are supported only with cards of banks issued in Ukraine


## Info
* bin - first 6 digits of the card.
