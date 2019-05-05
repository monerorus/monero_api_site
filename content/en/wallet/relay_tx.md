---
weight: 805
---

## **relay_tx**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"relay_tx","params":{"hex":"#...^ see introductiontx_metadata#...^ see introduction"}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "relay_tx",
      "params": {"hex": "#...^ see introductiontx_metadata#...^ see introduction"},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"hex": "#...^ see introductiontx_metadata#...^ see introduction"}
  rpc_connection.relay_tx(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "tx_hash": "1c42dcc5672bb09bccf33fb1e9ab4a498af59a6dbd33b3d0cfb289b9e0e25fa5"
    }
  }
```
Relay a transaction previously created with `"do_not_relay":true`.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *hex*     | string | transaction metadata returned from a `transfer` method with `get_tx_metadata` set to `true`.
|**Outputs:** | tx_hash   |        | String for the publically searchable transaction hash.