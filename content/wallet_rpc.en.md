---
weight: 10
title: Wallet RPC API Reference
---

# Wallet RPC 

<aside class="success">
Updated
</aside>

## Introduction

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


## **get_balance**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_balance","params":{"account_index":0,"address_indices":[0,1]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
import requests
import json


wallet_url = "http://127.0.0.1:18082/json_rpc"
header = {"Content-Type": "application/json"}

data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_balance",
    "params": {"account_index": 0, "address_indices": [0, 1]},
}
response = requests.post(wallet_url, data=json.dumps(data), headers=header)
response.raise_for_status()
response.json()
```
##### python; python-monerorpc:
```python
from monerorpc.authproxy import AuthServiceProxy


rpc_connection = AuthServiceProxy('http://127.0.0.1:18082/json_rpc')
params = {"account_index": 0, "address_indices": [0, 1]}
rpc_connection.get_balance(params)
```

```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "balance": 157443303037455077,
    "multisig_import_needed": false,
    "per_subaddress": [{
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "address_index": 0,
      "balance": 157360317826255077,
      "label": "Primary account",
      "num_unspent_outputs": 5281,
      "unlocked_balance": 157360317826255077
    },{
      "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      "address_index": 1,
      "balance": 59985211200000,
      "label": "",
      "num_unspent_outputs": 1,
      "unlocked_balance": 59985211200000
    }],
    "unlocked_balance": 157443303037455077
  }
}
```
Return the wallet's balance.  
Alias: *getbalance*.  

|             | Parameter              | Type                            | Description
| ---         | ---                    | ---                             | ---
|**Inputs:**  | *account_index*        | unsigned int                    | Return balance for this account.
|             | *address_indices*      | array of unsigned int           | (Optional) Return balance detail for those subaddresses.
|**Outputs:** | balance                | unsigned int                    | The total balance of the current monero|wallet|rpc in session.
|             | unlocked_balance       | unsigned int                    | Unlocked funds are those funds that are sufficiently deep enough in the Monero blockchain to be considered safe to spend.
|             | multisig_import_needed | boolean                         | True if importing multisig data is needed for returning a correct balance.
|             | per_subaddress         | array of subaddress information | Balance information for each subaddress in an account.
|             | ..address_index        | unsigned int                    | Index of the subaddress in the account.
|             | ..address              | string                          | Address at this index. Base58 representation of the public keys.
|             | ..balance              | unsigned int                    | Balance for the subaddress (locked or unlocked).
|             | ..unlocked_balance     | unsigned int                    | Unlocked balance for the subaddress.
|             | ..label                | string                          | Label for the subaddress.
|             | ..num_unspent_outputs  | unsigned int                    | Number of unspent outputs available for the subaddress.


## **get_address**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address","params":{"account_index":0,"address_index":[0,1,4]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_address",
    "params": {"account_index": 0, "address_index": [0, 1, 4]},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"account_index": 0, "address_index": [0, 1, 4]}
rpc_connection.get_address(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "addresses": [{
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "address_index": 0,
      "label": "Primary account",
      "used": true
    },{
      "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      "address_index": 1,
      "label": "",
      "used": true
    },{
      "address": "77xa6Dha7kzCQuvmd8iB5VYoMkdenwCNRU9khGhExXQ8KLL3z1N1ZATBD1sFPenyHWT9cm4fVFnCAUApY53peuoZFtwZiw5",
      "address_index": 4,
      "label": "test2",
      "used": true
    }]
  }
}
```
Return the wallet's addresses for an account. Optionally filter for specific set of subaddresses.  
Alias: *getaddress*.  

|             | Parameter       | Type                  | Description
| ---         | ---             | ---                   | ---
|**Inputs:**  | *account_index* | unsigned int          | Return subaddresses for this account.
|             | *address_index* | array of unsigned int | (Optional) List of subaddresses to return from an account.
|**Outputs:** | address         | string                | The 95|character hex address string of the monero|wallet|rpc in session.
|             | addresses       |                       | array of addresses informations
|             | ..address       | string                | The 95-character hex (sub)address string.
|             | ..label         | string                | Label of the (sub)address
|             | ..address_index | unsigned int          | index of the subaddress
|             | ..used          | boolean               | states if the (sub)address has already received funds


## **get_address_index**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address_index","params":{"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_address_index",
    "params": {
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"
}
rpc_connection.get_address_index(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "index": {
      "major": 0,
      "minor": 1
    }
  }
}
```
Get account and address indexes from a specific (sub)address  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *address* | string       | (sub)address to look for.
|**Outputs:** | index     |              | subaddress informations
|             | ..major   | unsigned int | Account index.
|             | ..minor   | unsigned int | Address index.


## **create_address**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_address","params":{"account_index":0,"label":"new-sub"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "create_address",
    "params": {"account_index": 0, "label": "new-sub"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"account_index": 0, "label": "new-sub"}
rpc_connection.create_address(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "7BG5jr9QS5sGMdpbBrZEwVLZjSKJGJBsXdZLt8wiXyhhLjy7x2LZxsrAnHTgD8oG46ZtLjUGic2pWc96GFkGNPQQDA3Dt7Q",
    "address_index": 5
  }
}
```
Create a new address for an account. Optionally, label the new address.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *account_index* | unsigned int | Create a new address for this account.
|             | *label*         | string       | (Optional) Label for the new address.
|**Outputs:** | address         | string       | Newly created address. Base58 representation of the public keys.
|             | address_index   | unsigned int | Index of the new address under the input account.


## **label_address**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"label_address","params":{"index":{"major":0,"minor":5},"label":"myLabel"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "label_address",
    "params": {"index": {"major": 0, "minor": 5}, "label": "myLabel"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"index": {"major": 0, "minor": 5}, "label": "myLabel"}
rpc_connection.label_address(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Label an address.  
Alias: *None*.  

|             | Parameter | Type             | Description
| ---         | ---       | ---              | ---
|**Inputs:**  | *index*   | subaddress index | JSON Object containing the major & minor address index:
|             | ..*major* | unsigned int     | Account index for the subaddress.
|             | ..*minor* | unsigned int     | Index of the subaddress in the account.
|             | *label*   | string           | Label for the address.
|**Outputs:** | None.     |                  |


## **get_accounts**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_accounts","params":{"tag":"myTag"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_accounts",
    "params": {"tag": "myTag"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"tag": "myTag"}
rpc_connection.get_accounts(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "subaddress_accounts": [{
      "account_index": 0,
      "balance": 157663195572433688,
      "base_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "label": "Primary account",
      "tag": "myTag",
      "unlocked_balance": 157443303037455077
    },{
      "account_index": 1,
      "balance": 0,
      "base_address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
      "label": "Secondary account",
      "tag": "myTag",
      "unlocked_balance": 0
    }],
    "total_balance": 157663195572433688,
    "total_unlocked_balance": 157443303037455077
  }
}
```
Get all accounts for a wallet. Optionally filter accounts by tag.  
Alias: *None*.  

|             | Parameter              | Type         | Description
| ---         | ---                    | ---          | ---
|**Inputs:**  | *tag*                  | string       | (Optional) Tag for filtering accounts.
|**Outputs:** | subaddress_accounts    |              |array of subaddress account information:
|             | ..account_index        | unsigned int | Index of the account.
|             | ..balance              | unsigned int | Balance of the account (locked or unlocked).
|             | ..base_address         | string       | Base64 representation of the first subaddress in the account.
|             | ..label                | string       | (Optional) Label of the account.
|             | ..tag                  | string       | (Optional) Tag for filtering accounts.
|             | ..unlocked_balance     | unsigned int | Unlocked balance for the account.
|             | total_balance          | unsigned int | Total balance of the selected accounts (locked or unlocked).
|             | total_unlocked_balance | unsigned int | Total unlocked balance of the selected accounts.


## **create_account**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_account","params":{"label":"Secondary account"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "create_account",
    "params": {"label": "Secondary account"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"label": "Secondary account"}
rpc_connection.create_account(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "account_index": 1,
    "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp"
  }
}
```
Create a new account with an optional label.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *label*       | string       | (Optional) Label for the account.
|**Outputs:** | account_index | unsigned int | Index of the new account.
|             | address       | string       | Address for this account. Base58 representation of the public keys.


## **label_account**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"label_account","params":{"account_index":0,"label":"Primary account"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "label_account",
    "params": {"account_index": 0, "label": "Primary account"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"account_index": 0, "label": "Primary account"}
rpc_connection.label_account(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "account_tags": [{
      "accounts": [0,1],
      "label": "",
      "tag": "myTag"
    }]
  }
}
```
Label an account.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *account_index* | unsigned int | Apply label to account at this index.
|             | *label*         | string       | Label for the account.
|**Outputs:** | *None*.         |              | 


## **get_account_tags**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_account_tags","params":""}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_account_tags",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.get_account_tags()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "account_tags": [{
      "accounts": [0],
      "label": "Test tag",
      "tag": "myTag"
    }]
  }
}
```
Get a list of user-defined account tags.  
Alias: *None*.  

|             | Parameter    | Type         | Description
| ---         | ---          | ---          | ---
|**Inputs:**  | *None*.      |              |  
|**Outputs:** | account_tags |              | array of account tag information:
|             | tag          | string       | Filter tag.
|             | label        | string       | Label for the tag.
|             | accounts     | array of int | List of tagged account indices.


## **tag_accounts**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"tag_accounts","params":{"tag":"myTag","accounts":[0,1]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "tag_accounts",
    "params": {"tag": "myTag", "accounts": [0, 1]},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"tag": "myTag", "accounts": [0, 1]}
rpc_connection.tag_accounts(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Apply a filtering tag to a list of accounts.  
Alias: *None*.  

|             | Parameter  | Type                  | Description
| ---         | ---        | ---                   | ---
|**Inputs:**  | *tag*      | string                | Tag for the accounts.
|             | *accounts* | array of unsigned int | Tag this list of accounts.
|**Outputs:** | *None*.    |                       |


## **untag_accounts**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"untag_accounts","params":{"accounts":[1]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "untag_accounts",
    "params": {"accounts":[1]},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"accounts":[1]}
rpc_connection.untag_accounts(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Remove filtering tag from a list of accounts.  
Alias: *None*.  

|             | Parameter  | Type                  | Description
| ---         | ---        | ---                   | ---
|**Inputs:**  | *accounts* | array of unsigned int | Remove tag from this list of accounts.
|**Outputs:** | *None*.    |                       |


## **set_account_tag_description**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_account_tag_description","params":{"tag":"myTag","description":"Test tag"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "set_account_tag_description",
    "params": {"tag": "myTag", "description": "Test tag"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"tag": "myTag", "description": "Test tag"}
rpc_connection.set_account_tag_description(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Set description for an account tag.  
Alias: *None*.  

|             | Parameter     | Type   | Description
| ---         | ---           | ---    | ---
|**Inputs:**  | *tag*         | string | Set a description for this tag.
|             | *description* | string | Description for the tag.
|**Outputs:** | *None*.       |        |


## **get_height**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_height"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_height",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.get_height()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "height": 145545
  }
}
```
Returns the wallet's current block height.  
Alias: *getheight*.  


|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | height    | unsigned int | The current monero-wallet-rpc's blockchain height. If the wallet has been offline for a long time, it may need to catch up with the daemon.


## **transfer**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer","params":{"destinations":[{"amount":100000000000,"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"},{"amount":200000000000,"address":"75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"get_tx_key": true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "transfer",
    "params": {
        "destinations": [
            {
                "amount": 100000000000,
                "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
            },
            {
                "amount": 200000000000,
                "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
            },
        ],
        "account_index": 0,
        "subaddr_indices": [0],
        "priority": 0,
        "ring_size": 7,
        "get_tx_key": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "destinations": [
        {
            "amount": 100000000000,
            "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        },
        {
            "amount": 200000000000,
            "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
        },
    ],
    "account_index": 0,
    "subaddr_indices": [0],
    "priority": 0,
    "ring_size": 7,
    "get_tx_key": True,
}
rpc_connection.transfer(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 300000000000,
    "fee": 86897600000,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "7663438de4f72b25a0e395b770ea9ecf7108cd2f0c4b75be0b14a103d3362be9",
    "tx_key": "25c9d8ec20045c80c93d665c9d3684aab7335f8b2cd02e1ba2638485afd1c70e236c4bdd7a2f1cb511dbf466f13421bdf8df988b7b969c448ca6239d7251490e4bf1bbf9f6ffacffdcdc93b9d1648ec499eada4d6b4e02ce92d4a1c0452e5d009fbbbf15b549df8856205a4c7bda6338d82c823f911acd00cb75850b198c5803",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
```
Send monero to a number of recipients.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *destinations*    |                       | array of destinations to receive XMR:
|             | ..*amount*        | unsigned int          | Amount to send to each destination, in @atomic|units.
|             | ..*address*       | string                | Destination public address.
|             | *account_index*   | unsigned int          | (Optional) Transfer from this account index. (Defaults to 0)
|             | *subaddr_indices* | array of unsigned int | (Optional) Transfer from this set of subaddresses. (Defaults to 0)
|             | *priority*        | unsigned int          | Set a priority for the transaction. Accepted Values are: 0|3 for: default, unimportant, normal, elevated, priority.
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Number of outputs to mix in the transaction (this output + N decoys from the blockchain).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32|byte/64|character hex string to identify a transaction.
|             | *get_tx_key*      | boolean               | (Optional) Return the transaction key after sending.
|             | *do_not_relay*    | boolean               | (Optional) If true, the newly created transaction will not be relayed to the monero network. (Defaults to false)
|             | *get_tx_hex*      | boolean               | Return the transaction as hex string after sending (Defaults to false)
|             | *get_tx_metadata* | boolean               | Return the metadata needed to relay the transaction. (Defaults to false)
|**Outputs:** | amount            |                       | Amount transferred for the transaction.
|             | fee               | int                   | Integer value of the fee charged for the txn.
|             | multisig_txset    |                       | Set of multisig transactions in the process of being signed (empty for non|multisig).
|             | tx_blob           |                       | Raw transaction represented as hex string, if get_tx_hex is true.
|             | tx_hash           | string                | String for the publically searchable transaction hash.
|             | tx_key            | string                | String for the transaction key if get_tx_key is true, otherwise, blank string.
|             | tx_metadata       |                       | Set of transaction metadata needed to relay this transfer later, if get_tx_metadata is true.
|             | unsigned_txset    | string                | Set of unsigned tx for cold-signing purposes.


## **transfer_split**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer_split","params":{"destinations":[{"amount":1000000000000,"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"},{"amount":2000000000000,"address":"75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"get_tx_key": true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "transfer_split",
    "params": {
        "destinations": [
            {
                "amount": 1000000000000,
                "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
            },
            {
                "amount": 2000000000000,
                "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
            },
        ],
        "account_index": 0,
        "subaddr_indices": [0],
        "priority": 0,
        "ring_size": 7,
        "get_tx_key": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "destinations": [
        {
            "amount": 1000000000000,
            "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        },
        {
            "amount": 2000000000000,
            "address": "75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv",
        },
    ],
    "account_index": 0,
    "subaddr_indices": [0],
    "priority": 0,
    "ring_size": 7,
    "get_tx_key": True,
}
rpc_connection.transfer_split(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount_list": [3000000000000],
    "fee_list": [85106400000],
    "multisig_txset": "",
    "tx_hash_list": ["c8d815f48f27d53fdaf198a74b292a91bfaf87529a9a9a9ee66079a890b3b58b"],
    "unsigned_txset": ""
  }
}
```
Same as transfer, but can split into more than one tx if necessary.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *destinations*    |                       | array of destinations to receive XMR:
|             | ..*amount*        | unsigned int          | Amount to send to each destination, in @atomic|units.
|             | ..*address*       | string                | Destination public address.
|             | *account_index*   | unsigned int          | (Optional) Transfer from this account index. (Defaults to 0)
|             | *subaddr_indices* | array of unsigned int | (Optional) Transfer from this set of subaddresses. (Defaults to 0)
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Sets ringsize to n (mixin + 1).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32|byte/64|character hex string to identify a transaction.
|             | *get_tx_keys*     | boolean               | (Optional) Return the transaction keys after sending.
|             | *priority*        | unsigned int          | Set a priority for the transactions. Accepted Values are: 0|3 for: default, unimportant, normal, elevated, priority.
|             | *do_not_relay*    | boolean               | (Optional) If true, the newly created transaction will not be relayed to the monero network. (Defaults to false)
|             | *get_tx_hex*      | boolean               | Return the transactions as hex string after sending
|             | *new_algorithm*   | boolean               | True to use the new transaction construction algorithm, defaults to false.
|             | *get_tx_metadata* | boolean               | Return list of transaction metadata needed to relay the transfer later.
|**Outputs:** | tx_hash_list      | array of string       | The tx hashes of every transaction.
|             | tx_key_list       | array of string       | The transaction keys for every transaction.
|             | amount_list       | array of integer      | The amount transferred for every transaction.
|             | fee_list          | array of integer      | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string       | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string       | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string                | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string                | Set of unsigned tx for cold|signing purposes.


## **sign_transfer**

> In the example below, we first generate an unsigned_txset on a read only wallet before signing it:
> Generate unsigned_txset using the above "transfer" method on read-only wallet:
##### shell:
```shell
curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer","params":{"destinations":[{"amount":1000000000000,"address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"do_not_relay":true,"get_tx_hex":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sign_transfer",
    "params": {
        "destinations": [
            {
                "amount": 1000000000000,
                "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
            }
        ],
        "account_index": 0,
        "subaddr_indices": [0],
        "priority": 0,
        "ring_size": 7,
        "do_not_relay": True,
        "get_tx_hex": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "destinations": [
        {
            "amount": 1000000000000,
            "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        }
    ],
    "account_index": 0,
    "subaddr_indices": [0],
    "priority": 0,
    "ring_size": 7,
    "do_not_relay": True,
    "get_tx_hex": True,
}
rpc_connection.sign_transfer(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 1000000000000,
    "fee": 15202740000,
    "multisig_txset": "",
    "tx_blob": "...long_hex...",
    "tx_hash": "c648ba0a049e5ce4ec21361dbf6e4b21eac0f828eea9090215de86c76b31d0a4",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": "...long_hex..."
  }
}
```

> Sign tx using the previously generated unsigned_txset
##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign_transfer","params":{"unsigned_txset": "...long_hex..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sign_transfer",
    "params": {"unsigned_txset": "...long_hex..."},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"unsigned_txset": "...long_hex..."}
rpc_connection.sign_transfer(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signed_txset": "...long_hex...",
    "tx_hash_list": ["ff2e2d49fbfb1c9a55754f786576e171c8bf21b463a74438df604b7fa6cebc6d"]
  }
}
```
Sign a transaction created on a read-only wallet (in cold-signing process)  
Alias: *None*.  

|             | Parameter        | Type            | Description
| ---         | ---              | ---             | ---
|**Inputs:**  | *unsigned_txset* | string          | Set of unsigned tx returned by "transfer" or "transfer_split" methods.
|             | *export_raw*     | boolean         | (Optional) If true, return the raw transaction data. (Defaults to false)
|**Outputs:** | signed_txset     | string          | Set of signed tx to be used for submitting transfer.
|             | tx_hash_list     | array of string | The tx hashes of every transaction.
|             | tx_raw_list      | array of string | The tx raw data of every transaction.


## **submit_transfer**

> In the example below, we submit the transfer using the signed_txset generated above:
##### shell:
```shell
curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_transfer","params":{"tx_data_hex":...long_hex..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "submit_transfer",
    "params": {"tx_data_hex": "...long_hex..."},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"tx_data_hex": "...long_hex..."}
rpc_connection.submit_transfer(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_hash_list": ["40fad7c828bb383ac02648732f7afce9adc520ba5629e1f5d9c03f584ac53d74"]
  }
}
```
Submit a previously signed transaction on a read-only wallet (in cold-signing process).  
Alias: *None*.  

