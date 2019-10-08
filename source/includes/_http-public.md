# Public HTTP API

The public HTTP API allows read access to public market data.

## Get Market List

This endpoint returns all TOP.ONE's supported trading symbol.

> Request: Get Market List

```shell
curl "https://gateway.topone.run/t/v1/market/list"
```

> Response: Get Market List

```json
{
    "code": 0,
    "data": {
        "list": [
            {
                "name": "BTC/USDT",
                "stockName": "BTC",
                "stockPrec": 6,
                "moneyName": "USDT",
                "moneyPrec": 4,
                "feePrec": 4,
                "minAmount": "10.00000000",
                "isTrading": true
            }
        ]             
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
name | String | market name
stockName | String | stock coin name
stockPrec | Integer | stock coin precision
moneyName | String | base coin 
moneyPrec | Integer | base coin precision
feePrec | String | fee precision
minAmount | String | order min amount
isTrading | Boolean | trading status

## Get Latest Tickers for All Pairs

Retrieves summary information for each currency pair listed on the exchange. 

> Request: Get Latest Tickers for All Pairs

```shell
curl "https://gateway.topone.run/t/v1/market/ticker"
```

> Response: Get Latest Tickers for All Pairs

```json
{
    "code": 0,
    "data": {
        "BTC/USDT": {
            "lastPrice": "10255.5341",
            "lowestAsk": "10289",
            "highestBid": "10009",
            "percentChange": "0.0240414333045545",
            "baseVolume": "34139211.2527106788",
            "quoteVolume": "3363.760377",
            "high24hr": "10288.9997",
            "low24hr": "10009.0027"
        }
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
lastPrice | String | Execution price for the most recent trade for this pair.
lowestAsk | String | Lowest current purchase price for this asset.
highestBid | String | Highest current sale price for this asset.
percentChange | String | Price change percentage.
baseVolume | String | Base units traded in the last 24 hours.
quoteVolume | String | Quoted units traded in the last 24 hours.
isFrozen | String | Indicates if this market is currently trading or not.
high24hr | String | The highest execution price for this pair within the last 24 hours.
low24hr | String | The lowest execution price for this pair within the last 24 hours.


## Get Market Depth

This endpoint retrieves the current order book of a specific pair.

> Request: Get Market Depth

```shell
curl "https://gateway.topone.run/t/v1/market/depth?market=BTC/USDT"
```

Query Params: 

Field | Data Type | Description
------|-----------|------------
market | String | market name

> Response: Get Market Depth

```json
{
    "code": 0,
    "data": {
        "time": 1569493654.07239,
        "asks": [
            ["8443.04", "0.474139"],
            ["8446.88", "0.052319"],
            ["8447.21", "0.490829"]
        ],
        "bids": [
            ["8416.54", "0.071663"],
            ["8403.51", "0.13025"],
            ["8394.36", "0.019315"]
        ]
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
time | Float | create time
asks | Array | [price, amount] order by price asc
bids | Array | [price, amount] order by price desc
   

## Get the Most Recent Trades

This endpoint retrieves the most recent trades with their price, volume, and direction.

> Request: Get the Most Recent Trades

```shell
curl "https://gateway.topone.run/t/v1/market/recent/trades?market=BTC/USDT"
```

Query Params: 

Field | Data Type | Description
------|-----------|------------
market | String | market name

> Response: Get the Most Recent Trades

```json
{
    "code": 0,
    "data": {
        "list": [
            [1569487995.803009, "10255.5341", "0.019399", 2],
            [1569487995.802333, "10179.5404", "0.033313", 2],
            [1569487995.794085, "10196.5787", "0.032284", 2]
        ]
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
list.item | Array | [time, price, amount, side]  side(1:sell,2:buy)


## Get Historical Trades

Get historical trades

> Request: Get Historical Trades

```shell
curl "https://gateway.topone.run/t/v1/market/historical/trades?market=BTC/USDT&pageSize=100&pageCursor=0&pageMark=0"
```

Query Params:

Field | Data Type | Description
------|-----------|------------
market | String | market name, eg. BTC/USDT
pageSize | Integer | Default 100, max 500.
pageCursor | Integer | `id` of the last item returned from the last request, default 0
pageMark | Integer | Get from the last request, default 0

> Response: Get Historical Trades

```json
{
    "code": 0,
    "data": {
        "pageMark": 1567267200,     // For the next request
        "list": [
            {
                "id": 200556,
                "createTime": 1569487486.22367,
                "side": 2,
                "price": "10177.39430000",
                "dealStock": "0.04687400"
            },
            {
                "id": 200555,
                "createTime": 1569487486.192549,
                "side": 1,
                "price": "10194.60830000",
                "dealStock": "0.03480500"
            }
        ]
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
id | Integer | id
createTime | Float | create time
side | Integer | 1:sell, 2:buy
price | String | deal price
dealStock | String | deal amount
