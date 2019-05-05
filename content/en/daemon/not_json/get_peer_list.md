---
weight: 305
---

## **/get_peer_list**

> Example (truncated lists):

```shell
$ curl -X POST http://127.0.0.1:18081/get_peer_list -H 'Content-Type: application/json'
```
```python
  #...^ see introduction
  url = "http://127.0.0.1:18081/get_peer_list"
  #...^ see introduction
```
```json
{
  "gray_list": [{
    "host": "640304833",
    "id": 5345237316225602120,
    "ip": 640304833,
    "last_seen": 1525540510,
    "port": 18080
  },{
    "host": "2183731038",
    "id": 14955030573998424430,
    "ip": 2183731038,
    "last_seen": 1525540499,
    "port": 28080
  }, ...
  ],
  "status": "OK",
  "white_list": [{
    "host": "1221637955",
    "id": 10354694710033118926,
    "ip": 1221637955,
    "last_seen": 1525540511,
    "port": 18080
  },{
    "host": "1780407354",
    "id": 17193661050352240890,
    "ip": 1780407354,
    "last_seen": 1525540510,
    "port": 18080
  }, ...
  ]
}
```
Get the known peers list.  
Alias: None.  

|             | Parameter   | Type         | Description
| ---         | ---         | ---          | ---
|**Inputs:**  | *None*.     |              |
|**Outputs:** | gray_list   |              | array of offline *peer* structure as follows:
|             | ..host      | unsigned int | IP address in integer format
|             | ..id        | string       | Peer id
|             | ..ip        | unsigned int | IP address in integer format
|             | ..last_seen | unsigned int | unix time at which the peer has been seen for the last time
|             | ..port      | unsigned int | TCP port the peer is using to connect to monero network.
|             | status      | string       | General RPC error code. "OK" means everything looks good. Any other value means that something went wrong.
|             | white_list  |              | array of online *peer* structure, as above.