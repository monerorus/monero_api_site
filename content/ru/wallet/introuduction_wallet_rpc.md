---
weight: 800
title: Wallet RPC API Reference
---

# Wallet RPC 

<aside class="success">
Updated
</aside>


## Введение

```python
  #Эта часть одинакова для всех методов и описана только тут.
  #Для каждого вызова необходимо сначала задать это:
      import requests
      import json
      wallet_url = "http://127.0.0.1:18082/json_rpc"
      header = {"Content-Type": "application/json"}

  #Эта часть у каждого метода своя.
  #Необходимо задать параметры в структуре данных для запроса, например:
      data = {
          "jsonrpc": "2.0",
          "id": "0",
          "method": "get_balance",
          "params": {"account_index": 0, "address_indices": [0, 1]},
      }

  #Эта часть одинакова для всех методов и описана только тут.
  #Для каждого запроса ответ можно получить таким способом:
      response = requests.post(wallet_url, data=json.dumps(data), headers=header)
      response.raise_for_status()
      response.json()
```
```py
  #Эта часть одинакова для всех методов и описана только тут.
  #Для каждого вызова необходимо сначала задать это:
      from monerorpc.authproxy import AuthServiceProxy
      rpc_connection = AuthServiceProxy('http://127.0.0.1:18082/json_rpc')
```

Здесь представлен список всех возможных методов вызова monero-wallet-rpc, их входных и выходных данных, а также примеры применения каждого из них. Программа monero-wallet-rpc заменила интерфейс RPC, который был в simplewallet, а затем появился в monero-wallet-cli.

Все методы monero-wallet-rpc используют один и тот же интерфейс JSON RPC. Например:

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

Если monero-wallet-rpc был запущен с аргументом `--rpc-login` как `username:password`, следует использовать следующий пример:

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
Примечание: "@atomic-units" составляют наименьшую часть от 1 XMR в соответствии с реализацией monerod. <br>
<b>1 XMR = 1e12 @atomic-units.</b>
</aside> 

Данный список был обновлен на заморозке кода 2018-09-14 после слияния коммита bb30a7236725e456138f055f96a634c75ce2b491 (Wallet RPC версия 1.3), высота блока была 1643308.

## JSON RPC Методы: