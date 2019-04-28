---
weight: 205
---

## **get_output_distribution**

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_output_distribution","params":{"amounts":[628780000],"from_height":1462078}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "distributions": [{
      "amount": 2628780000,
      "base": 0,
      "distribution": "",
      "start_height": 1462078
    }],
    "status": "OK"
  }
}
```
Alias: None.  

|             | Parameter      | Type                  | Description
| ---         | ---            | ---                   | ---
|**Inputs:**  | *amounts*      | array of unsigned int | amounts to look for
|             | *cumulative*   | boolean               | (optional, default is `false`) States if the result should be cumulative (`true`) or not (`false`)
|             | *from_height*  | unsigned int          | (optional, default is 0) starting height to check from
|             | *to_height*    | unsigned int          | (optional, default is 0) ending height to check up to
|**Outputs:** | distributions  |                       | array of structure distribution as follows:
|             | ..amount       | unsigned int          |
|             | ..base         | unsigned int          |
|             | ..distribution | array of unsigned int |
|             | ..start_height | unsigned int          |
|             | status         | string                | General RPC error code. "OK" means everything looks good.
