## **relay_tx**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"relay_tx","params":{"txids":[9fd75c429cbe52da9a52f2ffc5fbd107fe7fd2099c0d8de274dc8a67e0c98613]}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "status": "OK"
  }
}
```
Relay a list of transaction IDs.  
Alias: None.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *txids*   | array of string | list of transaction IDs to relay
|**Outputs:** | status    | string          | General RPC error code. "OK" means everything looks good.
