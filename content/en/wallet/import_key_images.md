---
weight: 805
---

## **import_key_images**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_key_images", "params":{"signed_key_images":[{"key_image":"cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876","signature":"c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00"},{"key_image":"65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19","signature":"c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c"}]}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "import_key_images",
      "params": {
          "signed_key_images": [
              {
                  "key_image": "cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876",
                  "signature": "c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00",
              },
              {
                  "key_image": "65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19",
                  "signature": "c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c",
              },
          ]
      },
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {
      "signed_key_images": [
          {
              "key_image": "cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876",
              "signature": "c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00",
          },
          {
              "key_image": "65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19",
              "signature": "c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c",
          },
      ]
  }
  rpc_connection.import_key_images(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "height": 76428,
      "spent": 62708953408711,
      "unspent": 0
    }
  }
```
Import signed key images list and verify their spent status.  
Alias: *None*.  

|             | Parameter           | Type         | Description
| ---         | ---                 | ---          | ---
|**Inputs:**  | *signed_key_images* |              | array of signed key images:
|             | ..*key_image*       | string       |
|             | ..*signature*       | string       |
|**Outputs:** | height              | unsigned int |
|             | spent               | unsigned int | Amount (in @atomic|units) spent from those key images.
|             | unspent             | unsigned int | Amount (in @atomic|units) still available from those key images.