---
weight: 815
---

## **get_address_index**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address_index","params":{"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_address_index",
      "params": {
          "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"
      },
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  params = {
      "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"
  }
  rpc_connection.get_address_index(params)
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "index": {
        "major": 0,
        "minor": 1
      }
    }
  }
```
Get account and address indexes from a specific (sub)address  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *address* | string       | (sub)address to look for.
|**Outputs:** | index     |              | subaddress informations
|             | ..major   | unsigned int | Account index.
|             | ..minor   | unsigned int | Address index.
