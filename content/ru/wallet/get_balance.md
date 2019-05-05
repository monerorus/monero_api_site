---
weight: 805
---

## **get_balance**

```shell
  curl -X POST http://127.0.0.1:18082/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_balance","params":{"account_index":0,"address_indices":[0,1]}}' -H 'Content-Type: application/json'
```

```python
  ...^ см. вступление
  data = {
      "jsonrpc": "2.0",
      "id": "0",
      "method": "get_balance",
      "params": {"account_index": 0, "address_indices": [0, 1]},
  }
  ...^ см. вступление
```
```py
  ...^ см. вступление
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
Возвращает информацию о балансе кошелька.  
Alias: *getbalance*.  

|              | Параметр              | Тип                            | Описание
| ---          | ---                    | ---                             | ---
|**Входные:**  | *account_index*        | unsigned int                    | Возвратить баланс данного счета.
|              | *address_indices*      | array of unsigned int           | (Выборочно) Вернуть детализированный баланс для данных подадресов.
|**Выходные:** | balance                | unsigned int                    | Общий баланс кошелька monero-wallet-rpc в текущей сессии.
|              | unlocked_balance       | unsigned int                    | Разблокированный баланс – это те средства, которые уже были подтверждены в блокчейне Monero и считаются безопасными для дальнейшего использования.
|              | multisig_import_needed | boolean                         | True, если для получения правильного баланса требуется импорт данных multisig (мильтиподписей).
|              | per_subaddress         | array of subaddress information | Информация о балансе каждого субадреса в выбранном счете.
|              | ..address_index        | unsigned int                    | Индекс субадреса в счете.
|              | ..address              | string                          | Адрес соответствующий индексу. Base58 представление публичных ключей.
|              | ..balance              | unsigned int                    | Баланс субадреса (заблокированый или разблокированый).
|              | ..unlocked_balance     | unsigned int                    | Разблокированный баланс субадреса.
|              | ..label                | string                          | Метка субадреса.
|              | ..num_unspent_outputs  | unsigned int                    | Количество неизрасходованных выходов, доступных субадресу. 