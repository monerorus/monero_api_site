---
weight: 205
---

## **get_fee_estimate**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_fee_estimate"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_fee_estimate",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.get_fee_estimate()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "fee": 187610000,
    "status": "OK",
    "untrusted": false
  }
}
```
Gives an estimation on fees per kB.  
Alias: None.  
|             | Parameter      | Type         | Description
| ---         | ---            | ---          | ---
|**Inputs:**  | *grace_blocks* | unsigned int | Optional
|**Outputs:** | fee            | unsigned int | Amount of fees estimated per kB in @atomic-units
|             | status         | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted      | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
