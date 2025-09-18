# 1. getblock.io
Hello! 

Thank you for contacting us. I have analyzed your request and explain why it is not working and how to fix it.
1. You are using `GET` instead of `POST` — JSON-RPC GetBlock's methods (including `eth_estimateGas`) use `POST`-requests ([docs](https://docs.getblock.io/guides/testing-rpc-connection/using-curl-for-testing)).
2. There is no URL access token — for the additional access to GetBlock API, the endpoint should look like `https://go.getblock.io /<ACCESS_TOKEN>/` — the request will not be available to the account without the token ([docs](https://docs.getblock.io/guides/testing-rpc-connection/using-curl-for-testing)).

### Here is a corrected working example
```bash
curl -location - publication request 'https://go.getblock.io /<TOKEN ACCESS>/' \
--header "Content type: application/json" \
-- raw data'{
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "parameters": [
    {
      "from whom": "0xFE3B557E8Fb62b89F4916B721be55cEb828dBd73",
      "to whom": "0x44Aa93095D6749A706051658B970b941c72c1D53",
      "value":"0x1"
    }
  ],
  "identifier": "getblock.io "
}'
```

Always in touch,<br/>
Your Technical Support


# 2. Trezor
Hello!

Thank you for contacting us. I have analyzed your request and explain why it is not working and how to fix it.
1. Non-existent REST endpoint — /api/v2/gettxout/<txid> is Bitcoin Core endpoint. In Blockbook REST you need to use `GET /api/v2/utxo/<txid>`.
2. The problematic syntax of curl is that you have a `--request GET \ --url` with \ and spaces in the middle of the string. This will break the shell command.
3. API key header — there no need for the key.

### Here is a corrected working example
```bash
curl --request GET --url \
https://btc4.trezor.io/api/v2/utxo/<address>
```

Always in touch,<br/>
Your Technical Support


# 3.  DOGE blockbook
Запрос к DOGE
```bash
curl -sS \
  --request GET \
  --url "https://doge1.trezor.io/api/v2/status" \
  --header "Accept: application/json"
```
Ответ. Нас интересует bestHeight, оно совпадает с количеством блоков на [https://blockchair.com/dogecoin](Blockchair)
```json
{
  "blockbook": {
    "coin": "Dogecoin",
    "network": "DOGE",
    "host": "backend10",
    "version": "0.5.0",
    "gitCommit": "ae0172dd",
    "buildTime": "2025-06-10T13:11:59+00:00",
    "syncMode": true,
    "initialSync": false,
    "inSync": true,
    "bestHeight": 5881802,
    "lastBlockTime": "2025-09-18T09:35:54.864086439Z",
    "inSyncMempool": true,
    "lastMempoolTime": "2025-09-18T11:38:28.784687067+02:00",
    "mempoolSize": 236,
    "decimals": 8,
    "dbSize": 134833966839,
    "hasFiatRates": true,
    "currentFiatRatesTime": "2025-09-18T09:30:00.359077455Z",
    "about": "Blockbook - blockchain indexer for Trezor Suite https://trezor.io/trezor-suite. Do not use for any other purpose."
  },
  "backend": {
    "chain": "main",
    "blocks": 5881802,
    "headers": 5881802,
    "bestBlockHash": "c18e8e2e11c1c4360e2cde6038d1e05ed927a521344b861faa3e8c6411c265dc",
    "difficulty": "44013175.26501506",
    "sizeOnDisk": 195870775812,
    "version": "1140900",
    "subversion": "/Shibetoshi:1.14.9/",
    "protocolVersion": "70015"
  }
}
```