|             | Parameter     | Type            | Description
| ---         | ---           | ---             | ---
|**Inputs:**  | *tx_data_hex* | string          | Set of signed tx returned by "sign_transfer"
|**Outputs:** | tx_hash_list  | array of string | The tx hashes of every transaction.


## **sweep_dust**


> In this example, `sweep_dust` returns nothing because there are no funds to sweep:  
##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_dust","params":{"get_tx_keys":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sweep_dust",
    "params": {"get_tx_keys": True},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"get_tx_keys": True}
rpc_connection.sweep_dust(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig_txset": "",
    "unsigned_txset": ""
  }
}
```
Send all dust outputs back to the wallet's, to make them easier to spend (and mix).  
Alias: *sweep_unmixable*.  

|             | Parameter         | Type             | Description
| ---         | ---               | ---              | ---
|**Inputs:**  | *get_tx_keys*     | boolean          | (Optional) Return the transaction keys after sending.
|             | *do_not_relay*    | boolean          | (Optional) If true, the newly created transaction will not be relayed to the monero network. (Defaults to false)
|             | *get_tx_hex*      | boolean          | (Optional) Return the transactions as hex string after sending. (Defaults to false)
|             | *get_tx_metadata* | boolean          | (Optional) Return list of transaction metadata needed to relay the transfer later. (Defaults to false)
|**Outputs:** | tx_hash_list      | array of string  | The tx hashes of every transaction.
|             | tx_key_list       | array of string  | The transaction keys for every transaction.
|             | amount_list       | array of integer | The amount transferred for every transaction.
|             | fee_list          | array of integer | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string  | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string  | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string           | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string           | Set of unsigned tx for cold|signing purposes.


## **sweep_all**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_all","params":{"address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","subaddr_indices":[4],"ring_size":7,"unlock_time":0,"get_tx_keys":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sweep_all",
    "params": {
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "subaddr_indices": [4],
        "ring_size": 7,
        "unlock_time": 0,
        "get_tx_keys": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "subaddr_indices": [4],
    "ring_size": 7,
    "unlock_time": 0,
    "get_tx_keys": True,
}
rpc_connection.sweep_all(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount_list": [9985885770000],
    "fee_list": [14114230000],
    "multisig_txset": "",
    "tx_hash_list": ["ab4b6b65cc8cd8c9dd317d0b90d97582d68d0aa1637b0065b05b61f9a66ea5c5"],
    "tx_key_list": ["b9b4b39d3bb3062ddb85ec0266d4df39058f4c86077d99309f218ce4d76af607"],
    "unsigned_txset": ""
  }
}
```
Send all unlocked balance to an address.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *address*         | string                | Destination public address.
|             | *account_index*   | unsigned int          | Sweep transactions from this account.
|             | *subaddr_indices* | array of unsigned int | (Optional) Sweep from this set of subaddresses in the account.
|             | *priority*        | unsigned int          | (Optional) Priority for sending the sweep transfer, partially determines fee.
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Sets ringsize to n (mixin + 1).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32-byte/64-character hex string to identify a transaction.
|             | *get_tx_keys*     | boolean               | (Optional) Return the transaction keys after sending.
|             | *below_amount*    | unsigned int          | (Optional) Include outputs below this amount.
|             | *do_not_relay*    | boolean               | (Optional) If true, do not relay this sweep transfer. (Defaults to false)
|             | *get_tx_hex*      | boolean               | (Optional) return the transactions as hex encoded string. (Defaults to false)
|             | *get_tx_metadata* | boolean               | (Optional) return the transaction metadata as a string. (Defaults to false)
|**Outputs:** | tx_hash_list      | array of string       | The tx hashes of every transaction.
|             | tx_key_list       | array of string       | The transaction keys for every transaction.
|             | amount_list       | array of integer      | The amount transferred for every transaction.
|             | fee_list          | array of integer      | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string       | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string       | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string                | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string                | Set of unsigned tx for cold-signing purposes.


## **sweep_single**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_single","params":{"address":"74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD","ring_size":7,"unlock_time":0,"key_image":"a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e","get_tx_keys":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sweep_single",
    "params": {
        "address": "74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD",
        "ring_size": 7,
        "unlock_time": 0,
        "key_image": "a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e",
        "get_tx_keys": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD",
    "ring_size": 7,
    "unlock_time": 0,
    "key_image": "a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e",
    "get_tx_keys": True,
}
rpc_connection.sweep_single(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 27126892247503,
    "fee": 14111630000,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
```
Send all of a specific unlocked output to an address.  
Alias: *None*.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *address*         | string                | Destination public address.
|             | *account_index*   | unsigned int          | Sweep transactions from this account.
|             | *subaddr_indices* | array of unsigned int | (Optional) Sweep from this set of subaddresses in the account.
|             | *priority*        | unsigned int          | (Optional) Priority for sending the sweep transfer, partially determines fee.
|             | *mixin*           | unsigned int          | Number of outputs from the blockchain to mix with (0 means no mixing).
|             | *ring_size*       | unsigned int          | Sets ringsize to n (mixin + 1).
|             | *unlock_time*     | unsigned int          | Number of blocks before the monero can be spent (0 to not add a lock).
|             | *payment_id*      | string                | (Optional) Random 32|byte/64|character hex string to identify a transaction.
|             | *get_tx_keys*     | boolean               | (Optional) Return the transaction keys after sending.
|             | *key_image*       | string                | Key image of specific output to sweep.
|             | *below_amount*    | unsigned int          | (Optional) Include outputs below this amount.
|             | *do_not_relay*    | boolean               | (Optional) If true, do not relay this sweep transfer. (Defaults to false)
|             | *get_tx_hex*      | boolean               | (Optional) return the transactions as hex encoded string. (Defaults to false)
|             | *get_tx_metadata* | boolean               | (Optional) return the transaction metadata as a string. (Defaults to false)
|**Outputs:** | tx_hash_list      | array of string       | The tx hashes of every transaction.
|             | tx_key_list       | array of string       | The transaction keys for every transaction.
|             | amount_list       | array of integer      | The amount transferred for every transaction.
|             | fee_list          | array of integer      | The amount of fees paid for every transaction.
|             | tx_blob_list      | array of string       | The tx as hex string for every transaction.
|             | tx_metadata_list  | array of string       | List of transaction metadata needed to relay the transactions later.
|             | multisig_txset    | string                | The set of signing keys used in a multisig transaction (empty for non|multisig).
|             | unsigned_txset    | string                | Set of unsigned tx for cold|signing purposes.


## **relay_tx**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"relay_tx","params":{"hex":"...tx_metadata..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "relay_tx",
    "params": {"hex": "...tx_metadata..."},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"hex": "...tx_metadata..."}
rpc_connection.relay_tx(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_hash": "1c42dcc5672bb09bccf33fb1e9ab4a498af59a6dbd33b3d0cfb289b9e0e25fa5"
  }
}
```
Relay a transaction previously created with `"do_not_relay":true`.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *hex*     | string | transaction metadata returned from a `transfer` method with `get_tx_metadata` set to `true`.
|**Outputs:** | tx_hash   |        | String for the publically searchable transaction hash.


## **store**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"store"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "store"
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.store()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Save the wallet file.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |


## **get_payments**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_payments","params":{"payment_id":"60900e5603bf96e3"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_payments",
    "params": {"payment_id": "60900e5603bf96e3"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"payment_id": "60900e5603bf96e3"}
rpc_connection.get_payments(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "payments": [{
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 1000000000000,
      "block_height": 127606,
      "payment_id": "60900e5603bf96e3",
      "subaddr_index": {
        "major": 0,
        "minor": 0
      },
      "tx_hash": "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f",
      "unlock_time": 0
    }]
  }
}
```
Get a list of incoming payments using a given payment id.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *payment_id*    | string       | Payment ID used to find the payments (16 characters hex).
|**Outputs:** | payments        |              | list of:
|             | ..payment_id    | string       | Payment ID matching the input parameter.
|             | ..tx_hash       | string       | Transaction hash used as the transaction ID.
|             | ..amount        | unsigned int | Amount for this payment.
|             | ..block_height  | unsigned int | Height of the block that first confirmed this payment.
|             | ..unlock_time   | unsigned int | Time (in block height) until this payment is safe to spend.
|             | ..subaddr_index |              | subaddress index:
|             | ....major       | unsigned int | Account index for the subaddress.
|             | ....minor       | unsigned int | Index of the subaddress in the account.
|             | ..address       | string       | Address receiving the payment | Base58 representation of the public keys.


## **get_bulk_payments**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_bulk_payments","params":{"payment_ids":["60900e5603bf96e3"],"min_block_height":"120000"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_bulk_payments",
    "params": {"payment_ids": ["60900e5603bf96e3"], "min_block_height": "120000"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"payment_ids": ["60900e5603bf96e3"], "min_block_height": "120000"}
rpc_connection.get_bulk_payments(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "payments": [{
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 1000000000000,
      "block_height": 127606,
      "payment_id": "60900e5603bf96e3",
      "subaddr_index": {
        "major": 0,
        "minor": 0
      },
      "tx_hash": "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f",
      "unlock_time": 0
    }]
  }
}
```
Get a list of incoming payments using a given payment id, or a list of payments ids, from a given height. This method is the preferred method over `get_payments` because it has the same functionality but is more extendable. Either is fine for looking up transactions by a single payment ID.  
Alias: *None*.  

|             | Parameter          | Type            | Description
| ---         | ---                | ---             | ---
|**Inputs:**  | *payment_ids*      | array of string | Payment IDs used to find the payments (16 characters hex).
|             | *min_block_height* | unsigned int    | The block height at which to start looking for payments.
|**Outputs:** | payments           |                 | list of:
|             | ..payment_id       | string          | Payment ID matching one of the input IDs.
|             | ..tx_hash          | string          | Transaction hash used as the transaction ID.
|             | ..amount           | unsigned int    | Amount for this payment.
|             | ..block_height     | unsigned int    | Height of the block that first confirmed this payment.
|             | ..unlock_time      | unsigned int    | Time (in block height) until this payment is safe to spend.
|             | ..subaddr_index    |                 | subaddress index:
|             | ....major          | unsigned int    | Account index for the subaddress.
|             | ....minor          | unsigned int    | Index of the subaddress in the account.
|             | ..address          | string          | Address receiving the payment; Base58 representation of the public keys.


