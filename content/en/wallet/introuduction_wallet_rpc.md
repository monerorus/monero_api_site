---
weight: 800
title: Wallet RPC API Reference
---

# Wallet RPC 

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

This is a list of the monero-wallet-rpc calls, their inputs and outputs, and examples of each. The program monero-wallet-rpc replaced the rpc interface that was in simplewallet and then monero-wallet-cli.  
All monero-wallet-rpc methods use the same JSON RPC interface. For example:  
<code>
IP=127.0.0.1  
PORT=18082  
METHOD="make_integrated_address"  
PARAMS="{\"payment_id\":\"1234567890123456789012345678900012345678901234567890123456789000\"}"
curl \
    -X POST http://$IP:$PORT/json_rpc \
    -d '{"jsonrpc":"2.0","id":"0","method":"'$METHOD'","params":'"$PARAMS"'}' \
    -H 'Content-Type: application/json'
</code>

If the monero-wallet-rpc was executed with the `--rpc-login` argument as `username:password`, then follow this example:  
<code>
IP=127.0.0.1  
PORT=18082  
METHOD="make_integrated_address"  
PARAMS="{\"payment_id\":\"1234567890123456789012345678900012345678901234567890123456789000\"}"  
curl \
    -u username:password --digest \
    -X POST http://$IP:$PORT/json_rpc \
    -d '{"jsonrpc":"2.0","id":"0","method":"'$METHOD'","params":'"$PARAMS"'}' \
    -H 'Content-Type: application/json'
</code>

<aside class="notice">
"@atomic-units" refer to the smallest fraction of 1 XMR according to the monerod implementation.  <br>
<b>1 XMR = 1e12 @atomic-units.</b>
</aside> 

This list has been updated on a frozen code on 2018-09-14 after merged commit bb30a7236725e456138f055f96a634c75ce2b491 (Wallet RPC version 1.3), and at block height 1643308.

## JSON RPC Methods: