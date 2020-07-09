# Cryptocurrency Combination Spread Data
This repository is provided to give access to developers who wish to pull down the executium `spread` data.

## Demo
There is a useful [online demo provided by executium here](https://marketdata.executium.com/spread-data-demo/)

![spread](https://i.imgur.com/zKTjg21.jpg)

## API Endpoint: Fetch Spread Data
Spreads are calculated as Ask-Bid for price, and Ask/Bid for ratio.

```
POST /api/v2/public/fetch-spread-data
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
combination | 1 | YES |  | Provide a valid combination such as `binance-btcusdt+bitmax-btcusdc`. The `+` acts as a join for the combination. The order is ascending by time.
latestonly |  | NO |  | Set as `true` to activate. Useful to pull when you are only looking to update the latest point


**Successful Response Payload:**
```javascript


   "data":[
      {
         "price":{
            "open":9.14,
            "close":9.52,
            "high":9.52,
            "low":8.23,
            "time":"1594294380000"
         },
         "ratio":{
            "open":1.001,
            "close":1.001,
            "high":1.001,
            "low":1.0009,
            "time":"1594294380000"
         }
      }
   ],
	
```

## API Endpoint: Symbols
All symbols listed and supported on executium. This `endpoint` also accepts `GET`, you can filter the data using the `exchange` parameter, for example `GET /api/v2/system/symbols?exchange=bifinex`.

To get a working code you need to combine the `exchange` with the `id`. For example `binance-ethbtc` is a combination of the two. So `binance-ethbtc+bitfinex-ethbtc` would provide the candle data for that combination.

```
POST /api/v2/system/symbols
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
exchange |  | NO |  | Filter the data by exchange.


**Successful Response Payload:**
```javascript
{
  "data": {
    "binance": [
      {
        "id": "ethbtc",
        "symbol": "ETH/BTC",
        "quote": "BTC",
        "base": "ETH",
        "min": 0.000001,
        "pp": 6,
        "pa": 3
      },
      {
        "id": "ltcbtc",
        "symbol": "LTC/BTC",
        "quote": "BTC",
        "base": "LTC",
        "min": 0.000001,
        "pp": 6,
        "pa": 2
      },
      ...
      ...
      ...
    "bitfinex": [
      {
        "id": "btcusd",
        "symbol": "BTC/USD",
        "quote": "USD",
        "base": "BTC",
        "min": 0.000009999999999999999,
        "pp": 5,
        "pa": -1
      },
      {
        "id": "ltcusd",
        "symbol": "LTC/USD",
        "quote": "USD",
        "base": "LTC",
        "min": 0.000009999999999999999,
        "pp": 5,
        "pa": -1
      },
      ...
      ...

      
```

## API Endpoint: Match Pairs
This system is provided to give insight into a `pairing` and where you can also trade it. For this endpoint we accept both `POST` and `GET`. An example of `GET` would be `https://marketdata.executium.com/api/v2/public/match-pair?code=btcusdt,btcusd`. 

```
POST /api/v2/public/match-pair
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
code | 1 | YES |  | Provide a pair such as `btcusdt` to discover where else you can trade the pairing `btcusdt`. Comma delimited list acceptable upto 10. Exclude the exchange code from your query and request just the pair like shown.
limit |  | NO | 10 | 
pagenumber |  | NO | 1 | 


**Successful Response Payload:**
```javascript


{
  "data": {
  
      "BTCUSDT": {
      "pair": "btcusdt",
      "count": 14,
      "active": [
        "Binance",
        "Bitfinex",
        "Bitmart",
        "Bitmax",
        "Bittrex",
        "Ftx",
        "Gateio",
        "Huobipro",
        "Kraken",
        "Kucoin",
        "Liquid",
        "Okex",
        "Poloniex",
        "Upbit"
      ],
      "detail": {
        "binance": {
          "id": "btcusdt",
          "symbol": "BTC/USDT",
          "quote": "USDT",
          "base": "BTC",
          "min": 0.01,
          "pp": 2,
          "pa": 6
        },
        "bitfinex": {
          "id": "btcusdt",
          "symbol": "BTC/USDT",
          "quote": "UST",
          "base": "BTC",
          "min": 0.000009999999999999999,
          "pp": 5,
          "pa": -1
        },
        ...
        ...
        ...

      },
      "possible_combinations": 196
    },
    "BTCUSD": {
      "pair": "btcusd",
      "count": 11,
      "active": [
        "Bitfinex",
        "Bitflyer",
        "Bitmex",
        "Bitstamp",
        "Bittrex",
        "Coinbase",
        "Coinbasepro",
        "Ftx",
        "Itbit",
        "Kraken",
        "Liquid"
      ],
      "detail": {
        "bitfinex": {
          "id": "btcusd",
          "symbol": "BTC/USD",
          "quote": "USD",
          "base": "BTC",
          "min": 0.000009999999999999999,
          "pp": 5,
          "pa": -1
        },
        ...
        ...
        ...
		}
	}
	

```