## **incoming_transfers**


> get all transfers:
##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"all","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "incoming_transfers",
    "params": {
        "transfer_type": "all",
        "account_index": 0,
        "subaddr_indices": [3],
        "verbose": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "transfer_type": "all",
    "account_index": 0,
    "subaddr_indices": [3],
    "verbose": True,
}
rpc_connection.incoming_transfers(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfers": [{
      "amount": 60000000000000,
      "global_index": 122405,
      "key_image": "768f5144777eb23477ab7acf83562581d690abaf98ca897c03a9d2b900eb479b",
      "spent": true,
      "subaddr_index": 3,
      "tx_hash": "f53401f21c6a43e44d5dd7a90eba5cf580012ad0e15d050059136f8a0da34f6b",
      "tx_size": 159
    },{
      "amount": 27126892247503,
      "global_index": 594994,
      "key_image": "7e561394806afd1be61980cc3431f6ef3569fa9151cd8d234f8ec13aa145695e",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
      "tx_size": 157
    },{
      "amount": 27169374733655,
      "global_index": 594997,
      "key_image": "e76c0a3bfeaae35e4173712f782eb34011198e26b990225b71aa787c8ba8a157",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "0bd959b59117ee1254bd8e5aa8e77ec04ef744144a1ffb2d5c1eb9380a719621",
      "tx_size": 158
    }]
  }
}
```

> get available transfers:
##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"available","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "incoming_transfers",
    "params": {
        "transfer_type": "available",
        "account_index": 0,
        "subaddr_indices": [3],
        "verbose": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "transfer_type": "available",
    "account_index": 0,
    "subaddr_indices": [3],
    "verbose": True,
}
rpc_connection.incoming_transfers(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfers": [{
      "amount": 27126892247503,
      "global_index": 594994,
      "key_image": "7e561394806afd1be61980cc3431f6ef3569fa9151cd8d234f8ec13aa145695e",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
      "tx_size": 157
    },{
      "amount": 27169374733655,
      "global_index": 594997,
      "key_image": "e76c0a3bfeaae35e4173712f782eb34011198e26b990225b71aa787c8ba8a157",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "0bd959b59117ee1254bd8e5aa8e77ec04ef744144a1ffb2d5c1eb9380a719621",
      "tx_size": 158
    }]
  }
}
```

> get unavailable transfers:
##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"unavailable","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "incoming_transfers",
    "params": {
        "transfer_type": "unavailable",
        "account_index": 0,
        "subaddr_indices": [3],
        "verbose": True,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "transfer_type": "unavailable",
    "account_index": 0,
    "subaddr_indices": [3],
    "verbose": True,
}
rpc_connection.incoming_transfers(params)
```
```json
{
"id": "0",
"jsonrpc": "2.0",
"result": {
  "transfers": [{
    "amount": 60000000000000,
    "global_index": 122405,
    "key_image": "768f5144777eb23477ab7acf83562581d690abaf98ca897c03a9d2b900eb479b",
    "spent": true,
    "subaddr_index": 3,
    "tx_hash": "f53401f21c6a43e44d5dd7a90eba5cf580012ad0e15d050059136f8a0da34f6b",
    "tx_size": 159
  }]
}
}
```

Return a list of incoming transfers to the wallet.  

|             | Parameter         | Type                  | Description
| ---         | ---               | ---                   | ---
|**Inputs:**  | *transfer_type*   | string                | "all": all the transfers, "available": only transfers which are not yet spent, OR "unavailable": only transfers which are already spent.
|             | *account_index*   | unsigned int          | (Optional) Return transfers for this account. (defaults to 0)
|             | *subaddr_indices* | array of unsigned int | (Optional) Return transfers sent to these subaddresses.
|             | *verbose*         | boolean               | (Optional) Enable verbose output, return key image if true.
|**Outputs:** | transfers         |                       | list of:
|             | ..amount          | unsigned int          | Amount of this transfer.
|             | ..global_index    | unsigned int          | Mostly internal use, can be ignored by most users.
|             | ..key_image       | string                | Key image for the incoming transfer's unspent output (empty unless verbose is true).
|             | ..spent           | boolean               | Indicates if this transfer has been spent.
|             | ..subaddr_index   | unsigned int          | Subaddress index for incoming transfer.
|             | ..tx_hash         | string                | Several incoming transfers may share the same hash if they were in the same transaction.
|             | ..tx_size         | unsigned int          | Size of transaction in bytes.


## **query_key**


> Example (Query view key):
##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"query_key","params":{"key_type":"view_key"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "query_key",
    "params": {"key_type": "view_key"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"key_type": "view_key"}
rpc_connection.query_key(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "key": "0a1a38f6d246e894600a3e27238a064bf5e8d91801df47a17107596b1378e501"
  }
}
```
> Example (Query mnemonic key):

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"query_key","params":{"key_type":"mnemonic"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "query_key",
    "params": {"key_type": "mnemonic"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"key_type": "mnemonic"}
rpc_connection.query_key(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "key": "vocal either anvil films dolphin zeal bacon cuisine quote syndrome rejoices envy okay pancakes tulips lair greater petals organs enmity dedicated oust thwart tomorrow tomorrow"
  }
}
```

Return the spend or view private key.  
Alias: *None*.  

|             | Parameter  | Type   | Description
| ---         | ---        | ---    | ---
|**Inputs:**  | *key_type* | string | Which key to retrieve: "mnemonic" - the mnemonic seed (older wallets do not have one) OR "view_key" - the view key
|**Outputs:** | key        | string | The view key will be hex encoded, while the mnemonic will be a string of words.


## **make_integrated_address**


> Example (Payment ID is empty, use a random ID):

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_integrated_address","params":{"standard_address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "make_integrated_address",
    "params": {
        "standard_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "standard_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
}
rpc_connection.make_integrated_address(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn",
    "payment_id": "420fa29b2d9a49f5"
  }
}
```

Make an integrated address from the wallet address and a payment id.  
Alias: *None*.  

|             | Parameter           | Type   | Description
| ---         | ---                 | ---    | ---
|**Inputs:**  | *standard_address*  | string | (Optional, defaults to primary address) Destination public address.
|             | *payment_id*        | string | (Optional, defaults to a random ID) 16 characters hex encoded.
|**Outputs:** | integrated_address* | string |
|             | payment_id*         | string | hex encoded;


## **split_integrated_address**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"split_integrated_address","params":{"integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "split_integrated_address",
    "params": {
        "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"
}
rpc_connection.split_integrated_address(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "is_subaddress": false,
    "payment_id": "420fa29b2d9a49f5",
    "standard_address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
  }
}
```
Retrieve the standard address and payment id corresponding to an integrated address.  
Alias: *None*.  

|             | Parameter            | Type    | Description
| ---         | ---                  | ---     | ---
|**Inputs:**  | *integrated_address* | string  |
|**Outputs:** | is_subaddress        | boolean | States if the address is a subaddress
|             | payment              | string  | hex encoded
|             | standard_address     | string  |


## **stop_wallet**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"stop_wallet"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "stop_wallet",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.stop_wallet()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Stops the wallet, storing the current state.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |


## **rescan_blockchain**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"rescan_blockchain"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "rescan_blockchain",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.rescan_blockchain()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Rescan the blockchain from scratch, losing any information which can not be recovered from the blockchain itself.  
This includes destination addresses, tx secret keys, tx notes, etc.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |


## **set_tx_notes**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_tx_notes","params":{"txids":["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"],"notes":["This is an example"]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "set_tx_notes",
    "params": {
        "txids": [
            "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"
        ],
        "notes": ["This is an example"],
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txids": [
        "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"
    ],
    "notes": ["This is an example"],
}
rpc_connection.set_tx_notes(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Set arbitrary string notes for transactions.  
Alias: *None*.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *txids*   | array of string | transaction ids
|             | *notes*   | array of string | notes for the transactions
|**Outputs:** | *None*.   |                 |


## **get_tx_notes**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_notes","params":{"txids":["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_tx_notes",
    "params": {"txids": ["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"txids": ["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]}
rpc_connection.get_tx_notes(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "notes": ["This is an example"]
  }
}
```
Get string notes for transactions.  
Alias: *None*.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *txids*   | array of string | transaction ids
|**Outputs:** | notes     | array of string | notes for the transactions


## **set_attribute**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_attribute","params":{"key":"my_attribute","value":"my_value"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "set_attribute",
    "params": {"key": "my_attribute", "value": "my_value"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"key": "my_attribute", "value": "my_value"}
rpc_connection.set_attribute(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Set arbitrary attribute.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *key*     | string | attribute name
|             | *value*   | string | attribute value
|**Outputs:** | *None*.   |        |


## **get_attribute**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_attribute","params":{"key":"my_attribute"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_attribute",
    "params": {"key": "my_attribute"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"key": "my_attribute"}
rpc_connection.get_attribute(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "value": "my_value"
  }
}
```
Get attribute value by name.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *key*     | string | attribute name
|**Outputs:** | value     | string | attribute value


## **get_tx_key**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_key","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_tx_key",
    "params": {"txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"}
rpc_connection.get_tx_key(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06"
  }
}
```
Get transaction secret key from transaction id.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *txid*    | string | transaction id.
|**Outputs:** | tx_key    | string | transaction secret key.


## **check_tx_key**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_key","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","tx_key":"feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_tx_key",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06",
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06",
    "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
}
rpc_connection.check_tx_key(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "confirmations": 0,
    "in_pool": false,
    "received": 1000000000000
  }
}
```
Check a transaction in the blockchain with its secret key.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *txid*        | string       | transaction id.
|             | *tx_key*      | string       | transaction secret key.
|             | *address*     | string       | destination public address of the transaction.
|**Outputs:** | confirmations | unsigned int | Number of block mined after the one with the transaction.
|             | in_pool       | boolean      | States if the transaction is still in pool or has been added to a block.
|             | received      | unsigned int | Amount of the transaction.


## **get_tx_proof**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"this is my transaction"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_tx_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "message": "this is my transaction",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
    "message": "this is my transaction",
}
rpc_connection.get_tx_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"
  }
}
```
Get transaction signature to prove it.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *txid*    | string | transaction id.
|             | *address* | string | destination public address of the transaction.
|             | *message* | string | (Optional) add a message to the signature to further authenticate the prooving process.
|**Outputs:** | signature | string | transaction signature.


