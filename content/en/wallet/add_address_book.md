---
weight: 805
---

## **add_address_book**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"add_address_book","params":{"address":"78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j","description":"Third account"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "add_address_book",
      "params": {
          "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
          "description": "Third account",
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
      "description": "Third account",
  }
  rpc_connection.add_address_book(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "index": 1
    }
  }
```
Add an entry to the address book.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *address*     | string       |
|             | *payment_id*  |              | (optional) string, defaults to "0000000000000000000000000000000000000000000000000000000000000000";
|             | *description* |              | (optional) string, defaults to "";
|**Outputs:** | index         | unsigned int | The index of the address book entry.