## **get_address_book**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address_book","params":{"entries":[0,1]}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_address_book",
      "params": {"entries": [0,1]},
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {"entries": [0,1]}
  rpc_connection.get_address_book(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "entries": [{
        "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
        "description": "Second account",
        "index": 0,
        "payment_id": "0000000000000000000000000000000000000000000000000000000000000000"
      },{
        "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
        "description": "Third account",
        "index": 1,
        "payment_id": "0000000000000000000000000000000000000000000000000000000000000000"
      }]
    }
  }
```
Retrieves entries from the address book.  
Alias: *None*.  

|             | Parameter     | Type                  | Description
| ---         | ---           | ---                   | ---
|**Inputs:**  | *entries*     | array of unsigned int | indices of the requested address book entries
|**Outputs:** | entries       |                       | array of entries:
|             | ..address     | string                | Public address of the entry
|             | ..description | string                | Description of this address entry
|             | ..index       | unsigned int          |
|             | ..payment_id  | string                |
