---
weight: 205
---

## **get_output_histogram**


```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_output_histogram","params":{"amounts":[20000000000]}}' -H 'Content-Type: application/json'
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "histogram": [{
      "amount": 20000000000,
      "recent_instances": 0,
      "total_instances": 381458,
      "unlocked_instances": 0
    }],
    "status": "OK",
    "untrusted": false
  }
}
```
Get a histogram of output amounts. For all amounts (possibly filtered by parameters), gives the number of outputs on the chain for that amount.
RingCT outputs counts as 0 amount.
Alias: None

|             | Parameter            | Type                 | Description
| ---         | ---                  | ---                  | ---
|**Inputs:**  | *amounts*            | list of unsigned int |
|             | *min_count*          | unsigned int         |
|             | *max_count*          | unsigned int         |
|             | *unlocked*           | boolean              |
|             | *recent_cutoff*      | unsigned int         |
|**Outputs:** | histogram            |                      |list of histogram entries, in the following structure:
|             | ..amount             | unsigned int         | Output amount in @atomic-units
|             | ..total_instances    | unsigned int         |
|             | ..unlocked_instances | unsigned int         |
|             | ..recent_instances   | unsigned int         |
|             | status               | string               | General RPC error code. "OK" means everything looks good.
|             | untrusted            | boolean              | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
