# REST Public

## Instruments
```shell
curl "https://api.xxxx.com/api/instruments"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/instruments", true);
    xhr.send();
}
```

> Sample response:

```json
[
    {
        "instrumentType": "SPOT",
        "minOrderPrice": "0.00001",
        "minOrderSize": "0.001",
        "instrumentId": "ETH/BTC",
        "lotSize": "0.001",
        "maxOrderSize": "100000",
        "asset": "ETH",
        "quoteAsset": "BTC",
        "tickSize": "0.00001",
        "maxOrderPrice": "100000"
    }
]
```

### Http request
```GET /api/instruments```

### Request Parameters
Name                  | Type(value)      | Mandatory   | Description
----------------------| -----------------|-------------|-----------------------------
instrumentId          | String           | O           | 
instrumentType        | Enum             | O           |
asset                 | String           | O           |
quoteAsset            | String           | O           |
underlying            | String           | O           | 

### Success Response Body Fields
Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|--------------------------------
instrumentId       | String           | M           | e.g. BTCUSD
asset              | String           | M           | e.g. BTC
quoteAsset         | String           | M           | e.g. USD
instrumentType     | Enum             | M           | 
tickSize           | DoubleString     | M           | price increment
lotSize            | DoubleString     | M           | size increment
minOrderPrice      | DoubleString     | M           | 
maxOrderPrice      | DoubleString     | M           | 
minOrderSize       | DoubleString     | M           | 
maxOrderSize       | DoubleString     | M           | 
expiry             | Long             | (M)         | Mandatory for FUTURES instrument
underlying         | String           | (M)         | Mandatory for FUTURES instrument
contractMultiplier | Integer          | (M)         | Mandatory for FUTURES instrument

## Ticker
```shell
curl "https://api.xxxx.com/api/ticker?instrumentId=ETH/BTC"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/ticker?instrumentId=ETH/BTC", true);
    xhr.send();
}
```

> Sample response:

```json
{
    "24hLow": "0.03146",
    "24hVolume": "5514.332",
    "lastModifiedTime": 1545990354807,
    "bestAsk": "0.03249",
    "instrumentId": "ETH/BTC",
    "24hHigh": "0.0334",
    "24hChange": "-0.00083",
    "lastPrice": "0.03248",
    "bestBid": "0.03248"
}
```

### Http request
```GET /api/ticker```

### Request Parameters
Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
instrumentId       | String           | M           | e.g. "ETHBTC"

### Success Response Body Fields
Name             | Type(value)      | Mandatory   | Description
-----------------| -----------------|-------------|-----------------------
instrumentId     | String           | M           | e.g. "ETHBTC"
lastModifiedTime | Long             | M           | 
lastPrice        | DoubleString     | M           | 
bestBid          | DoubleString     | M           | 
bestAsk          | DoubleString     | M           | 
24hHigh          | DoubleString     | M           | 
24hLow           | DoubleString     | M           | 
24hVolume        | DoubleString     | M           | 
24hChange        | DoubleString     | M           | 

## All Tickers
```shell
curl "https://api.xxxx.com/api/allTickers"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/allTickers", true);
    xhr.send();
}
```

> Sample response:

```json
[
    {
        "24hLow": "0.03146",
        "24hVolume": "5514.332",
        "lastModifiedTime": 1545990442807,
        "bestAsk": "0.03249",
        "instrumentId": "ETH/BTC",
        "24hHigh": "0.0334",
        "24hChange": "-0.00083",
        "lastPrice": "0.03248",
        "bestBid": "0.03248"
    }
]
```

### Http request
```GET /api/allTickers```

### Success Response Body Array Json Fields
Name             | Type(value)      | Mandatory   | Description
-----------------| -----------------|-------------|-----------------------
instrumentId     | String           | M           | e.g. "ETHBTC"
lastModifiedTime | Long             | M           | 
lastPrice        | DoubleString     | M           | 
bestBid          | DoubleString     | M           | 
bestAsk          | DoubleString     | M           | 
24hHigh          | DoubleString     | M           | 
24hLow           | DoubleString     | M           | 
24hVolume        | DoubleString     | M           | 
24hChange        | DoubleString     | M           | 

## Order Book
```shell
curl "https://api.xxxx.com/api/orderbook?instrumentId=ETH/BTC&level=1"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/orderbook?instrumentId=ETH/BTC&level=1", true);
    xhr.send();
}
```

> Sample response:

