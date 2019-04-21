## **get_languages**

```shell
  curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_languages"}' -H 'Content-Type: application/json'
```
```python
  ...^ see introduction
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_languages",
  }
  ...^ see introduction
```
```py
  ...^ see introduction
  rpc_connection.get_languages()
```
```json
  {
    "id": "0",
    "jsonrpc": "2.0",
    "result": {
      "languages": ["Deutsch","English","Espanol","Francais","Italiano","Nederlands","Portugues","пїЅпїЅпїЅпїЅпїЅпїЅпїЅ пїЅпїЅпїЅпїЅ","???","???? (??)","Esperanto","Lojban"]
    }
  }
```
Get a list of available languages for your wallet's seed.  
Alias: *None*.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *None*.   |                 |
|**Outputs:** | languages | array of string | List of available languages
