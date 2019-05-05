---
weight: 805
---

## **get_height**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_height"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_height",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.get_height()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "height": 145545
    }
  }
```
Returns the wallet's current block height.  
Alias: *getheight*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | height    | unsigned int | The current monero-wallet-rpc's blockchain height. If the wallet has been offline for a long time, it may need to catch up with the daemon.