## **check_tx_proof**

> In the example below, the transaction has been proven:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"this is my transaction","signature":"InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_tx_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "message": "this is my transaction",
        "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
    "message": "this is my transaction",
    "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
}
rpc_connection.check_tx_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "confirmations": 482,
    "good": true,
    "in_pool": false,
    "received": 1000000000000
  }
}
```

> In the example below, the wrong message is used, avoiding the transaction to be proved:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"wrong message","signature":"InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_tx_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "message": "wrong message",
        "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
    "message": "wrong message",
    "signature": "InProofV13vqBCT6dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ",
}
rpc_connection.check_tx_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "confirmations": 0,
    "good": false,
    "in_pool": false,
    "received": 0
  }
}
```

Prove a transaction by checking its signature.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *txid*        | string       | transaction id.
|             | *address*     | string       | destination public address of the transaction.
|             | *message*     | string       | (Optional) Should be the same message used in `get_tx_proof`.
|             | *signature*   | string       | transaction signature to confirm.
|**Outputs:** | confirmations | unsigned int | Number of block mined after the one with the transaction.
|             | good          | boolean      | States if the inputs proves the transaction.
|             | in_pool       | boolean      | States if the transaction is still in pool or has been added to a block.
|             | received      | unsigned int | Amount of the transaction.


## **get_spend_proof**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"this is my transaction"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_spend_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "message": "this is my transaction",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "message": "this is my transaction",
}
rpc_connection.get_spend_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"
  }
}
```
Generate a signature to prove a spend. Unlike proving a transaction, it does not requires the destination public address.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *txid*    | string | transaction id.
|             | *message* | string | (Optional) add a message to the signature to further authenticate the prooving process.
|**Outputs:** | signature | string | spend signature.


## **check_spend_proof**


> In the example below, the spend has been proven:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"this is my transaction","signature":"SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_spend_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "message": "this is my transaction",
        "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "message": "this is my transaction",
    "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB",
}
rpc_connection.check_spend_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true
  }
}
```

> In the example below, the wrong message is used, avoiding the spend to be proved:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"wrong message","signature":"SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_spend_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "message": "wrong message",
        "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "message": "wrong message",
    "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB",
}
rpc_connection.check_spend_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": false
  }
}
```

Prove a spend using a signature. Unlike proving a transaction, it does not requires the destination public address.  
Alias: *None*.  

|             | Parameter   | Type    | Description
| ---         | ---         | ---     | ---
|**Inputs:**  | *txid*      | string  | transaction id.
|             | *message*   | string  | (Optional) Should be the same message used in `get_spend_proof`.
|             | *signature* | string  | spend signature to confirm.
|**Outputs:** | good        | boolean | States if the inputs proves the spend.


## **get_reserve_proof**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_reserve_proof","params":{"all":false,"account_index":0,"amount":100000000000}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_reserve_proof",
    "params": {"all": False, "account_index": 0, "amount": 100000000000},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"all": False, "account_index": 0, "amount": 100000000000}
rpc_connection.get_reserve_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A"
  }
}
```
Generate a signature to prove of an available amount in a wallet.  
Alias: *None*.  

|             | Parameter       | Type         | Description
| ---         | ---             | ---          | ---
|**Inputs:**  | *all*           | boolean      | Proves all wallet balance to be disposable.
|             | *account_index* | unsigned int | Specify the account from witch to prove reserve. (ignored if `all` is set to true)
|             | *amount*        | unsigned int | Amount (in @atomic-units) to prove the account has for reserve. (ignored if `all` is set to true)
|             | *message*       | string       | (Optional) add a message to the signature to further authenticate the prooving process.
|**Outputs:** | signature       | string       | reserve signature.



## **check_reserve_proof**

> In the example below, the reserve has been proven:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_reserve_proof","params":{"address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","signature":"ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_reserve_proof",
    "params": {
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "signature": "ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "signature": "ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A",
}
rpc_connection.check_reserve_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true,
    "spent": 0,
    "total": 100000000000
  }
}
```

> In the example below, all wallet reserve has been proven:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_reserve_proof","params":{"address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","message":"I have 10 at least","signature":"...signature..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_reserve_proof",
    "params": {
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "message": "I have 10 at least",
        "signature": "...signature...",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "message": "I have 10 at least",
    "signature": "...signature...",
}
rpc_connection.check_reserve_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true,
    "spent": 0,
    "total": 164113855714662789
  }
}
```

> In the example below, the wrong message is used, avoiding the reserve to be proved:

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"wrong message","signature":"SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "check_spend_proof",
    "params": {
        "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
        "message": "wrong message",
        "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "txid": "19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be",
    "message": "wrong message",
    "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB",
}
rpc_connection.check_spend_proof(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": false
  }
}
```
Proves a wallet has a disposable reserve using a signature.  
Alias: *None*.  

|             | Parameter   | Type    | Description
| ---         | ---         | ---     | ---
|**Inputs:**  | *address*   | string  | Public address of the wallet.
|             | *message*   | string  | (Optional) Should be the same message used in `get_reserve_proof`.
|             | *signature* | string  | reserve signature to confirm.
|**Outputs:** | good        | boolean | States if the inputs proves the reserve.


## **get_transfers**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_transfers","params":{"in":true,"account_index":1}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_transfers",
    "params": {"in": True, "account_index": 1},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"in": True, "account_index": 1}
rpc_connection.get_transfers(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "in": [{
      "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
      "amount": 200000000000,
      "confirmations": 1,
      "double_spend_seen": false,
      "fee": 21650200000,
      "height": 153624,
      "note": "",
      "payment_id": "0000000000000000",
      "subaddr_index": {
        "major": 1,
        "minor": 0
      },
      "suggested_confirmations_threshold": 1,
      "timestamp": 1535918400,
      "txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a",
      "type": "in",
      "unlock_time": 0
    }]
  }
}
```
Returns a list of transfers.  
Alias: *None*.  

|             | Parameter                            | Type                  | Description
| ---         | ---                                  | ---                   | ---
|**Inputs:**  | *in*                                 | boolean               | (Optional) Include incoming transfers.
|             | *out*                                | boolean               | (Optional) Include outgoing transfers.
|             | *pending*                            | boolean               | (Optional) Include pending transfers.
|             | *failed*                             | boolean               | (Optional) Include failed transfers.
|             | *pool*                               | boolean               | (Optional) Include transfers from the daemon's transaction pool.
|             | *filter_by_height*                   | boolean               | (Optional) Filter transfers by block height.
|             | *min_height*                         | unsigned int          | (Optional) Minimum block height to scan for transfers, if filtering by height is enabled.
|             | *max_height*                         | unsigned int          | (Opional) Maximum block height to scan for transfers, if filtering by height is enabled (defaults to max block height).
|             | *account_index*                      | unsigned int          | (Optional) Index of the account to query for transfers. (defaults to 0)
|             | *subaddr_indices*                    | array of unsigned int | (Optional) List of subaddress indices to query for transfers. (defaults to 0)
|**Outputs:** | in                                   |                       | array of transfers:
|             | .. address                           | string                | Public address of the transfer.
|             | .. amount                            | unsigned int          | Amount transferred.
|             | .. confirmations                     | unsigned int          | Number of block mined since the block containing this transaction (or block height at which the transaction should be added to a block if not yet confirmed).
|             | .. double_spend_seen                 | boolean               | True if the key image(s) for the transfer have been seen before.
|             | .. fee                               | unsigned int          | Transaction fee for this transfer.
|             | .. height                            | unsigned int          | Height of the first block that confirmed this transfer (0 if not mined yet).
|             | .. note                              | string                | Note about this transfer.
|             | .. payment_id                        | string                | Payment ID for this transfer.
|             | .. subaddr_index                     |                       | JSON object containing the major & minor subaddress index:
|             | ..  major                            | unsigned int          | Account index for the subaddress.
|             | ..  minor                            | unsigned int          | Index of the subaddress under the account.
|             | .. suggested_confirmations_threshold | unsigned int          | Estimation of the confirmations needed for the transaction to be included in a block.
|             | .. timestamp                         | unsigned int          | POSIX timestamp for when this transfer was first confirmed in a block (or timestamp submission if not mined yet).
|             | .. txid                              | string                | Transaction ID for this transfer.
|             | .. type                              | string                | Transfer type: "in"
|             | .. unlock_time                       | unsigned int          | Number of blocks until transfer is safely spendable.
|             | out                                  |                       | array of transfers (see above).
|             | pending                              |                       | array of transfers (see above).
|             | failed                               |                       | array of transfers (see above).
|             | pool                                 |                       | array of transfers (see above).


## **get_transfer_by_txid**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_transfer_by_txid","params":{"txid":"c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_transfer_by_txid",
    "params": {"txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"}
