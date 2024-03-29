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

	url := "https://bsc.assetux.com/api/ecommerce/payment"

	payload := strings.NewReader("{\n \"tokenAddress\": \"0x55d398326f99059fF775485246999027B3197955 \",\n \"currency\": \"USD\",\n \"amount\": 1200,\n \"chainId\": 56,\n \"cryptoAddress\": \"0x970609bA2C160a1b491b90867681918BDc9773aF \",\n \"email\": \"support@assetux.com\",\n \"method\": \"VISAMASTER\",\n ")

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
  url: 'https://bsc.assetux.com/api/ecommerce/paymen',
  headers: {'assetux-v4-token': 'RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni', 'Content-Type': 'application/json'},
  data: {
	tokenAddress: "0x55d398326f99059fF775485246999027B3197955 ",
	currency": "USD",
	amount": 1200,
	chainId: 56,
	cryptoAddress: "0x970609bA2C160a1b491b90867681918BDc9773aF",
	email: "test@test.com",
	method: "VISAMASTER"
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

url = "https://bsc.assetux.com/api/ecommerce/payment"

payload = {
	"tokenAddress": "0x55d398326f99059fF775485246999027B3197955 ",
	"currency": "USD",
	"amount": 1200,
	"chainId": 56,
	"cryptoAddress": "0x970609bA2C160a1b491b90867681918BDc9773aF",
	"email": "test@test.com",
	"method": "VISAMASTER"
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
curl -XPOST 'https://bsc.assetux.com/api/ecommerce/payment' \
     -H 'assetux-v4-token: RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni' \
     -H 'Content-Type: application/json' \
     -d '{"tokenAddress": "0x55d398326f99059fF775485246999027B3197955 ", "currency": "USD", "amount": 1200, "chainId": 56, "cryptoAddress": "0x970609bA2C160a1b491b90867681918BDc9773aF", "email": "test@test.com", "method": "VISAMASTER"}' \
     --compressed
```


## HTTP
```http
POST /api/ecommerce/payment HTTP/1.1
Assetux-V4-Token: RYXwLOxxkKIYb165ZPEebSmJhO6RP1ni
Content-Type: application/json
Host: https://bsc.assetux.com
Content-Length: 150

{
	"tokenAddress": "0x55d398326f99059fF775485246999027B3197955 ",
	"currency": "USD",
	"amount": 1200,
	"chainId": 56,
	"cryptoAddress": "0x970609bA2C160a1b491b90867681918BDc9773aF",
	"email": "test@test.com",
	"method": "VISAMASTER"
}
```
