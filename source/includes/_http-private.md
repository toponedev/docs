# Private HTTP API

The private HTTP API allows read / write access to your private account. You have to use [API Token](#get-api-token) to send requests.

## Get Balances

This endpoint returns all supported market. 

> Request: Get Balances

```shell
curl -X GET \
     -H "Authorization: YOUR_API_TOKEN" \
     https://gateway.topone.run/t/v1/balance/query?assets=BTC,EOS,ETH
```

Query Params:

Field | Data Type | Description
------|-----------|------------
assets | String | List of assets you want to query, separate by `,`

> Response: Get Balances

```json
{   
   "code": 0,
   "data": {
       "list": [
           {
               "asset": "ETH",                  
               "available": "8517.32476151",    
               "freeze": "0",                  
               "total": "8517.32476151",        
               "anchorValue": "0.00003567"      
           }
       ]
   }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
asset | String | asset name
available | String | available balance
freeze | String | order freeze
total | String | total balance
anchorValue | Integer | BTC valuation

## Get All Open Orders

This endpoint returns all supported market.

> Request: Get All Open Orders

```shell
curl -X GET \
     -H "Authorization: YOUR_API_TOKEN" \
     https://gateway.topone.run/t/v1/order/query?market=BTC/USDT&page=1&pageSize=20
```

Query Params:

Field | Data Type | Description
------|-----------|------------
market | String | market name
page | Integer | current page
pageSize | Integer | Number of displays per page

> Response: Get All Open Orders

```json
{   
   "code": 0,
   "data": {
       "total": 1,
       "list": [
           {
               "id": 26211,                      
               "type": 1,                         
               "market": "TOP/ETH",              
               "side": 2,                        
               "createTime": 1526205633.6342139,  
               "updateTime": 1526205633.6342139,  
               "price": "0.00001057",                     
               "amount": "10000",                 
               "left": "10000",                   
               "dealStock": "0",                 
               "dealMoney": "0"                
           }
       ]
   }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
id | Integer | order id
type | Integer | 1: limit order 2: market order
market | String | market name
side | Integer | 1: sell 2: buy 
createTime | Float | order time
updateTime | Float | update time
price | String | order price
amount | String | order amount
left | String | order left
dealStock | String | quote volume
dealMoney | String | base volume

## Limit Order

This endpoint place a new limit order and send to the exchange to be matched.


> Request: Limit Order

```shell
curl -X POST \
     -H "Authorization: YOUR_API_TOKEN" \
     -H "Content-type: application/json" \
     -d '{"market": "TOP/ETH", "side": 2, "amount": "1000", "price": "0.00001057"}' \
     https://gateway.topone.run/t/v1/order/limit
```

Input Params:

Field | Data Type | Description
------|-----------|------------
market | String | market name
side | Integer | 1: sell 2: buy
amount | String | order size 
price | String | The limit price of limit order

> Response: Limit Order

```json
{
    "code": 0,
    "data": {
        "id": 26211,                       
        "type": 1,                         
        "market": "TOP/ETH",               
        "side": 2,                         
        "createTime": 1526205633.6342139,  
        "updateTime": 1526205633.6342139,  
        "price": "0.00001057",             
        "status": 1,                       
        "amount": "10000",                 
        "left": "10000",                   
        "dealStock": "0",                  
        "dealMoney": "0"          
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
id | Integer | order id
type | Integer | 1: limit order 2: market order
market | String | market name
side | Integer | 1: sell 2: buy 
createTime | Float | order time
updateTime | Float | update time
price | String | order price
status | Integer | 1:pending  2:completed  3:canceled 4:partial-canceled
amount | String | order amount
left | String | order left
dealStock | String | quote volume
dealMoney | String | base volume

## Market Order

This endpoint place a new market order and send to the exchange to be matched.

> Request: Market Order

```shell
curl -X POST \
     -H "Authorization: YOUR_API_TOKEN" \
     -H "Content-type: application/json" \
     -d '{"market": "TOP/ETH", "side": 2, "amount": "1000"}' \
     https://gateway.topone.run/t/v1/order/market
```

Input Params:

Field | Data Type | Description
------|-----------|------------
market | String | market name
side | Integer | 1: sell 2: buy
amount | String | order size 

> Response: Market Order

```json
{
    "code": 0,
    "data": {
        "id": 5104074,
        "market": "TOP/ETH",
        "type": 1,
        "side": 1,
        "createTime": 1560843193.14178,
        "updateTime": 1560843193.14178,
        "status": 1,
        "price": "0.0123",
        "amount": "1000",
        "left": "1000",
        "dealStock": "0",
        "dealMoney": "0"
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
id | Integer | order id
type | Integer | 1: limit order 2: market order
market | String | market name
side | Integer | 1: sell 2: buy 
createTime | Float | order time
updateTime | Float | update time
price | String | order price
status | Integer | 1:pending  2:completed  3:canceled 4:partial-canceled
amount | String | order amount
left | String | order left
dealStock | String | quote volume
dealMoney | String | base volume

## Cancel Order

This endpoint submit a request to cancel an order.

> Request: Cancel Order

```shell
curl -X POST \
     -H "Authorization: YOUR_API_TOKEN" \
     -H "Content-type: application/json" \
     -d '{"market": "TOP/ETH", "orderId": 5104074}' \
     https://gateway.topone.run/t/v1/order/cancel
```

Input Params:

Field | Data Type | Description
------|-----------|------------
market | String | market name
orderId | Integer | order id

> Response: Cancel Order

```json
{
    "code": 0,
    "data": {
        "id": 26316, 
        "type": 1, 
        "market": "TOP/ETH", 
        "side": 2, 
        "createTime": 1526209523.637193, 
        "updateTime": 1526209523.637193, 
        "price": "0.0000101", 
        "dealMoney": "0", 
        "status": 3, 
        "amount": "10000",
        "left": "10000", 
        "dealStock": "0"
    }
}
```


Response data:

Field | Data Type | Description
------|-----------|------------
id | Integer | order id
type | Integer | 1: limit order 2: market order
market | String | market name
side | Integer | 1: sell 2: buy 
createTime | Float | order time
updateTime | Float | update time
price | String | order price
status | Integer | 1:pending  2:completed  3:canceled 4:partial-canceled
amount | String | order amount
left | String | order left
dealStock | String | quote volume
dealMoney | String | base volume

## Get Historical Orders

This endpoint returns historical orders based on a specific searching criteria.

> Request: Get Historical Orders

```shell
curl -X GET \
     -H "Authorization: YOUR_API_TOKEN" \
     https://gateway.topone.run/t/v1/order/history?pageMark=0&pageCursor=0&pageSize=20&market=TOP/ETH&side=1&startTime=0&endTime=0
```

Query Params:

Field | Data Type | Description
------|-----------|------------
pageSize | Integer | Default 100, max 500.
pageCursor | Integer | `id` of the last item returned from the last request, default 0
pageMark | Integer | Get from the last request, default 0
market | String | market name
side | Integer | 1:sell 2:buy
startTime | Integer | unix timestamp
endTime | Integer | unix timestamp

> Response: Get Historical Orders

```json
{
    "code": 0,
    "data": {
        "pageMark": 1559318400,     // For the next request
        "list": [
            {
                "id": 26316,                        
                "status": 3,                        
                "dealMoney": "0",                   
                "createTime": 1526209523.637193,    
                "side": 2,                          
                "finishTime": 1526209523.637193,    
                "market": "TOP/ETH",                
                "type": 1,                          
                "price": "0.0000101",               
                "amount": "10000",       
                "dealStock": "0"            
            }
        ]
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
id | Integer | order id
type | Integer | 1: limit order 2: market order
market | String | market name
side | Integer | 1: sell 2: buy 
createTime | Float | order time
updateTime | Float | update time
price | String | order price
status | Integer | 1:pending  2:completed  3:canceled 4:partial-canceled
amount | String | order amount
left | String | order left
dealStock | String | quote volume
dealMoney | String | base volume

## Get Historical Trades

This endpoint returns historical trades based on a specific searching criteria.

> Request: Get Historical Trades

```shell
curl -X GET \
     -H "Authorization: YOUR_API_TOKEN" \
     https://gateway.topone.run/t/v1/deals/history?pageMark=0&pageCursor=0&pageSize=20&market=TOP/ETH&startTime=0&endTime=0
```

Query Params:

Field | Data Type | Description
------|-----------|------------
pageSize | Integer | Default 100, max 500.
pageCursor | Integer | `id` of the last item returned from the last request, default 0
pageMark | Integer | Get from the last request, default 0
market | String | market name
startTime | Integer | unix timestamp
endTime | Integer | unix timestamp

> Response: Get Historical Trades

```json
{
    "code": 0,
    "data": {
        "pageMark": 1559318400,     // For the next request
        "list": [
            {
                "createTime": 1526209901.418669,    
                "market": "TOP/ETH",                 
                "dealId": 47521,                    
                "side": 2,                          
                "price": "0.00600000",              
                "dealStock": "16.00000000",         
                "dealMoney": "0.0960000000000000",  
                "feeAsset": "TOP",                 
                "fee": "0E-16"
            }
        ]
    }
}
```

Response data:

Field | Data Type | Description
------|-----------|------------
createTime | Float | deal time
market | Integer | market name
dealId | String | deal id
side | Integer | 1: sell 2: buy 
price | Float | deal price
dealStock | Float | deal quote volume
dealMoney | String | deal base volume
feeAsset | Integer | fee coin
fee | String | fee amount