rpc_connection.get_transfer_by_txid(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfer": {
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 300000000000,
      "confirmations": 1,
      "destinations": [{
        "address": "7BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "amount": 100000000000
      },{
        "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
        "amount": 200000000000
      }],
      "double_spend_seen": false,
      "fee": 21650200000,
      "height": 153624,
      "note": "",
      "payment_id": "0000000000000000",
      "subaddr_index": {
        "major": 0,
        "minor": 0
      },
      "suggested_confirmations_threshold": 1,
      "timestamp": 1535918400,
      "txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a",
      "type": "out",
      "unlock_time": 0
    }
  }
}
```
Show information about a transfer to/from this address.  
Alias: *None*.  


|             | Parameter                         | Type         | Description
| ---         | ---                               | ---          | ---
|**Inputs:**  | *txid*                            | string       | Transaction ID used to find the transfer.
|             | *account_index*                   | unsigned int | (Optional) Index of the account to query for the transfer.
|**Outputs:** | transfer                          |              | JSON object containing payment information:
|             | address                           | string       | Address that transferred the funds. Base58 representation of the public keys.
|             | amount                            | unsigned int | Amount of this transfer.
|             | confirmations                     | unsigned int | Number of block mined since the block containing this transaction (or block height at which the transaction should be added to a block if not yet confirmed).
|             | destinations                      |              | array of JSON objects containing transfer destinations:
|             | ..amount                          | unsigned int | Amount transferred to this destination.
|             | ..address                         | string       | Address for this destination. Base58 representation of the public keys.
|             | double_spend_seen                 | boolean      | True if the key image(s) for the transfer have been seen before.
|             | fee                               | unsigned int | Transaction fee for this transfer.
|             | height                            | unsigned int | Height of the first block that confirmed this transfer.
|             | note                              | string       | Note about this transfer.
|             | payment_id                        | string       | Payment ID for this transfer.
|             | subaddr_index                     |              | JSON object containing the major & minor subaddress index:
|             | ..major                           | unsigned int | Account index for the subaddress.
|             | ..minor                           | unsigned int | Index of the subaddress under the account.
|             | suggested_confirmations_threshold | unsigned int | Estimation of the confirmations needed for the transaction to be included in a block.
|             | timestamp                         | unsigned int | POSIX timestamp for the block that confirmed this transfer (or timestamp submission if not mined yet).
|             | txid                              | string       | Transaction ID of this transfer (same as input TXID).
|             | type                              | string       | Type of transfer, one of the following: "in", "out", "pending", "failed", "pool"
|             | unlock_time                       | unsigned int | Number of blocks until transfer is safely spendable.
                
                
## **sign**     


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign","params":{"data":"This is sample data to be signed"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sign",
    "params": {"data": "This is sample data to be signed"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"data": "This is sample data to be signed"}
rpc_connection.sign(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3"
  }
}
```
Sign a string.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *data*    | string | Anything you need to sign.
|**Outputs:** | signature | string | Signature generated against the "data" and the account public address.


## **verify**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"verify","params":{"data":"This is sample data to be signed","address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","signature":"SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "verify",
    "params": {
        "data": "This is sample data to be signed",
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "signature": "SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "data": "This is sample data to be signed",
    "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "signature": "SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3",
}
rpc_connection.verify(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true
  }
}
```
Verify a signature on a string.  
Alias: *None*.  

|             | Parameter   | Type    | Description
| ---         | ---         | ---     | ---
|**Inputs:**  | *data*      | string  | What should have been signed.
|             | *address*   | string  | Public address of the wallet used to `sign` the data.
|             | *signature* | string  | signature generated by `sign` method.
|**Outputs:** | good        | boolean |


## **export_outputs**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_outputs"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "export_outputs",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.export_outputs()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "outputs_data_hex": "...outputs..."
  }
}
```
Export all outputs in hex format.  
Alias: *None*.  

|             | Parameter        | Type   | Description
| ---         | ---              | ---    | ---
|**Inputs:**  | *None*.          |        |
|**Outputs:** | outputs_data_hex | string | wallet outputs in hex format.


## **import_outputs**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_outputs","params":{"outputs_data_hex":"...outputs..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "import_outputs",
    "params": {"outputs_data_hex": "...outputs..."},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"outputs_data_hex": "...outputs..."}
rpc_connection.import_outputs(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "num_imported": 6400
  }
}
```
Import outputs in hex format.  
Alias: *None*.  

|             | Parameter          | Type         | Description
| ---         | ---                | ---          | ---
|**Inputs:**  | *outputs_data_hex* | string       | wallet outputs in hex format.
|**Outputs:** | num_imported       | unsigned int | number of outputs imported.


## **export_key_images**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_key_images"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "export_key_images",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.export_key_images()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signed_key_images": [{
      "key_image": "cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876",
      "signature": "c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00"
    },{
      "key_image": "65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19",
      "signature": "c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c"
    },...]
  }
}
```
Export a signed set of key images.  
Alias: *None*.  

|             | Parameter         | Type   | Description
| ---         | ---               | ---    | ---
|**Inputs:**  | *None*.           |        |
|**Outputs:** | signed_key_images |        | array of signed key images:
|             | ..key_image       | string |
|             | ..signature       | string |


## **import_key_images**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_key_images", "params":{"signed_key_images":[{"key_image":"cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876","signature":"c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00"},{"key_image":"65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19","signature":"c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c"}]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "import_key_images",
    "params": {
        "signed_key_images": [
            {
                "key_image": "cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876",
                "signature": "c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00",
            },
            {
                "key_image": "65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19",
                "signature": "c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c",
            },
        ]
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "signed_key_images": [
        {
            "key_image": "cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876",
            "signature": "c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00",
        },
        {
            "key_image": "65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19",
            "signature": "c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c",
        },
    ]
}
rpc_connection.import_key_images(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "height": 76428,
    "spent": 62708953408711,
    "unspent": 0
  }
}
```
Import signed key images list and verify their spent status.  
Alias: *None*.  

|             | Parameter           | Type         | Description
| ---         | ---                 | ---          | ---
|**Inputs:**  | *signed_key_images* |              | array of signed key images:
|             | ..*key_image*       | string       |
|             | ..*signature*       | string       |
|**Outputs:** | height              | unsigned int |
|             | spent               | unsigned int | Amount (in @atomic|units) spent from those key images.
|             | unspent             | unsigned int | Amount (in @atomic|units) still available from those key images.



## **make_uri**

##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_uri","params":{"address":"55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","amount":10,"payment_id":"420fa29b2d9a49f5","tx_description":"Testing out the make_uri function.","recipient_name":"el00ruobuob Stagenet wallet"}}'  -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "make_uri",
    "params": {
        "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
        "amount": 10,
        "payment_id": "420fa29b2d9a49f5",
        "tx_description": "Testing out the make_uri function.",
        "recipient_name": "el00ruobuob Stagenet wallet",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "amount": 10,
    "payment_id": "420fa29b2d9a49f5",
    "tx_description": "Testing out the make_uri function.",
    "recipient_name": "el00ruobuob Stagenet wallet",
}
rpc_connection.make_uri(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "uri": "monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
  }
}
```
Create a payment URI using the official URI spec.  
Alias: *None*.  

|             | Parameter        | Type         | Description
| ---         | ---              | ---          | ---
|**Inputs:**  | *address*        | string       | Wallet address
|             | *amount*         | unsigned int | (optional) the integer amount to receive, in **@atomic-units**
|             | *payment_id*     | string       | (optional) 16 or 64 character hexadecimal payment id
|             | *recipient_name* | string       | (optional) name of the payment recipient
|             | *tx_description* | string       | (optional) Description of the reason for the tx
|**Outputs:** | uri              | string       | This contains all the payment input information as a properly formatted payment URI


## **parse_uri**


##### shell:
```shell
$ curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"parse_uri","params":{"uri":"monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "parse_uri",
    "params": {
        "uri": "monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "uri": "monero:55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
}
rpc_connection.parse_uri(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "uri": {
      "address": "55LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 10,
      "payment_id": "420fa29b2d9a49f5",
      "recipient_name": "el00ruobuob Stagenet wallet",
      "tx_description": "Testing out the make_uri function."
    }
  }
}
```
Parse a payment URI to get payment information.  
Alias: *None*.  

|             | Parameter        | Type         | Description
| ---         | ---              | ---          | ---
|**Inputs:**  | *uri*            | string       | This contains all the payment input information as a properly formatted payment URI
|**Outputs:** | uri              |              | JSON object containing payment information:
|             | ..address        | string       | Wallet address
|             | ..amount         | unsigned int | Integer amount to receive, in @atomic|units (0 if not provided)
|             | ..payment_id     | string       | 16 or 64 character hexadecimal payment id (empty if not provided)
|             | ..recipient_name | string       | Name of the payment recipient (empty if not provided)
|             | ..tx_description | string       | Description of the reason for the tx (empty if not provided)


## **get_address_book**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address_book","params":{"entries":[0,1]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_address_book",
    "params": {"entries": [0,1]},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"entries": [0,1]}
rpc_connection.get_address_book(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "entries": [{
      "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
      "description": "Second account",
      "index": 0,
      "payment_id": "0000000000000000000000000000000000000000000000000000000000000000"
    },{
      "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
      "description": "Third account",
      "index": 1,
      "payment_id": "0000000000000000000000000000000000000000000000000000000000000000"
    }]
  }
}
```
Retrieves entries from the address book.  
Alias: *None*.  

|             | Parameter     | Type                  | Description
| ---         | ---           | ---                   | ---
|**Inputs:**  | *entries*     | array of unsigned int | indices of the requested address book entries
|**Outputs:** | entries       |                       | array of entries:
|             | ..address     | string                | Public address of the entry
|             | ..description | string                | Description of this address entry
|             | ..index       | unsigned int          |
|             | ..payment_id  | string                |


## **add_address_book**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"add_address_book","params":{"address":"78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j","description":"Third account"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "add_address_book",
    "params": {
        "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
        "description": "Third account",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
    "description": "Third account",
}
rpc_connection.add_address_book(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "index": 1
  }
}
```
Add an entry to the address book.  
Alias: *None*.  

|             | Parameter     | Type         | Description
| ---         | ---           | ---          | ---
|**Inputs:**  | *address*     | string       |
|             | *payment_id*  |              | (optional) string, defaults to "0000000000000000000000000000000000000000000000000000000000000000";
|             | *description* |              | (optional) string, defaults to "";
|**Outputs:** | index         | unsigned int | The index of the address book entry.


## **delete_address_book**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"delete_address_book","params":{"index":1}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "delete_address_book",
    "params": {"index": 1},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"index": 1}
rpc_connection.delete_address_book(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Delete an entry from the address book.  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *index*   | unsigned int | The index of the address book entry.
|**Outputs:** | *None*.   |              |


## **refresh**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"refresh","params":{"start_height":100000}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "refresh",
    "params": {"start_height": 100000},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"start_height": 100000}
