---
weight: 805
---

## **refresh**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"refresh","params":{"start_height":100000}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "refresh",
      "params": {"start_height": 100000},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"start_height": 100000}
  rpc_connection.refresh(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "blocks_fetched": 24,
      "received_money": true
    }
  }
```
Refresh a wallet after openning.  
Alias: *None*.  

|             | Parameter      | Type         | Description
| ---         | ---            | ---          | ---
|**Inputs:**  | *start_height* | unsigned int | (Optional) The block height from which to start refreshing.
|**Outputs:** | blocks_fetched | unsigned int | Number of new blocks scanned.
|             | received_money | boolean      | States if transactions to the wallet have been found in the blocks.