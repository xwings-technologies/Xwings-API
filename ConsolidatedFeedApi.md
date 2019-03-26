# Consolidated Feed REST

Base endpoint: https://xxx.com/consolidated

## Feed Data Sources
```shell
curl "https://api.xxxx.com/dataSources"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/dataSources", true);
    xhr.send();
}
```

> Sample response:

```json
[
    {
        "instrumentId": "ETH/BTC",
        "dataSources": [
            "COINBASE_PRO",
            "BITSTAMP",
            "BITFINEX",
            "GEMINI"
        ]
    }
]
```

Get data sources of consolidated feed

### Http request

```METHOD: GET```

```PATH: /api/dataSources```

### Request Parameters
Name                  | Type(value)      | Mandatory   | Description
----------------------| -----------------|-------------|-----------------------------
instrumentId          | String           | O           |

### Success Response Body Fields
Name               | Type(value)         | Mandatory   | Description
-------------------| --------------------|-------------|--------------------------------
instrumentId       | String              | M           | e.g. BTCUSD
dataSources        | Array of dataSource | M           | e.g. [COINBASE_PRO, BITSTAMP, BITFINEX]

## Feed Ticker
```shell
curl "https://api.xxxx.com/ticker?instrumentId=ETH/BTC&dataSource=CONSOLIDATED"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/ticker?instrumentId=ETH/BTC&dataSource=CONSOLIDATED", true);
    xhr.send();
}
```

> Sample response:

```json
{
    "24hLow": "0.0314",
    "24hVolume": "33113.85823278",
    "lastModifiedTime": 1545996511335,
    "instrumentId": "ETH/BTC",
    "24hHigh": "0.03327",
    "24hChange": "-0.00082",
    "dataSource": "CONSOLIDATED",
    "lastPrice": "0.03245"
}
```

### Http request

```METHOD: GET```

```PATH: /api/ticker```

### Request Parameters
Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
instrumentId       | String           | M           | e.g. "ETHBTC"
dataSource         | Enum             | M           | e.g. "CONSOLIDATED"

### Success Response Body Fields
Name             | Type(value)      | Mandatory   | Description
-----------------| -----------------|-------------|-----------------------
instrumentId     | String           | M           | e.g. "ETHBTC"
dataSource       | Enum             | M           |
lastModifiedTime | Long             | M           | 
lastPrice        | DoubleString     | M           | 
24hHigh          | DoubleString     | M           | 
24hLow           | DoubleString     | M           | 
24hVolume        | DoubleString     | M           | 
24hChange        | DoubleString     | M           | 

## Feed All Tickers
```shell
curl "https://api.xxxx.com/allTickers?dataSource=CONSOLIDATED"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/allTickers?dataSource=CONSOLIDATED", true);
    xhr.send();
}
```

> Sample response:

```json
[
	{
	    "24hLow": "0.0314",
	    "24hVolume": "33113.85823278",
	    "lastModifiedTime": 1545996511335,
	    "instrumentId": "ETH/BTC",
	    "24hHigh": "0.03327",
	    "24hChange": "-0.00082",
	    "dataSource": "CONSOLIDATED",
	    "lastPrice": "0.03245"
	}
]
```

### Http request

```METHOD: GET```

```PATH: /api/allTickers```
    
### Request Parameters
Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
dataSource         | Enum             | M           | e.g. "CONSOLIDATED"    

### Success Response Body Array Json Fields
Name             | Type(value)      | Mandatory   | Description
-----------------| -----------------|-------------|-----------------------
instrumentId     | String           | M           | e.g. "ETHBTC"
dataSource       | Enum             | M           |
lastModifiedTime | Long             | M           | 
lastPrice        | DoubleString     | M           | 
24hHigh          | DoubleString     | M           | 
24hLow           | DoubleString     | M           | 
24hVolume        | DoubleString     | M           | 
24hChange        | DoubleString     | M           | 

## Feed Order Book

```shell
curl "https://api.xxxx.com/orderbook?instrumentId=ETH/BTC&bookLevel=1&dataSource=CONSOLIDATED"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/orderbook?instrumentId=ETH/BTC&bookLevel=1&dataSource=CONSOLIDATED", true);
    xhr.send();
}
```

> Sample response:

```json
{
    "dataSource": "CONSOLIDATED",
    "sequence": "5",
    "lastModifiedTime": 1545734172781,
    "bookLevel": 1,
    "instrumentId": "ETH/BTC",
    "asks": [
       {
            "size": "0.0752",
            "price": "59.0",
            "numOfOrders": 0
        },
        {
            "size": "1000.0",
            "price": "50.0",
            "numOfOrders": 0
        },
        {
            "size": "0.01",
            "price": "39.59",
            "numOfOrders": 0
        }
    ],
    "bids": [
        {
            "size": "100.49862944",
            "price": "0.03236",
            "numOfOrders": 0
        },
        {
            "size": "1.232",
            "price": "0.03235",
            "numOfOrders": 0
        },
        {
            "size": "14.22706801",
            "price": "0.03234",
            "numOfOrders": 0
        }
    ]
}
```

