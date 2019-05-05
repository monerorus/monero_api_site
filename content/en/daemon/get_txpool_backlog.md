---
weight: 205
---

## **get_txpool_backlog**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_txpool_backlog"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_txpool_backlog",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.get_txpool_backlog()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "backlog": "...Binary...",
    "status": "OK",
    "untrusted": false
  }
}
```
Get all transaction pool backlog  
Alias: None.  

|             | Parameter      | Type                          | Description
| ---         | ---            | ---                           | ---
|**Inputs:**  | *None*.        |                               |
|**Outputs:** | backlog:       |                               | array of structures *tx_backlog_entry* (in binary form):
|             | ..blob_size    | unsigned int (in binary form) |
|             | ..fee          | unsigned int (in binary form) |
|             | ..time_in_pool | unsigned int (in binary form) |
|             | status         | string                        | General RPC error code. "OK" means everything looks good.
|             | untrusted      | boolean                       | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
