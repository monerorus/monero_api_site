## **/get_info (not JSON)**

This method is a convenient backward support and should not be used anymore. See [get_info](#get-info) JSON RPC for details.  
Alias:

* **/getinfo**
* **get_info**


## **/get_limit**

```shell
$ curl -X POST http://127.0.0.1:18081/get_limit -H 'Content-Type: application/json'
```
```json
{
  "limit_down": 8192,
  "limit_up": 128,
  "status": "OK",
  "untrusted": false
}
```
Get daemon bandwidth limits.  
Alias: None.  

|             | Parameter  | Type         | Description
| ---         | ---        | ---          | ---
|**Inputs:**  | *None*.    |              |
|**Outputs:** | limit_down | unsigned int | Download limit in kBytes per second
|             | limit_up   | unsigned int | Upload limit in kBytes per second
|             | status     | string       | General RPC error code. "OK" means everything looks good.
|             | untrusted  | boolean      | States if the result is obtained using the bootstrap mode, and is therefore not trusted (`true`), or when the daemon is fully synced (`false`).
