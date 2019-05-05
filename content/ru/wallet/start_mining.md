---
weight: 805
---

## **start_mining**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"start_mining","params":{"threads_count":1,"do_background_mining":true,"ignore_battery":false}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "start_mining",
      "params": {"threads_count": 1, "do_background_mining": True, "ignore_battery": False},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"threads_count": 1, "do_background_mining": True, "ignore_battery": False}
  rpc_connection.start_mining(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Start mining in the Monero daemon.  
Alias: *None*.  

|             | Parameter              | Type         | Description
| ---         | ---                    | ---          | ---
|**Inputs:**  | *threads_count*        | unsigned int | Number of threads created for mining.
|             | *do_background_mining* | boolean      | Allow to start the miner in @smart-mining mode.
|             | *ignore_battery*       | boolean      | Ignore battery status (for @smart-mining only)
|**Outputs:** | *None*.                |              |