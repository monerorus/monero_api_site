---
weight: 805
---

## **delete_address_book**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"delete_address_book","params":{"index":1}}' -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "delete_address_book",
      "params": {"index": 1},
  }
  #...^ see introduction
```
```py
  #...^ see introduction
  params = {"index": 1}
  rpc_connection.delete_address_book(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
    }
  }
```
Delete an entry from the address book.  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *index*   | unsigned int | The index of the address book entry.
|**Outputs:** | *None*.   |              |