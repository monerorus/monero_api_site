---
weight: 805
---

## **get_tx_notes**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_notes","params":{"txids":["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_tx_notes",
      "params": {"txids": ["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"txids": ["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]}
  rpc_connection.get_tx_notes(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "notes": ["This is an example"]
    }
  }
```
Get string notes for transactions.  
Alias: *None*.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *txids*   | array of string | transaction ids
|**Outputs:** | notes     | array of string | notes for the transactions