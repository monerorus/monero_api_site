---
weight: 200
title: Wallet RPC API Reference
---

# Daemon RPC

<aside class="success">
Updated
</aside>

## Introduction

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