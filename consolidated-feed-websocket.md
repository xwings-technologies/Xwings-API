Base endpoint: wss://xxx.com/consolidated

# Consolidated Feed Websocket

## Feed Data Sources Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/cfs");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "dataSource", "instrumentIds": ["ETH/BTC", "XLM/BTC", "XMR/BTC", "XRP/BTC"]}';
        ws.send(data);
    };

    ws.onmessage = function (evt) {
        var received_msg = evt.data;
    };
}
```

> Sample data:

```json
//request
{
  "type": "subscribe",
  "channel": "dataSource",
  "instrumentIds": [
    "ETH/BTC",
    "XLM/BTC",
    "XMR/BTC",
    "XRP/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "dataSource",
  "instrumentId": "ETH/BTC",
  "dataSources": [
    "BITSTAMP",
    "BITFINEX",
    "GEMINI",
    "COINBASE_PRO"
  ],
  "timestamp": 1546506477512
}
//channel
{
  "instrumentId": "ETH/BTC",
  "type": "dataSource",
  "dataSource": [
    "BITSTAMP",
    "BITFINEX",
    "COINBASE_PRO"
  ],
  "timestamp": 1546509059461197
}
```

### Request Fields
Name                  | Type(value)                     | Mandatory   | Description
----------------------| --------------------------------|-------------|-----------------------------
type                  | subscribe/unsubscribe           | M           | Subscribe/Unsubscribe message type
channel               | dataSource                      | M           |
instrumentIds         | Array of instrumentId Strings   | M           |
userMessageId         | Integer                         | O           | Unique message id for this websocket session

### Response Fields
Name                  | Type(value)                     | Mandatory   | Description
----------------------| --------------------------------|-------------|-----------------------------
type                  | subscribe/unsubscribe           | M           | Subscribe/Unsubscribe message type
channel               | dataSource                      | M           |
instrumentId	      | instrumentId String	            | M	          |
dataSources	          | Array of Enum                   | M	          |
userMessageId         | Integer                         | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields:
Name           | Type(value)    | Mandatory   | Description
---------------| ---------------|-------------|----------------
type           | dataSource     | M           |
instrumentId   | String         | M           | e.g. "BTC/USD"
dataSources    | Array of Enum  | M           | 
timestamp      | Long           | M           | data source update time


## Feed Ticker Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/cfs");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "ticker", "instrumentIds": ["ETH/BTC", "XLM/BTC", "XMR/BTC", "XRP/BTC"]}';
        ws.send(data);
    };

    ws.onmessage = function (evt) {
        var received_msg = evt.data;
    };
}
```

> Sample data:

```json
//request
{
  "type": "subscribe",
  "channel": "ticker",
  "instrumentIds": [
    "ETH/BTC",
    "XLM/BTC",
    "XMR/BTC",
    "XRP/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "ticker",
  "instrumentIds": [
    "ETH/BTC",
    "XLM/BTC",
    "XMR/BTC",
    "XRP/BTC"
  ],
  "timestamp": 1546508497272
}
//channel
{
  "type": "ticker",
  "dataSource": "BITSTAMP",
  "timestamp": 1546508495096,
  "instrumentId": "ETH/BTC",
  "lastPrice": "0.03872964",
  "24hHigh": "0.04",
  "24hLow": "0.0382027",
  "24hVolume": "4953.03785251",
  "24hChange": "0.00024413"
}
```

Ticker data with 24h market statistics is pushed every 5 seconds

### Request Fields
Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribe/unsubscribe           | M           | Subscribe/Unsubscribe message type
channel        | ticker                          | M           |
dataSource     | Enum                            | O           | Subscribe/Unsubscribe all data sources by default including "CONSOLIDATED" ticker price
userMessageId  | Integer                         | O           | Unique message id for this websocket session
instrumentIds  | Array of instrumentId Strings   | M           |


### Response Fields
Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribed/unsubscribed         | M           | Subscribed/Unsubscribed message type
channel        | ticker                          | M           |
dataSource     | Enum                            | M           | 
timestamp      | Long                            | M           | Request accepted time
instrumentIds  | Array of instrumentId Strings   | M           |
userMessageId  | Integer                         | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields:
Name           | Type(value)    | Mandatory   | Description
---------------| ---------------|-------------|----------------
type           | ticker         | M           |
dataSource     | Enum           | M           | 
timestamp      | Long           | M           | Ticker created time
instrumentId   | String         | M           | e.g. "BTCUSD"
lastPrice      | DoubleString   | M           |
24hHigh        | DoubleString   | M           |
24hLow         | DoubleString   | M           |
24hVolume      | DoubleString   | M           |
24hChange      | DoubleString   | M           |


## Feed Order Book Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/cfs");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "orderBook", "depth": 50, "instrumentIds": ["ETH/BTC"]}';
        ws.send(data);
    };

    ws.onmessage = function (evt) {
        var received_msg = evt.data;
    };
}
```

> Sample data:

```json
//request
{
  "type": "subscribe",
  "channel": "orderBook",
  "depth": 50,
  "instrumentIds": [
    "ETH/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "orderBook",
  "timestamp": 1546511253719,
  "dataSource": "COINBASE_PRO",
  "depth": 50,
  "instrumentId": "ETH/BTC",
  "bids": [
    [
      "0.03898",
      "3.44469471"
    ],
    [
      "0.03897",
      "0.1515"
    ],
    [
      "0.03896",
      "11.82334269"
    ]
  ]
}
//channel
{
  "type": "orderBook",
  "instrumentId": "ETH/BTC",
  "timestamp": 1546511328,
  "dataSource": "GEMINI",
  "bids": [
    [
      "0.03801",
      "50"
    ]
  ],
  "asks": []
}
```

### Request Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           |
dataSource     | Enum                           | O           | Subscribe/Unsubscribe all exchange data sources by default
depth          | Integer                        | O           | Default to 25
instrumentIds  | Array of instrumentId Strings  | M           |
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields
Name           | Type(value)                         | Mandatory   | Description
---------------| ------------------------------------|-------------|----------------
type           | subscribed/unsubscribed             | M           | Subscribe/Unsubscribe message type
channel        | orderBook                           | M           |
dataSource     | Enum                                | M           | 
timestamp      | Long                                | M           | When subscription request was accepted
depth          | Integer                             | M           |
instrumentId   | instrumentId String                 | M           |
bids           | Array of [price, size]              | M           | Snapshot of bids with the aggregated size for each price level
asks           | Array of [price, size]              | M           | Snapshot of asks with the aggregated size for each price level
userMessageId  | Integer                             | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name           | Type(value)                        |  Mandatory  | Description
---------------| -----------------------------------| ------------|--------------------------------------
type           | orderBook                          | M           |
timestamp      | Long                               | M           | order book update time
instrumentId   | String                             | M           |
dataSource     | Enum                               | M           | 
bids           | Array of [price, size]             | M           | Update of bids with the aggregated size for the updated price level
asks           | Array of [price, size]             | M           | Update of asks with the aggregated size for the updated price level


## Feed Trade Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/cfs");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "trade", "instrumentIds": ["ETH/BTC"]}';
        ws.send(data);
    };

    ws.onmessage = function (evt) {
        var received_msg = evt.data;
    };
}
```

> Sample data:

```json
//request
{
  "type": "subscribe",
  "channel": "trade",
  "instrumentIds": [
    "ETH/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "trade",
  "instrumentIds": [
    "ETH/BTC"
  ],
  "timestamp": 1546514515204
}
//channel
{
  "type": "trade",
  "instrumentId": "ETH/BTC",
  "timestamp": 1546514515175,
  "dataSource": "COINBASE_PRO",
  "price": "0.03853",
  "size": "0.01",
  "side": "SELL"
}
```

trade data is pushed whenever a trade occurs in the system.

### Request Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           |
dataSource     | Enum                           | O           | Subscribe/Unsubscribe all exchange data sources by default
instrumentIds  | Array of instrumentId Strings  | M           |
userMessageId  | Integer                        | O           | Unique message id for this websocket session

### Response Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribed/unsubscribe         | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           |
dataSource     | Enum                           | M           | 
timestamp      | Long                           | M           | When the subscription request was accepted
instrumentIds  | Array of instrumentId Strings  | M           |
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields
Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-------------
type             | trade           | M           |
timestamp        | Long            | M           | Trade time
instrumentId     | String          | M           |
dataSource       | Enum            | M           | 
tradeId          | String          | M           |
price            | DoubleString    | M           |
size             | DoubleString    | M           |
side             | Enum            | M           | Buy/Sell