```json
{
    "sequence": "0",
    "lastModifiedTime": 1545990730713,
    "level": 1,
    "instrumentId": "ETH/BTC",
    "asks": [
        {
            "size": "6.348",
            "price": "0.03227",
            "numOfOrders": 1
        }
    ],
    "bids": [
        {
            "size": "1.268",
            "price": "0.03226",
            "numOfOrders": 1
        }
    ]
}
```

    Weight: 5

### Http request
```GET /api/orderbook```
    
### Request Parameters
Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 
level           | Integer          | M           | 1 - top bid and ask; 2 - order book; 3 - full order level book

### Success Response Body Fields
Name               | Type(value)                                   | Mandatory   | Description
-------------------| ----------------------------------------------|-------------|-----------------------
instrumentId       | String                                        | M           |
lastModifiedTime   | Long                                          | M           | 
bookLevel       | Integer                                       | M           | 1/2/3
sequence        | Long                                          | M           | 
bids            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 - This is one sized array;Level 2 - The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 - The order level information is returned
asks            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 - This is one sized array;Level 2 - The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 - The order level information is returned

## Trades
```shell
curl "https://api.xxxx.com/api/trades?instrumentId=ETH/BTC"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/trades?instrumentId=ETH/BTC", true);
    xhr.send();
}
```

> Sample response:

```json
[
    {
        "side": "BUY",
        "size": "0.01",
        "instrumentId": "ETH/BTC",
        "price": "0.0323",
        "createdTime": 1545991656158,
        "tradeId": "448679"
    },
    {
        "side": "BUY",
        "size": "0.01",
        "instrumentId": "ETH/BTC",
        "price": "0.0323",
        "createdTime": 1545991656146,
        "tradeId": "448678"
    },
    {
        "side": "BUY",
        "size": "0.01",
        "instrumentId": "ETH/BTC",
        "price": "0.0323",
        "createdTime": 1545991656133,
        "tradeId": "448677"
    },
    {
        "side": "BUY",
        "size": "0.01",
        "instrumentId": "ETH/BTC",
        "price": "0.0323",
        "createdTime": 1545991656121,
        "tradeId": "448676"
    }
]
```

Returns most recent trades in an array.

### Http request
```GET /api/trades```
    
### Request Parameters
Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 

### Success Response Body Array Json Fields
Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           |
createdTime     | Long             | M           | 
tradeId   | String           | M           | 
price     | DoubleString     | M           | 
size      | DoubleString     | M           | 
side      | Enum             | M           |

## Charts
```shell
curl "https://api.xxxx.com/api/charts?instrumentId=ETH/BTC&startTime=1545990160243&granularity=60"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/charts?instrumentId=ETH/BTC&startTime=1545990160243&granularity=60", true);
    xhr.send();
}
```

> Sample response:

```json
[
	{
        "volume": "1.030",
        "high": "0.03234",
        "low": "0.03228",
        "openPrice": "0.03234",
        "startTime": 1545993300000,
        "closePrice": "0.03228"
    },
    {
        "volume": "14.723",
        "high": "0.03235",
        "low": "0.03225",
        "openPrice": "0.03225",
        "startTime": 1545993000000,
        "closePrice": "0.03234"
    },
    {
        "volume": "3.630",
        "high": "0.03234",
        "low": "0.03222",
        "openPrice": "0.03234",
        "startTime": 1545992700000,
        "closePrice": "0.03223"
    }
]
```

It returns an array of data point stats.

### Http request
```GET /api/charts```

### Request Parameters
Name          | Type(value)     | Mandatory   | Description
--------------| ----------------|-------------|-----------------------
instrumentId  | String          | M           | 
startTime     | Long            | M           | Milliseconds since Unix Epoch
endTime       | Long            | O           | Milliseconds since Unix Epoch
granularity   | Integer         | M           | In seconds; 60/300/900/3600/21600/86400;The combination of startTime, endTime and granularity determines how many data points obtained. The maximum supported number of data points is xxx

### Success Response Body Fields
Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-----------------------
lastModifiedTime | Long            | O           |
startTime        | Long            | M           | 
endTime          | Long            | M           | 
openPrice        | String          | M           | 
closePrice       | String          | M           | 
low              | String          | M           | 
high             | String          | M           | 
volume           | String          | M           | 

## Time
```shell
curl "https://api.xxxx.com/api/time"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/api/time", true);
    xhr.send();
}
```

> Sample response:

```json
{
    "time": 1545994698933
}
```

It returns the server time in milliseconds since Unix Epoch

### Http request
```GET /api/time```
