---
weight: 205
---

## **hard_fork_info**

```shell
$ curl -X POST http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"hard_fork_info"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "hard_fork_info",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.hard_fork_info()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "earliest_height": 1009827,
    "enabled": false,
    "state": 2,
    "status": "OK",
    "threshold": 0,
    "version": 1,
    "votes": 7277,
    "voting": 2,
    "window": 10080
  }
}
```
Look up information regarding hard fork voting and readiness.  
Alias: None.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *None*.         |              |
|**Outputs:** | earliest_height | unsigned int | Block height at which hard fork would be enabled if voted in.
|             | enabled         | boolean      | Tells if hard fork is enforced.
|             | state           | unsigned int | Current hard fork state: 0 (There is likely a hard fork), 1 (An update is needed to fork properly), or 2 (Everything looks good).
|             | status          | string       | General RPC error code. "OK" means everything looks good.
|             | threshold       | unsigned int | Minimum percent of votes to trigger hard fork. Default is 80.
|             | version         | unsigned int | The major block version for the fork.
|             | votes           | unsigned int | Number of votes towards hard fork.
|             | voting          | unsigned int | Hard fork voting status.
|             | window          | unsigned int | Number of blocks over which current votes are cast. Default is 10080 blocks.
