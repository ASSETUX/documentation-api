## Go
```go
package main

import (
	"fmt"
	"strings"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://bsc.assetux.com/api/v4/payment/create"

	payload := strings.NewReader("{\n  \"amountIn\": 500,\n  \"currency\": \"KZT\",\n  \"paymentMethod\": \"QIWIVISAMASTER\",\n  \"creditCard\": \"2200220022002200\",\n  \"email\": \"support@assetux.com\",\n  \"lang\": \"en\"\n}")

	req, _ := http.NewRequest("POST", url, payload)

	req.Header.Add("assetux-v4-token", "RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni")
	req.Header.Add("Content-Type", "application/json")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```

## NodeJs
```js
const axios = require("axios").default;

const options = {
  method: 'POST',
  url: 'https://bsc.assetux.com/api/v4/payment/create',
  headers: {'assetux-v4-token': 'RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni', 'Content-Type': 'application/json'},
  data: {
    amountIn: 500,
    currency: 'KZT',
    paymentMethod: 'QIWIVISAMASTER',
    creditCard: '2200220022002200',
    email: 'support@assetux.com',
    lang: 'en'
  }
};

axios.request(options)
  .then(function (response) {
    console.log(response.data);
  })
  .catch(function (error) {
    console.error(error);
  });
```

## Python
```python
import requests

url = "https://bsc.assetux.com/api/v4/payment/create"

payload = {
    "amountIn": 500,
    "currency": "KZT",
    "paymentMethod": "QIWIVISAMASTER",
    "creditCard": "2200220022002200",
    "email": "support@assetux.com",
    "lang": "en"
}
headers = {
    "assetux-v4-token": "RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni",
    "Content-Type": "application/json"
}

response = requests.request("POST", url, json=payload, headers=headers)

print(response.text)
```

## curl
```curl
curl -XPOST 'https://bsc.assetux.com/api/v4/payment/create' \
     -H 'assetux-v4-token: RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni' \
     -H 'Content-Type: application/json' \
     -d '{"amountIn":500,"currency":"KZT","paymentMethod":"QIWIVISAMASTER","creditCard":"2200220022002200","email":"support@assetux.com","lang":"en"}' \
     --compressed
```


## HTTP
```http
POST /api/v4/payment/create HTTP/1.1
Assetux-V4-Token: RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni
Content-Type: application/json
Host: https://bsc.assetux.com
Content-Length: 150

{
  "amountIn": 500,
  "currency": "KZT",
  "paymentMethod": "QIWIVISAMASTER",
  "creditCard": "2200220022002200",
  "email": "support@assetux.com",
  "lang": "en"
}
```
