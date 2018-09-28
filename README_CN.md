# API

- `{{MARKET_API_URL}}`: `https://api.winbitex.co/v1/market`

## index

| method                                                  | auth required | description                          |
|:--------------------------------------------------------|:-------------:|:-------------------------------------|
| [get symbols](#get-symbols)                             |     false     | 获取所有可交易品种配置信息           |
| [get tickers](#get-tickers)                             |     false     | 获取所有可交易品种最新行情           |
| [get ticker](#get-ticker)                               |     false     | 获取最新行情                         |
| [get depth](#get-depth)                                 |     false     | 获取盘口深度                         |
| [get trades](#get-trades)                               |     false     | 获取最新成交记录                     |
| [get kline](#get-kline)                                 |     false     | 获取最新 K 线记录                    |
| [get bittrex style tickers](#get-bittrex-style-tickers) |     false     | 获取所有可交易品种最新行情 (bittrex) |

## response description

| field      | required | description |
|:-----------|:--------:|:------------|
| success    |   true   | 是否成功    |
| data       |  false   | 结果数据    |
| error_code |  false   | 错误代码    |

## error code

| code   | description |
|:-------|:------------|
| 150001 | 品种不存在  |

# get symbols

> [GET] `{{MARKET_API_URL}}/symbols`

## response example

| field         | description |
|:--------------|:------------|
| symbol        | 品种        |
| price_digits  | 报价小数位  |
| amount_digits | 数量小数位  |

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

| field       | description |
|:------------|:------------|
| last        | 最新价      |
| high        | 24h 最高价  |
| low         | 24h 最低价  |
| volume      | 24h 成交量  |
| change_rate | 24h 涨跌幅  |
| bid         | 买一盘口    |
| ask         | 卖一盘口    |

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

| field  | required | default | description |
|:-------|:--------:|:--------|:------------|
| symbol |   true   | -       | 品种        |

## response example

| field       | description |
|:------------|:------------|
| last        | 最新价      |
| high        | 24h 最高价  |
| low         | 24h 最低价  |
| volume      | 24h 成交量  |
| change_rate | 24h 涨跌幅  |
| bid         | 买一盘口    |
| ask         | 卖一盘口    |

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

| field  | required | default | description |
|:-------|:--------:|:--------|:------------|
| symbol |   true   | -       | 品种        |

## response example

| field | description            |
|:------|:-----------------------|
| bids  | 买方盘口, 按照价格倒序 |
| asks  | 卖方盘口, 按照价格正序 |

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

| field  | required | default | description |
|:-------|:--------:|:--------|:------------|
| symbol |   true   | -       | 品种        |

## response example

| field  | description       |
|:-------|:------------------|
| time   | 成交时间          |
| price  | 成交价            |
| volume | 成交量            |
| side   | 方向 (买:1, 卖:2) |

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

| field  | required | default | description                                      |
|:-------|:--------:|:--------|:-------------------------------------------------|
| symbol |   true   | -       | 品种                                             |
| period |  false   | 5min    | 间隔周期 (1min, 5min, 15min, 30min, 1hour, 1day) |
| limit  |  false   | 1000    | 限制条数 (1~2000)                                |

## response example

| field  | description |
|:-------|:------------|
| time   | 开始时间    |
| open   | 开盘价      |
| high   | 最高价      |
| low    | 最低价      |
| close  | 收盘价      |
| volume | 成交量      |

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

| field      | description |
|:-----------|:------------|
| MarketName | 品种        |
| High       | 24h 最高价  |
| Low        | 24h 最低价  |
| Volume     | 24h 成交量  |
| Last       | 最新价      |
| TimeStamp  | 数据时间戳  |
| Bid        | 买一价      |
| Ask        | 卖一价      |
| PrevDay    | 24h 开盘价  |

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
