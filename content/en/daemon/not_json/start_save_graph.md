---
weight: 305
---

## **/start_save_graph**

```shell
$ curl -X POST http://127.0.0.1:18081/start_save_graph -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  url = "http://127.0.0.1:18081/start_save_graph"
  ...^ see introduction
```
```json
{
  "status": "OK"
}
```
Obsolete. Conserved here for reference.  
Alias: None.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *None*.   |        |
|**Outputs:** | status    | string | General RPC error code. "OK" means everything looks good.