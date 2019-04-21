## **store**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"store"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "store"
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.store()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Save the wallet file.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |
