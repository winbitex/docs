# API

- [简体中文](./README_CN.md)
- `{{MARKET_API_URL}}`: `https://api.winbitex.co/v1/market`

## index

| method                                                  | auth required | description                                              |
|:--------------------------------------------------------|:-------------:|:---------------------------------------------------------|
| [get symbols](#get-symbols)                             |     false     | get all tradable symbols                                 |
| [get tickers](#get-tickers)                             |     false     | get ticker info of all tradable symbols                  |
| [get ticker](#get-ticker)                               |     false     | get last ticker info of the symbol                       |
| [get depth](#get-depth)                                 |     false     | get depth of the symbol                                  |
| [get trades](#get-trades)                               |     false     | get last trade records of the symbol                     |
| [get kline](#get-kline)                                 |     false     | get last kline data of the symbol                        |
| [get bittrex style tickers](#get-bittrex-style-tickers) |     false     | get ticker info of all tradable symbols in bittrex style |

## response description

| field      | required |
|:-----------|:--------:|
| success    |   true   |
| data       |  false   |
| error_code |  false   |

## error code

| code   | description      |
|:-------|:-----------------|
| 150001 | symbol not found |

# get symbols

> [GET] `{{MARKET_API_URL}}/symbols`

## response example

| field         |
|:--------------|
| symbol        |
| price_digits  |
| amount_digits |

```json
{
  "success": true,
  "data": [
    {
      "symbol": "BTCUSDT",
      "price_digits": 6,
      "amount_digits": 4
    },
    {
      "symbol": "ETHUSDT",
      "price_digits": 3,
      "amount_digits": 8
    }
  ]
}
```

# get tickers

> [GET] `{{MARKET_API_URL}}/tickers`

## response example

| field       | description              |
|:------------|:-------------------------|
| last        | last price               |
| high        | highest price in 24h     |
| low         | lowest price in 24h      |
| volume      | trade volume in 24h      |
| change_rate | price change rate in 24h |
| bid         | bid 1 of depth           |
| ask         | ask 1 of depth           |

```json
{
  "success": true,
  "data": {
    "BTCUSDT": {
      "last": 7040.10394,
      "high": 7064.39349,
      "low": 6850.685,
      "volume": 9213.1654,
      "change_rate": 0.00758,
      "bid": {
        "price": 6950.424973,
        "volume": 0.2073
      },
      "ask": {
        "price": 7039.296,
        "volume": 11.6024
      }
    },
    "ETHUSDT": {
      "last": 409.061,
      "high": 409.959,
      "low": 401.54,
      "volume": 91557.23992605,
      "change_rate": 0.00297,
      "bid": {
        "price": 405.221,
        "volume": 0.6855
      },
      "ask": {
        "price": 409.049,
        "volume": 17.2074
      }
    }
  }
}
```

# get ticker

> [GET] `{{MARKET_API_URL}}/ticker?symbol={SYMBOL}`

## request description

| field  | required | default |
|:-------|:--------:|:--------|
| symbol |   true   | -       |

## response example

| field       | description              |
|:------------|:-------------------------|
| last        | last price               |
| high        | highest price in 24h     |
| low         | lowest price in 24h      |
| volume      | trade volume in 24h      |
| change_rate | price change rate in 24h |
| bid         | bid 1 of depth           |
| ask         | ask 1 of depth           |

```json
{
  "success": true,
  "data": {
    "last": 7040.10394,
    "high": 7064.39349,
    "low": 6850.685,
    "volume": 9213.1654,
    "change_rate": 0.00758,
    "bid": {
      "price": 6950.424973,
      "volume": 0.2073
    },
    "ask": {
      "price": 7039.296,
      "volume": 11.6024
    }
  }
}
```

# get depth

> [GET] `{{MARKET_API_URL}}/depth?symbol={SYMBOL}`

## request description

| field  | required | default |
|:-------|:--------:|:--------|
| symbol |   true   | -       |

## response example

| field | description                          |
|:------|:-------------------------------------|
| bids  | depth of bid, order by price descend |
| asks  | depth of ask, order by price ascend  |

```json
{
  "success": true,
  "data": {
    "bids": [
      {
        "price": 6950.424973,
        "volume": 0.2073
      },
      {
        "price": 6950.414972,
        "volume": 0.2085
      }
    ],
    "asks": [
      {
        "price": 7039.296,
        "volume": 11.6024
      },
      {
        "price": 7039.325997,
        "volume": 1.1828
      }
    ]
  }
}
```

# get trades

> [GET] `{{MARKET_API_URL}}/trades?symbol={SYMBOL}`

## request description

| field  | required | default |
|:-------|:--------:|:--------|
| symbol |   true   | -       |

## response example

| field  | description   |
|:-------|:--------------|
| time   | -             |
| price  | -             |
| volume | -             |
| side   | buy:1, sell:2 |

```json
{
  "success": true,
  "data": [
    {
      "time": 1533627534,
      "price": 7040.10394,
      "volume": 0.07,
      "side": 1
    },
    {
      "time": 1533627530,
      "price": 7040.10394,
      "volume": 0.0314,
      "side": 1
    }
  ]
}
```

# get kline

> [GET] `{{MARKET_API_URL}}/kline?symbol={SYMBOL}&period={PERIOD}&limit={LIMIT}`

## request description

| field  | required | default | description                           |
|:-------|:--------:|:--------|:--------------------------------------|
| symbol |   true   | -       | -                                     |
| period |  false   | 5min    | 1min, 5min, 15min, 30min, 1hour, 1day |
| limit  |  false   | 1000    | 1~2000                                |

## response example

| field  | description   |
|:-------|:--------------|
| time   | time begin    |
| open   | open price    |
| high   | highest price |
| low    | lowest price  |
| close  | last price    |
| volume | trade volume  |

```json
{
  "success": true,
  "data": [
    {
      "time": 1533627000,
      "open": 7039.823912,
      "high": 7047.89514,
      "low": 7038.753805,
      "close": 7039.773907,
      "volume": 42.4889
    },
    {
      "time": 1533627300,
      "open": 7039.773907,
      "high": 7041.265803,
      "low": 7039.543884,
      "close": 7040.10394,
      "volume": 65.4688
    }
  ]
}
```

# get bittrex style tickers

> [GET] `{{MARKET_API_URL}}/bittrex/marketsummaries`

## response example

| field      | description          |
|:-----------|:---------------------|
| MarketName | symbol               |
| High       | highest price in 24h |
| Low        | lowest price in 24h  |
| Volume     | trade volume in 24h  |
| Last       | last price           |
| TimeStamp  | data timestamp       |
| Bid        | bid 1 price          |
| Ask        | ask 1 price          |
| PrevDay    | price before 24h     |

```json
{
  "success": true,
  "data": [
    {
      "MarketName": "BTCUSDT",
      "High": 6759.96,
      "Low": 6441.1,
      "Volume": 1075.7755,
      "Last": 6743.1,
      "TimeStamp": "2018-09-28T06:27:33.255",
      "Bid": 6743.1,
      "Ask": 6744,
      "PrevDay": 6472.34
    },
    {
      "MarketName": "ETHUSDT",
      "High": 233.39,
      "Low": 210.5,
      "Volume": 23950.4596,
      "Last": 231.34,
      "TimeStamp": "2018-09-28T06:27:33.256",
      "Bid": 230.97,
      "Ask": 231.41,
      "PrevDay": 215.47
    }
  ]
}
```
