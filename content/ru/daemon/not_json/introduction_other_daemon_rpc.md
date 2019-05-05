---
weight: 300
title: Wallet RPC API Reference
---

# Other Daemon RPC Calls
```python
  #This part is the same for all methods and described just here.
  #For each request you need define first this:
      import requests
      import json
      header = {"Content-Type": "application/json"}

  #This part is different for all method and described below for each method.
  #In data struct you set params for request, example:
      url = "http://127.0.0.1:18081/set_limit"
      data = {"limit_down": 1024}

  #This part is the same for all methods and described just here.
  #For each request you get response like this:
      response = requests.post(url, data=json.dumps(data), headers=header)
      response.raise_for_status()
      response.json()
```
Not all daemon RPC calls use the JSON_RPC interface. This section gives examples of these calls.

The data structure for these calls is different than the JSON RPC calls. Whereas the JSON RPC methods were called using the `/json_rpc` extension and specifying a method, these methods are called at their own extensions. For example:  
<code>
    IP=127.0.0.1
    PORT=18081
    METHOD='gettransactions'
	PARAMS='{"txs_hashes":["d6e48158472848e6687173a91ae6eebfa3e1d778e65252ee99d7515d63090408"]}'
	curl \
		-X POST http://$IP:$PORT/$METHOD \
		-d $PARAMS \
		-H 'Content-Type: application/json'
</code>

<aside class="notice">
It is recommended to use JSON RPC where such alternatives exist, rather than the following methods. For example, the recommended way to get a node's height is via the JSON RPC methods [get_info](#getinfo) or [get_last_block_header](#get-last-block-header), rather than [getheight](#getheight) below.
</aside>

For calls that end with **.bin**, the data is exchanged in the form of binary, serialized objects, as defined in the [Core RPC Server](https://github.com/monero-project/monero/blob/master/src/rpc/core_rpc_server_commands_defs.h).
