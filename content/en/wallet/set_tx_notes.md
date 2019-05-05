---
weight: 805
---

## **set_tx_notes**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_tx_notes","params":{"txids":["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"],"notes":["This is an example"]}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "set_tx_notes",
      "params": {
          "txids": [
              "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"
          ],
          "notes": ["This is an example"],
      },
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {
      "txids": [
          "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"
      ],
      "notes": ["This is an example"],
  }
  rpc_connection.set_tx_notes(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Set arbitrary string notes for transactions.  
Alias: *None*.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *txids*   | array of string | transaction ids
|             | *notes*   | array of string | notes for the transactions
|**Outputs:** | *None*.   |                 |