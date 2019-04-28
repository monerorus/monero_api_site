---
weight: 805
---

## **query_key**

> Example (Query view key):

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"query_key","params":{"key_type":"view_key"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "query_key",
      "params": {"key_type": "view_key"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"key_type": "view_key"}
  rpc_connection.query_key(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "key": "0a1a38f6d246e894600a3e27238a064bf5e8d91801df47a17107596b1378e501"
    }
  }
```
> Example (Query mnemonic key):


```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"query_key","params":{"key_type":"mnemonic"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "query_key",
      "params": {"key_type": "mnemonic"},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"key_type": "mnemonic"}
  rpc_connection.query_key(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "key": "vocal either anvil films dolphin zeal bacon cuisine quote syndrome rejoices envy okay pancakes tulips lair greater petals organs enmity dedicated oust thwart tomorrow tomorrow"
    }
  }
```
Return the spend or view private key.  
Alias: *None*.  

|             | Parameter  | Type   | Description
| ---         | ---        | ---    | ---
|**Inputs:**  | *key_type* | string | Which key to retrieve: "mnemonic" - the mnemonic seed (older wallets do not have one) OR "view_key" - the view key
|**Outputs:** | key        | string | The view key will be hex encoded, while the mnemonic will be a string of words.