Weight: 5

### Http request

```METHOD: GET```

```PATH: /api/orderbook```

### Request Parameters
Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 
level           | Integer          | M           | 1 - top bid and ask; 2 - order book;
dataSource      | Enum             | M           | e.g. "CONSOLIDATED"

### Success Response Body Fields
Name               | Type(value)                                   | Mandatory   | Description
-------------------| ----------------------------------------------|-------------|-----------------------
instrumentId       | String                                        | M           |
dataSource         | Enum                                          | M           | e.g. "CONSOLIDATED"
lastModifiedTime   | Long                                          | M           |
level              | Integer                                       | M           | 1/2
sequence           | Long                                          | M           | 
bids               | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 - This is one sized array;Level 2 - The aggregated size for each price level is returned with numOfOrders count for the price;Level
asks               | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 - This is one sized array;Level 2 - The aggregated size for each price level is returned with numOfOrders count for the price;Level

## Feed Trades

```shell
curl "https://api.xxxx.com/trades?instrumentId=ETH/USD&dataSource=COINBASE_PRO"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/trades?instrumentId=ETH/USD&dataSource=COINBASE_PRO", true);
    xhr.send();
}
```

> Sample response:

```json
[
    {
        "side": "SELL",
        "size": "45.12434133",
        "instrumentId": "ETH/BTC",
        "price": "0.03241",
        "createdTime": 1545998177713,
        "dataSource": "COINBASE_PRO"
    },
    {
        "side": "SELL",
        "size": "0.0179406",
        "instrumentId": "ETH/BTC",
        "price": "0.03241",
        "createdTime": 1545998177713,
        "dataSource": "COINBASE_PRO"
    },
    {
        "side": "SELL",
        "size": "0.0179406",
        "instrumentId": "ETH/BTC",
        "price": "0.03241",
        "createdTime": 1545998177713,
        "dataSource": "COINBASE_PRO"
    }
]
```

Returns most recent trades in an array.

### Http request

```METHOD: GET```

```PATH: /api/trades```

### Request Parameters
Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           |
dataSource      | Enum             | M           | e.g. "CONSOLIDATED"

### Success Response Body Array Json Fields
Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           |
dataSource      | Enum             | M           | e.g. "CONSOLIDATED"
createdTime     | Long             | M           |
tradeId         | String           | M           | 
price           | DoubleString     | M           | 
size            | DoubleString     | M           | 
side            | Enum             | M           |

## Feed Charts

```shell
curl "https://api.xxxx.com/charts?instrumentId=ETH/BTC&dataSource=COINBASE_PRO&startTime=1545998077713&endTime=1545998277713&granularity=60"
```

```javascript
function request() {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            return this.responseText;
        }
    });
    xhr.open("GET", "https://api.xxxx.com/charts?instrumentId=ETH/BTC&dataSource=COINBASE_PRO&startTime=1545998077713&endTime=1545998277713&granularity=60", true);
    xhr.send();
}
```

> Sample response:

```json
[
    {
        "volume": "1.0567541",
        "high": "0.03244",
        "low": "0.03242",
        "openPrice": "0.03242",
        "startTime": 1545998220000,
		"endTime": 1545998330000,
		"lastModifiedTime": 1545998230000,
        "closePrice": "0.03244",
        "dataSource": "COINBASE_PRO"
    },
    {
        "volume": "45.22106593",
        "high": "0.03241",
        "low": "0.03241",
        "openPrice": "0.03241",
        "startTime": 1545998160000,
		"endTime": 1545998330000,
		"lastModifiedTime": 1545998230000,
        "closePrice": "0.03241",
        "dataSource": "COINBASE_PRO"
    },
    {
        "volume": "0.2743248",
        "high": "0.0324",
        "low": "0.0324",
        "openPrice": "0.0324",
        "startTime": 1545998100000,
		"endTime": 1545998330000,
		"lastModifiedTime": 1545998230000,
        "closePrice": "0.0324",
        "dataSource": "COINBASE_PRO"
    }
]
```

It returns an array of data point stats.

### Http request

```METHOD: GET```

```PATH: /api/charts```

### Request Parameters
Name          | Type(value)     | Mandatory   | Description
--------------| ----------------|-------------|-----------------------
instrumentId  | String          | M           |
dataSource    | Enum            | M           | e.g. "CONSOLIDATED"
startTime     | Long            | M           | Seconds since Unix Epoch
endTime       | Long            | O           | Seconds since Unix Epoch
granularity   | Integer         | M           | In seconds; 60/300/900/3600/21600/86400;The combination of startTime, endTime and granularity determines how many data points obtained. The maximum supported number of data points is xxx

### Success Response Body Fields
Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-----------------------
lastModifiedTime | Long            | O           |
dataSource       | Enum            | M           | e.g. "CONSOLIDATED"
startTime        | Long            | M           |
openPrice        | String          | M           | 
closePrice       | String          | M           | 
low              | String          | M           | 
high             | String          | M           | 
volume           | String          | M           | 