rpc_connection.refresh(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "blocks_fetched": 24,
    "received_money": true
  }
}
```
Refresh a wallet after openning.  
Alias: *None*.  

|             | Parameter      | Type         | Description
| ---         | ---            | ---          | ---
|**Inputs:**  | *start_height* | unsigned int | (Optional) The block height from which to start refreshing.
|**Outputs:** | blocks_fetched | unsigned int | Number of new blocks scanned.
|             | received_money | boolean      | States if transactions to the wallet have been found in the blocks.


## **rescan_spent**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"rescan_spent"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "rescan_spent",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.rescan_spent()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {}
}
```
Rescan the blockchain for spent outputs.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |


## **start_mining**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"start_mining","params":{"threads_count":1,"do_background_mining":true,"ignore_battery":false}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "start_mining",
    "params": {"threads_count": 1, "do_background_mining": True, "ignore_battery": False},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"threads_count": 1, "do_background_mining": True, "ignore_battery": False}
rpc_connection.start_mining(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Start mining in the Monero daemon.  
Alias: *None*.  

|             | Parameter              | Type         | Description
| ---         | ---                    | ---          | ---
|**Inputs:**  | *threads_count*        | unsigned int | Number of threads created for mining.
|             | *do_background_mining* | boolean      | Allow to start the miner in @smart-mining mode.
|             | *ignore_battery*       | boolean      | Ignore battery status (for @smart-mining only)
|**Outputs:** | *None*.                |              |


## **stop_mining**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"stop_mining"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "stop_mining",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.stop_mining()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Stop mining in the Monero daemon.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |


## **get_languages**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_languages"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_languages",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.get_languages()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "languages": ["Deutsch","English","Espanol","Francais","Italiano","Nederlands","Portugues","������� ����","???","???? (??)","Esperanto","Lojban"]
  }
}
```
Get a list of available languages for your wallet's seed.  
Alias: *None*.  

|             | Parameter | Type            | Description
| ---         | ---       | ---             | ---
|**Inputs:**  | *None*.   |                 |
|**Outputs:** | languages | array of string | List of available languages


## **create_wallet**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_wallet","params":{"filename":"mytestwallet","password":"mytestpassword","language":"English"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "create_wallet",
    "params": {
        "filename": "mytestwallet",
        "password": "mytestpassword",
        "language": "English",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "filename": "mytestwallet",
    "password": "mytestpassword",
    "language": "English",
}
rpc_connection.create_wallet(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Create a new wallet. You need to have set the argument "--wallet-dir" when launching monero-wallet-rpc to make this work.  
Alias: *None*.  

|             | Parameter  | Type   | Description
| ---         | ---        | ---    | ---
|**Inputs:**  | *filename* | string | Wallet file name.
|             | *password* | string | (Optional) password to protect the wallet.
|             | *language* | string | Language for your wallets' seed.
|**Outputs:** | *None*.    |        |


## **open_wallet**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"open_wallet","params":{"filename":"mytestwallet","password":"mytestpassword"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "open_wallet",
    "params": {"filename": "mytestwallet", "password": "mytestpassword"},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"filename": "mytestwallet", "password": "mytestpassword"}
rpc_connection.open_wallet(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Open a wallet. You need to have set the argument "--wallet-dir" when launching monero-wallet-rpc to make this work.  
Alias: *None*.  

|             | Parameter  | Type   | Description
| ---         | ---        | ---    | ---
|**Inputs:**  | *filename* | string | wallet name stored in --wallet-dir.
|             | *password* | string | (Optional) only needed if the wallet has a password defined.
|**Outputs:** | *None*.    |        |


## **close_wallet**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"close_wallet"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "close_wallet",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.close_wallet()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Close the currently opened wallet, after trying to save it.  
Alias: *None*.  

|             | Parameter | Type | Description
| ---         | ---       | ---  | ---
|**Inputs:**  | *None*.   |      |
|**Outputs:** | *None*.   |      |


## **change_wallet_password**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"change_wallet_password","params":{"old_password":"theCurrentSecretPassPhrase","new_password":"theNewSecretPassPhrase"}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "change_wallet_password",
    "params": {
        "old_password": "theCurrentSecretPassPhrase",
        "new_password": "theNewSecretPassPhrase",
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "old_password": "theCurrentSecretPassPhrase",
    "new_password": "theNewSecretPassPhrase",
}
rpc_connection.change_wallet_password(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}
```
Change a wallet password.  
Alias: *None*.  

|             | Parameter      | Type   | Description
| ---         | ---            | ---    | ---
|**Inputs:**  | *old_password* | string | (Optional) Current wallet password, if defined.
|             | *new_password* | string | (Optional) New wallet password, if not blank.
|**Outputs:   | *None*.        |        |


## **is_multisig**


> Example for a non-multisig wallet:

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"is_multisig"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "is_multisig",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.is_multisig()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig": false,
    "ready": false,
    "threshold": 0,
    "total": 0
  }
}
```

> Example for a multisig wallet:

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"is_multisig"}' -H 'Content-Type: application/json'                  
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "is_multisig",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.is_multisig()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig": true,
    "ready": true,
    "threshold": 2,
    "total": 2
  }
}
```

Check if a wallet is a multisig one.  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | multisig  | boolean      | States if the wallet is multisig
|             | ready     | boolean      | 
|             | threshold | unsigned int | Amount of signature needed to sign a transfer.
|             | total     | unsigned int | Total amount of signature in the multisig wallet.


## **prepare_multisig**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"prepare_multisig"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "prepare_multisig",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.prepare_multisig()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig_info": "MultisigV1BFdxQ653cQHB8wsj9WJQd2VdnjxK89g5M94dKPBNw22reJnyJYKrz6rJeXdjFwJ3Mz6n4qNQLd6eqUZKLiNzJFi3UPNVcTjtkG2aeSys9sYkvYYKMZ7chCxvoEXVgm74KKUcUu4V8xveCBFadFuZs8shnxBWHbcwFr5AziLr2mE7KHJT"
  }
}
```
Prepare a wallet for multisig by generating a multisig string to share with peers.  
Alias: *None*.  

|             | Parameter     | Type   | Description
| ---         | ---           | ---    | ---
|**Inputs:**  | *None*.       |        |
|**Outputs:** | multisig_info | string | Multisig string to share with peers to create the multisig wallet.


## **make_multisig**


> Example for 2/2 Multisig Wallet:

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_multisig","params":{"multisig_info":["MultisigV1K4tGGe8QirZdHgTYoBZMumSug97fdDyM3Z63M3ZY5VXvAdoZvx16HJzPCP4Rp2ABMKUqLD2a74ugMdBfrVpKt4BwD8qCL5aZLrsYWoHiA7JJwDESuhsC3eF8QC9UMvxLXEMsMVh16o98GnKRYz1HCKXrAEWfcrCHyz3bLW1Pdggyowop"],"threshold":2}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "make_multisig",
    "params": {
        "multisig_info": [
            "MultisigV1K4tGGe8QirZdHgTYoBZMumSug97fdDyM3Z63M3ZY5VXvAdoZvx16HJzPCP4Rp2ABMKUqLD2a74ugMdBfrVpKt4BwD8qCL5aZLrsYWoHiA7JJwDESuhsC3eF8QC9UMvxLXEMsMVh16o98GnKRYz1HCKXrAEWfcrCHyz3bLW1Pdggyowop"
        ],
        "threshold": 2,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "multisig_info": [
        "MultisigV1K4tGGe8QirZdHgTYoBZMumSug97fdDyM3Z63M3ZY5VXvAdoZvx16HJzPCP4Rp2ABMKUqLD2a74ugMdBfrVpKt4BwD8qCL5aZLrsYWoHiA7JJwDESuhsC3eF8QC9UMvxLXEMsMVh16o98GnKRYz1HCKXrAEWfcrCHyz3bLW1Pdggyowop"
    ],
    "threshold": 2,
}
rpc_connection.make_multisig(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "55SoZTKH7D39drxfgT62k8T4adVFjmDLUXnbzEKYf1MoYwnmTNKKaqGfxm4sqeKCHXQ5up7PVxrkoeRzXu83d8xYURouMod",
    "multisig_info": ""
  }
}
```

