---
weight: 805
---

## **rescan_blockchain**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"rescan_blockchain"}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "rescan_blockchain",
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  rpc_connection.rescan_blockchain()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Rescan the blockchain from scratch, losing any information which can not be recovered from the blockchain itself.  
This includes destination addresses, tx secret keys, tx notes, etc.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |