# Private Websocket 

## General

You have to use [API Token](#get-api-token) to connect to private websocket server. 

<aside class="info"><b>You need to set the connection request header "Origin" to empty, otherwise you will not be able to establish the connection and get a 403 HTTP Status Code.</b></aside>

## Private Websocket URL

`wss://gateway.topone.run/ws/user/?token=YOUR_API_TOKEN`

## Subscribe to Account Updates

This topic publishes all balance updates of the current account.

### Subscribe

> Subscribe request

```json
{
  "id":"1",
  "method": "sub_balance",
  "params": {},
  "lang": "zh-CN"
} 
```


Method: `sub_balance`


> Subscribe response

```json
{
  "id": "1",
  "method": "sub_balance",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```

> Subscribe Update example

```json
{
  "method": "sub_balance",
  "ts": 1561948335075,
  "data": {
    "asset": "ETH", 
    "available": "99999980.24173",
    "freeze": "23.596"
  }
}
```

Update Data:

Field | Data Type | Description
------|-----------|------------
asset | String | asset name
available | String | available balance
freeze | String | order freeze

### Unsubscribe

> Unsubscribe request

```json
{
  "id":"1",
  "method": "unsub_balance",
  "params": {},
  "lang": "zh-CN"
} 
```

Method: `unsub_balance`

> Unsubscribe response

```json
{
  "id": "1",
  "method": "unsub_balance",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```

## Subscribe to Order Updates

This topic publishes all order updates of the current account.

### Subscribe

> Subscribe request

```json
{
  "id":"1",
  "method": "sub_orders",
  "params": {},
  "lang": "zh-CN"
} 
```

Method: `sub_orders`

> Subscribe response

```json
{
  "id": "1",
  "method": "sub_orders",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```

> Subscribe Update example

```json
{
  "method": "sub_orders",
  "ts": 1561948335075,
  "data": {
    "id": 132991,                      
    "market": "ETH/BTC",               
    "type": 1,                         
    "side": 2,                         
    "status": 2,                       
    "price": "0.08132",                
    "amount": "1.389",                 
    "left": "0",                       
    "dealStock": "1.389",              
    "dealMoney": "0.10953654",        
    "createTime": 1522235513.740678,   
    "updateTime": 1522235513.740684    
  }
}
```

Update Data:

Field | Data Type | Description
------|-----------|------------
id | Integer | order id
type | Integer | 1: limit order 2: market order
market | String | market name
side | Integer | 1: sell 2: buy 
status | Integer | 1:pending  2:completed  3:canceled 4:partial-canceled
createTime | Float | order time
updateTime | Float | update time
price | String | order price
amount | String | order amount
left | String | order left
dealStock | String | quote volume
dealMoney | String | base volume

### Unsubscribe

> Unsubscribe request

```json
{
  "id":"1",
  "method": "unsub_orders",
  "params": {},
  "lang": "zh-CN"
} 
```
Method: `unsub_orders`

> Unsubscribe response

```json
{
  "id": "1",
  "method": "unsub_orders",
  "code": 0,
  "msg": "",
  "ts": 1561948335075
}
```
