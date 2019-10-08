# Websocket Introduction

## Heartbeat and Connection

When the user's Websocket client connects to the TOP.ONE Websocket server, the server sends `ping` messages to it regularly.

When the user's Websocket client receives this heartbeat message, it should reply to the `pong` message.

When the Websocket server does not receive any `pong` messages within 3 minutes, the server will actively disconnect from the client.


## Subscribe to Topic

> Subscribe request

```json
{
  "id":"1",
  "method": "sub_kline_BTC/USDT_1m",  
  "params": {},
  "lang": "zh-CN"
}
```

To receive data you have to send a "sub" message first.

`{"id": "id generate by client", "method": "topic to sub", "params": {}, "lang": "zh-CN"}`

> Subscribe response

```json
{
  "code": 0,
  "msg": "OK",
  "id":"1",
  "method": "sub_kline_BTC/USDT_1m",  
  "data": {},
  "ts": 1569569618759
}
```

After successfully subscribed, you will receive a response to confirm subscription

`{"code": 0, "msg": "OK", "id": "id generate by client", "method": "topic to sub", "data": {}, "ts": 1569569618759}`

> Topic update

```json
{
  "method": "sub_kline_BTC/USDT_1m",
  "ts": 1561948335075,
  "data": {
    "list": [
      [1521700740, "0.08040", "0.07850", "0.08067", "0.07850", "35.585", "2.82398955"]
    ]
  }
}
```

Then, you will received message when there is update in this topic

`{"method": "topic to sub", "data": {}, "ts": 1561948335075}`

## Unsubscribe

> Unsubscribe request

```json
{
  "id":"1",
  "method": "unsub_kline_BTC/USDT_1m",  
  "params": {},
  "lang": "zh-CN"
}
```

To unsubscribe, you need to send below message

`{"id": "id generate by client", "method": "topic to unsub", "params": {}, "lang": "zh-CN"}`

> Unsubscribe response

```json
{
  "code": 0,
  "msg": "OK",
  "id":"1",
  "method": "unsub_kline_BTC/USDT_1m",  
  "data": {},
  "ts": 1569569618759
}
```

And you will receive a message to confirm the unsubscribe

`{"code": 0, "msg": "OK", "id": "id generate by client", "method": "topic to unsub", "data": {}, "ts": 1569569618759}`

## Pull Data

While connected to websocket, you can also use it in pull style by sending message to the server.

> Pull request

```json
{
  "id":"1",
  "method": "req_kline_BTC/USDT_1m",
  "params": {
    "from": 1561948335,
    "to": 1562948335
  },
  "lang": "zh-CN"
}
```

To request pull style data, you send below message

`{"id": "id generate by client", "method": "topic to req", "params": {}, "lang": "zh-CN"}`

> Pull response

```json
{
  "code": 0,
  "msg": "",
  "id": "1",
  "method": "req_kline_BTC/USDT_1m",
  "ts": 1561948335075,
  "data": {
    "list": [
      [1521700740, "0.08040", "0.07850", "0.08067", "0.07850", "35.585", "2.82398955"]
    ]
  }
}
```

You will receive a response accordingly and immediately

`{"code": 0, "msg": "OK", "id": "id generate by client", "method": "topic to pull", "data": {}, "ts": 1561948335075}`





# Public Websocket 


## Public Websocket URL

`wss://gateway.topone.run/ws/`

## Market Candlestick

This topic sends a new candlestick whenever it is available.

### Subscribe

> Subscribe request

```json
{
  "id":"1",
  "method": "sub_kline_$market_$period",  
  "params": {},
  "lang": "zh-CN"
}
```

Method: `sub_kline_$market_$period`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name
$period | String | 1m, 5m, 10m, 15m, 30m, 1h, 2h, 4h, 6h, 12h, 1d, 1w, 1mon

> Subscribe response

```json
{
  "code": 0,
  "msg": "",
  "id": "1",
  "method": "sub_kline_$market_$period",
  "ts": 1561948335075
}
```

> Subscribe Update example

```json
{
  "method": "sub_kline_TOP/ETH_1m",
  "ts": 1561948335075,
  "data": {
    "list": [
      [1521700740, "0.08040", "0.07850", "0.08067", "0.07850", "35.585", "2.82398955"] 
    ]
  }
}
```

Update Data:

Field | Data Type | Description
------|-----------|------------
list.item | Array | [time, Open, Close, High, Low, quoteVolume, baseVolume]
    
### Unsubscribe

> Unsubscribe request

```json
{
  "id":"1",
  "method": "unsub_kline_$market_$period",
  "params": {},
  "lang": "zh-CN"
}
```

Method: `unsub_kline_$market_$period`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name
$period | String | 1m, 5m, 10m, 15m, 30m, 1h, 2h, 4h, 6h, 12h, 1d, 1w, 1mon

> Unsubscribe response

```json
{
  "code": 0,
  "msg": "",
  "id": "1",
  "method": "unsub_kline_$market_$period",
  "ts": 1561948335075
}
```

### Pull Data

Pull request is supported with extra parameters to define the range. The maximum number of ticks in each response is 300.

> Pull request

```json
{
  "id":"1",
  "method": "req_kline_$market_$period",
  "params": {
    "from": 1561948335,
    "to": 1562948335
  },
  "lang": "zh-CN"
}
```

Method: `req_kline_$market_$period`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name
$period | String | 1m, 5m, 10m, 15m, 30m, 1h, 2h, 4h, 6h, 12h, 1d, 1w, 1mon


> Pull response

```json
{
  "id": "1",
  "method": "req_kline_$market_$period",
  "code": 0,
  "msg": "",
  "ts": 1561948335075,
  "data": {
    "list": [
      [1521700740, "0.08040", "0.07850", "0.08067", "0.07850", "35.585", "2.82398955"] 
    ]
  }
}
```

Pull Response Data:

Field | Data Type | Description
------|-----------|------------
list.item | Array | [time, Open, Close, High, Low, quoteVolume, baseVolume]


## Market Depth

This topic sends the latest market depth when it is updated.

### Subscribe

> Subscribe request

```json
{
  "id": "1",
  "method": "sub_depth_$market_$type",  
  "params": {},
  "lang": "zh-CN"
}
```

Method: `sub_depth_$market_$type`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name
$type | String | 1x, 10x, 100x, 1000x


> Subscribe response

```json
{
  "id": "1",
  "method": "sub_depth_$market_$type",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```

> Subscribe Update example

```json
{
  "method": "sub_depth_TOP/ETH_1x",
  "ts": 1561948335075,
  "data": {
    "time": 1521702329.776686,
    "asks": [                           
      ["0.0791", "2.038"]          
    ],
    "bids": [                       
      ["0.0793", "2.151"]
    ]
  }
}
```

Update Data:

Field | Data Type | Description
------|-----------|------------
time | Float | create time
asks | Array | sell orders [price, amount]
bids | Array | buy orders [price, amount]

### Unsubscribe 

> Unsubscribe request

```json
{
  "id":"1",
  "method": "unsub_depth_$market_$type",
  "params": {},
  "lang": "zh-CN"
}
```

Method: `unsub_depth_$market_$type`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name
$type | String | 1x, 10x, 100x, 1000x

> Unsubscribe response

```json
{
  "id": "1",
  "method": "unsub_depth_$market_$type",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```

## Ticker Data

Subscribe to ticker updates for all currency pairs.

### Subscribe

> Subscribe request

```json
{
  "id": "1",
  "method": "sub_deals_$market", 
  "params": {},
  "lang": "zh-CN"
}
```

Method: `sub_deals_$market`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name

> Subscribe response

```json
{
  "id": "1",
  "method": "sub_deals_$market",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```

> Subscribe Update example

```json
{
  "method": "sub_deals_TOP/ETH",
  "ts": 1561948335075,
  "data": {
    "list": [
      [1521702193.322789, "0.07877", "1.115", 1]   // 
    ]
  }
}
```


Update Data:

Field | Data Type | Description
------|-----------|------------
list.item | Array | [time, price, quoteVolume, side(1:sell,2:buy)]
 
### Unsubscribe
 
> Unsubscribe request

```json
{
  "id": "1",
  "method": "unsub_deals_$market", 
  "params": {},
  "lang": "zh-CN"
}
```


Method: `unsub_deals_$market`

Method Params:

Field | Data Type | Description
------|-----------|------------
$market | String | market name

> Unsubscribe response

```json
{
  "id": "1",
  "method": "unsub_deals_$market",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```
