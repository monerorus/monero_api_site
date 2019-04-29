---
weight: 200
title: Wallet RPC API Reference
---

# Daemon RPC

<aside class="success">
Updated
</aside>

## Introduction

```python
  This part is the same for all methods and described just here.
  For each request you need define first this:
      import requests
      import json
      wallet_url = "http://127.0.0.1:18082/json_rpc"
      header = {"Content-Type": "application/json"}

  This part is different for all method and described below for each method.
  In data struct you set params for request, example:
      data = {
          "jsonrpc": "2.0",
          "id": "0",
          "method": "get_balance",
          "params": {"account_index": 0, "address_indices": [0, 1]},
      }

  This part is the same for all methods and described just here.
  For each request you get response like this:
      response = requests.post(wallet_url, data=json.dumps(data), headers=header)
      response.raise_for_status()
      response.json()
```
```py
  This part is the same for all methods and described just here.
  For each request you need define first:
      from monerorpc.authproxy import AuthServiceProxy
      rpc_connection = AuthServiceProxy('http://127.0.0.1:18082/json_rpc')
```

This is a list of the monerod daemon RPC calls, their inputs and outputs, and examples of each.

Many RPC calls use the daemon's JSON RPC interface while others use their own interfaces, as demonstrated below.

<aside class="notice">
"@atomic-units" refer to the smallest fraction of 1 XMR according to the monerod implementation. <br> <b>1 XMR = 1e12 @atomic-units.</b>
</aside>
<aside class="notice">
Guide updated as of network height of 1,562,465.
</aside>

## JSON RPC Methods

The majority of monerod RPC calls use the daemon's `json_rpc` interface to request various bits of information. These methods all follow a similar structure, for example:

<code>
IP=127.0.0.1  
PORT=18081  
METHOD='get_block_header_by_height'  
ALIAS='getblockheaderbyheight'  
PARAMS='{"height":912345}'  
curl \
    -X POST http://$IP:$PORT/json_rpc \
    -d '{"jsonrpc":"2.0","id":"0","method":"'$METHOD'","params":'$PARAMS'}' \
    -H 'Content-Type: application/json'
</code>

Some methods include parameters, while others do not. Examples of each JSON RPC method follow.