> Example for 2/3 Multisig Wallet:

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_multisig","params":{"multisig_info":["MultisigV1MTVm4DZAdJw1PyVutpSy8Q4WisZBCFRAaZY7hhQnMwr5AZ4swzThyaSiVVQM5FHj1JQi3zPKhQ4k81BZkPSEaFjwRJtbfqfJcVvCqRnmBVcWVxhnihX5s8fZWBCjKrzT3CS95spG4dzNzJSUcjheAkLzCpVmSzGtgwMhAS3Vuz9Pas24","MultisigV1TEx58ycKCd6ADCfxF8hALpcdSRAkhZTi1bu4Rs6FdRC98EdB1LY7TAkMxasM55khFgcxrSXivaSr5FCMyJGHmojm1eE4HpGWPeZKv6cgCTThRzC4u6bkkSoFQdbzWN92yn1XEjuP2XQrGHk81mG2LMeyB51MWKJAVF99Pg9mX2BpmYFj"],"threshold":2}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "make_multisig",
    "params": {
        "multisig_info": [
            "MultisigV1MTVm4DZAdJw1PyVutpSy8Q4WisZBCFRAaZY7hhQnMwr5AZ4swzThyaSiVVQM5FHj1JQi3zPKhQ4k81BZkPSEaFjwRJtbfqfJcVvCqRnmBVcWVxhnihX5s8fZWBCjKrzT3CS95spG4dzNzJSUcjheAkLzCpVmSzGtgwMhAS3Vuz9Pas24",
            "MultisigV1TEx58ycKCd6ADCfxF8hALpcdSRAkhZTi1bu4Rs6FdRC98EdB1LY7TAkMxasM55khFgcxrSXivaSr5FCMyJGHmojm1eE4HpGWPeZKv6cgCTThRzC4u6bkkSoFQdbzWN92yn1XEjuP2XQrGHk81mG2LMeyB51MWKJAVF99Pg9mX2BpmYFj",
        ],
        "threshold": 2,
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "multisig_info": [
        "MultisigV1MTVm4DZAdJw1PyVutpSy8Q4WisZBCFRAaZY7hhQnMwr5AZ4swzThyaSiVVQM5FHj1JQi3zPKhQ4k81BZkPSEaFjwRJtbfqfJcVvCqRnmBVcWVxhnihX5s8fZWBCjKrzT3CS95spG4dzNzJSUcjheAkLzCpVmSzGtgwMhAS3Vuz9Pas24",
        "MultisigV1TEx58ycKCd6ADCfxF8hALpcdSRAkhZTi1bu4Rs6FdRC98EdB1LY7TAkMxasM55khFgcxrSXivaSr5FCMyJGHmojm1eE4HpGWPeZKv6cgCTThRzC4u6bkkSoFQdbzWN92yn1XEjuP2XQrGHk81mG2LMeyB51MWKJAVF99Pg9mX2BpmYFj",
    ],
    "threshold": 2,
}
rpc_connection.make_multisig(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "51sLpF8fWaK1111111111111111111111111111111111ABVbHNf1JFWJyFp5YZgZRQ44RiviJi1sPHgLVMbckRsDkTRgKS",
    "multisig_info": "MultisigxV18jCaYAQQvzCMUJaAWMCaAbAoHpAD6WPmYDmLtBtazD654E8RWkLaGRf29fJ3stU471MELKxwufNYeigP7LoE4tn2Sscwn5g7PyCfcBc1V4ffRHY3Kxqq6VocSCUTncpVeUskaDKuTAWtdB9VTBGW7iG1cd7Zm1dYgur3CiemkGjRUAj9bL3xTEuyaKGYSDhtpFZFp99HQX57EawhiRHk3qq4hjWX"
  }
}
```
Make a wallet multisig by importing peers multisig string.  
Alias: *None*.  

|             | Parameter       | Type            | Description
| ---         | ---             | ---             | ---
|**Inputs:**  | *multisig_info* | array of string | List of multisig string from peers.
|             | *threshold*     | unsigned int    | Amount of signatures needed to sign a transfer. Must be less or equal than the amount of signature in `multisig_info`.
|             | *password*      | string          | Wallet password 
|**Outputs:** | address         | string          | multisig wallet address.
|             | multisig_info   | string          | Multisig string to share with peers to create the multisig wallet (extra step for N|1/N wallets).


## **export_multisig_info**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_multisig_info"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "export_multisig_info",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.export_multisig_info()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "info": "4d6f6e65726f206d756c7469736967206578706f72740105cf6442b09b75f5eca9d846771fe1a879c9a97ab0553ffbcec64b1148eb7832b51e7898d7944c41cee000415c5a98f4f80dc0efdae379a98805bb6eacae743446f6f421cd03e129eb5b27d6e3b73eb6929201507c1ae706c1a9ecd26ac8601932415b0b6f49cbbfd712e47d01262c59980a8f9a8be776f2bf585f1477a6df63d6364614d941ecfdcb6e958a390eb9aa7c87f056673d73bc7c5f0ab1f74a682e902e48a3322c0413bb7f6fd67404f13fb8e313f70a0ce568c853206751a334ef490068d3c8ca0e"
  }
}
```
Export multisig info for other participants.  
Alias: *None*.  

|             | Parameter | Type   | Description
| ---         | ---       | ---    | ---
|**Inputs:**  | *None*.   |        | 
|**Outputs:** | info      | string | Multisig info in hex format for other participants.



## **import_multisig_info**

##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_multisig_info","params":{"info":["...multisig_info..."]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "import_multisig_info",
    "params": {"info": ["...multisig_info..."]},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"info": ["...multisig_info..."]}
rpc_connection.import_multisig_info(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "n_outputs": 35
  }
}
```
Import multisig info from other participants.  
Alias: *None*.  

|             | Parameter  | Type            | Description
| ---         | ---        | ---             | ---
|**Inputs:**  | *info*     | array of string | List of multisig info in hex format from other participants.
|**Outputs:** | n_outputs  | unsigned int    | Number of outputs signed with those multisig info.


## **finalize_multisig**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"finalize_multisig","params":{"multisig_info":["MultisigxV1JNC6Ja2oBt5Sqea9LN2YEF7WYZCpHqr2EKvPG89Trf3X4E8RWkLaGRf29fJ3stU471MELKxwufNYeigP7LoE4tn2McPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZEKVAQ4HPPyQciSCdNjgwsuFRBzrskMdMUwNMgKst1debYfm37i6PSzDoS2tk4kYTYj83kkAdR7kdshet1axQPd6HQ","MultisigxV1Unma7Ko4zdd8Ps3Af4oZwtj2JdWKzwNfP6s2G9ZvXhMoSscwn5g7PyCfcBc1V4ffRHY3Kxqq6VocSCUTncpVeUskMcPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZE1LTpWxLoC3vPMSrqVVcjnmL9LYfdCZz3fECjNZbCEDq3PHDiUuY5jurQTcNoGhDTio5WM9xaAdim9YByiS5KyqF4"]}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "finalize_multisig",
    "params": {
        "multisig_info": [
            "MultisigxV1JNC6Ja2oBt5Sqea9LN2YEF7WYZCpHqr2EKvPG89Trf3X4E8RWkLaGRf29fJ3stU471MELKxwufNYeigP7LoE4tn2McPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZEKVAQ4HPPyQciSCdNjgwsuFRBzrskMdMUwNMgKst1debYfm37i6PSzDoS2tk4kYTYj83kkAdR7kdshet1axQPd6HQ",
            "MultisigxV1Unma7Ko4zdd8Ps3Af4oZwtj2JdWKzwNfP6s2G9ZvXhMoSscwn5g7PyCfcBc1V4ffRHY3Kxqq6VocSCUTncpVeUskMcPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZE1LTpWxLoC3vPMSrqVVcjnmL9LYfdCZz3fECjNZbCEDq3PHDiUuY5jurQTcNoGhDTio5WM9xaAdim9YByiS5KyqF4",
        ]
    },
}
...
```
##### python; python-monerorpc:
```python
...
params = {
    "multisig_info": [
        "MultisigxV1JNC6Ja2oBt5Sqea9LN2YEF7WYZCpHqr2EKvPG89Trf3X4E8RWkLaGRf29fJ3stU471MELKxwufNYeigP7LoE4tn2McPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZEKVAQ4HPPyQciSCdNjgwsuFRBzrskMdMUwNMgKst1debYfm37i6PSzDoS2tk4kYTYj83kkAdR7kdshet1axQPd6HQ",
        "MultisigxV1Unma7Ko4zdd8Ps3Af4oZwtj2JdWKzwNfP6s2G9ZvXhMoSscwn5g7PyCfcBc1V4ffRHY3Kxqq6VocSCUTncpVeUskMcPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZE1LTpWxLoC3vPMSrqVVcjnmL9LYfdCZz3fECjNZbCEDq3PHDiUuY5jurQTcNoGhDTio5WM9xaAdim9YByiS5KyqF4",
    ]
}
rpc_connection.finalize_multisig(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "5B9gZUTDuHTcGGuY3nL3t8K2tDnEHeRVHSBQgLZUTQxtFYVLnho5JJjWJyFp5YZgZRQ44RiviJi1sPHgLVMbckRsDqDx1gV"
  }
}
```
Turn this wallet into a multisig wallet, extra step for N-1/N wallets.  
Alias: *None*.  

|             | Parameter       | Type            | Description
| ---         | ---             | ---             | ---
|**Inputs:**  | *multisig_info* | array of string | List of multisig string from peers.
|             | *password*      | string          | Wallet password 
|**Outputs:** | address         | string          | multisig wallet address.


## **sign_multisig**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign_multisig","params":{"tx_data_hex":"...multisig_txset..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "sign_multisig",
    "params": {"tx_data_hex": "...multisig_txset..."},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"tx_data_hex": "...multisig_txset..."}
rpc_connection.sign_multisig(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_data_hex": "...multisig_txset...",
    "tx_hash_list": ["4996091b61c1be112c1097fd5e97d8ff8b28f0e5e62e1137a8c831bacf034f2d"]
  }
}
```
Sign a transaction in multisig.  
Alias: *None*.  

|             | Parameter     | Type            | Description
| ---         | ---           | ---             | ---
|**Inputs:**  | *tx_data_hex* | string          | Multisig transaction in hex format, as returned by `transfer` under `multisig_txset`.
|**Outputs:** | tx_data_hex   | string          | Multisig transaction in hex format.
|             | tx_hash_list  | array of string | List of transaction Hash.


## **submit_multisig**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_multisig","params":{"tx_data_hex":"...tx_data_hex..."}}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "submit_multisig",
    "params": {"tx_data_hex": "...tx_data_hex..."},
}
...
```
##### python; python-monerorpc:
```python
...
params = {"tx_data_hex": "...tx_data_hex..."}
rpc_connection.submit_multisig(params)
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_hash_list": ["4996091b61c1be112c1097fd5e97d8ff8b28f0e5e62e1137a8c831bacf034f2d"]
  }
}
```
Submit a signed multisig transaction.  
Alias: *None*.  

|             | Parameter     | Type            | Description
| ---         | ---           | ---             | ---
|**Inputs:**  | *tx_data_hex* | string          | Multisig transaction in hex format, as returned by `sign_multisig` under `tx_data_hex`.
|**Outputs:** | tx_hash_list  | array of string | List of transaction Hash.


## **get_version**


##### shell:
```shell
$ curl -X POST http://localhost:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_version"}' -H 'Content-Type: application/json'
```
##### python; requests:
```python
...
data = {
    "jsonrpc": "2.0",
    "id": "0",
    "method": "get_version",
}
...
```
##### python; python-monerorpc:
```python
...
rpc_connection.get_version()
```
```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "version": 65539
  }
}
```
Get RPC version Major & Minor integer-format, where Major is the first 16 bits and Minor the last 16 bits.  
Alias: *None*.  

|             | Parameter | Type         | Description
| ---         | ---       | ---          | ---
|**Inputs:**  | *None*.   |              |
|**Outputs:** | version   | unsigned int | RPC version, formatted with `Major  2^16 + Minor` (Major encoded over the first 16 bits, and Minor over the last 16 bits).