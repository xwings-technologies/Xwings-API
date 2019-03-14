# Websocket Public

## Ticker Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/ws");

    ws.onopen = function () {
        var data = '{"type": "subscribe","channel": "ticker","instrumentIds": ["ETH/BTC","XRP/BTC"]}';
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
    "XRP/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "ticker",
  "instrumentIds": [
    "ETH/BTC",
    "XRP/BTC"
  ],
  "timestamp": 1546414351695
}
//channel
{
  "type": "ticker",
  "instrumentId": "ETH/BTC",
  "timestamp": 1546414339719,
  "lastPrice": "0.03811",
  "bestBid": "0.03814",
  "bestAsk": "0.03815",
  "24hHigh": "0.03811",
  "24hLow": "0.03662",
  "24hVolume": "753.235",
  "24hChange": "0.00145"
}
```

Ticker data with 24h market statistics is pushed every second.

### Request Fields
Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribe/unsubscribe           | M           | Subscribe/Unsubscribe message type
channel        | ticker                          | M           | 
userMessageId  | Integer                         | O           | Unique message id for this websocket session
instrumentIds  | Array of instrumentId Strings   | M           | 

### Response Fields
Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribed/unsubscribed         | M           | Subscribed/Unsubscribed message type
channel        | ticker                          | M           | 
timestamp      | Long                            | M           | Request accepted time
instrumentIds  | Array of instrumentId Strings   | M           | 
userMessageId  | Integer                         | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields:
Name           | Type(value)    | Mandatory   | Description
---------------| ---------------|-------------|----------------
type           | ticker         | M           | 
timestamp      | Long           | M           | Ticker created time
instrumentId   | String         | M           | e.g. "BTCUSD"
lastPrice      | DoubleString   | M           | 
bestBid        | DoubleString   | M           | 
bestAsk        | DoubleString   | M           | 
24hHigh        | DoubleString   | M           | 
24hLow         | DoubleString   | M           | 
24hVolume      | DoubleString   | M           | 
24hChange      | DoubleString   | M           | 

## Order Book Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/ws");

    ws.onopen = function () {
        var data = '{"type": "subscribe","channel": "orderBook","depth": 25,"instrumentIds": "ETH/BTC"]}';
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
  "depth": 25,
  "instrumentIds": [
    "ETH/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "orderBook",
  "timestamp": 1546414351648,
  "depth": 25,
  "instrumentId": "ETH/BTC",
  "bids": [
    [
      "0.03816",
      "2.165",
      1
    ],
    [
      "0.03814",
      "7.303",
      1
    ],
    [
      "0.03812",
      "0.897",
      1
    ]
  ],
  "asks": [
    [
      "0.03817",
      "7.689",
      1
    ],
    [
      "0.03818",
      "7.344",
      1
    ],
    [
      "0.03819",
      "2.223",
      1
    ]
  ]
}
//channel
{
  "type": "orderBook",
  "instrumentId": "ETH/BTC",
  "timestamp": 1546414338870,
  "bids": [
    [
      "0.03812",
      "0.997",
      2
    ]
  ],
  "asks": [
    [
      "0.03817",
      "0",
      0
    ]
  ]
}
```

### Request Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           | 
depth          | Integer                        | O           | Default to 25
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session

### Response Fields
Name           | Type(value)                         | Mandatory   | Description
---------------| ------------------------------------|-------------|----------------
type           | subscribed/unsubscribed             | M           | Subscribe/Unsubscribe message type
channel        | orderBook                           | M           | 
timestamp      | Long                                | M           | When subscription request was accepted
depth          | Integer                             | M           | 
instrumentId   | instrumentId String                 | M           | 
bids           | Array of [price, size, numOfOrders] | M           | Snapshot of bids with the aggregated size for each price level
asks           | Array of [price, size, numOfOrders] | M           | Snapshot of asks with the aggregated size for each price level
userMessageId  | Integer                             | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields
Name           | Type(value)                        |  Mandatory  | Description
---------------| -----------------------------------| ------------|--------------------------------------
type           | orderBook                          | M           |
timestamp      | Long                               | M           | order book update time
instrumentId   | String                             | M           |
bids           | Array of [price, size, numOfOrders]| M           | Update of bids with the aggregated size for the updated price level
asks           | Array of [price, size, numOfOrders]| M           | Update of asks with the aggregated size for the updated price level

## Full Order Book Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/ws");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "fullOrderBook", "instrumentIds": ["ETH/BTC"]}';
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
  "channel": "fullOrderBook",
  "instrumentIds": [
    "ETH/BTC"
  ]
}
//response
{
  "type": "subscribed",
  "channel": "fullOrderBook",
  "timestamp": 1546414351648,
  "instrumentId": "ETH/BTC",
  "bids": [
    [
      "0.03816",
      "2.165",
      "6b742a26-5dfb-423f-84de-48182b85c343	"
    ],
	[
      "0.03814",
      "1.586",
      "12a4eb0f-5800-4d74-9305-ef069156e305"
    ],
    [
      "0.03814",
      "2.457",
      "ee63cf9c-cc0b-420c-a30a-c064d0c0c5e3"
    ],
	[
      "0.03814",
      "3.26",
      "c25bc5ef-3ae1-4d8f-a1d1-6da789ef7e5f"
    ],
    [
      "0.03812",
      "0.897",
      "120bd10e-1046-4735-b070-45c35d8e1333"
    ]
  ],
  "asks": [
    [
      "0.03817",
      "2.059",
      "2d4ba2f0-e2fb-4a23-ab6a-0b9e70e20b03"
    ],
	[
      "0.03817",
      "5.63",
      "6ab23323-7270-4c7b-a20e-9abf352365bb"
    ],
	[
      "0.03818",
      "3.03",
      "8ead69cb-b3ef-4cf7-9214-74e5a18225ed"
    ],
    [
      "0.03818",
      "4.314",
      "c877d8fa-b74d-45be-a82e-b731c1e1baaf"
    ],
    [
      "0.03819",
      "2.223",
      "a211216c-98df-4c1a-9fdf-1ffff7e69f99"
    ]
  ]
}
//channel
{
  "type": "fullOrderBook",
  "instrumentId": "ETH/BTC",
  "timestamp": 1546414338870,
  "bids": [
    [
      "0.03812",
      "0.897",
      "120bd10e-1046-4735-b070-45c35d8e1333"
    ]
  ],
  "asks": [
    [
      "0.03817",
      "0",
      "2d4ba2f0-e2fb-4a23-ab6a-0b9e70e20b03"
    ]
  ]
}
```

### Request Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | fullOrderBook                  | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session

### Response Fields
Name           | Type(value)                         | Mandatory   | Description
---------------| ------------------------------------|-------------|----------------
type           | subscribed/unsubscribed             | M           | Subscribe/Unsubscribe message type
channel        | fullOrderBook                       | M           | 
timestamp      | Long                                | M           | When the subscription was accepted
instrumentId   | instrumentId String                 | M           | 
bids           | Array of [price, size, orderId]     | M           | Snapshot of buy orders
asks           | Array of [price, size, orderId]     | M           | Snapshot of sell orders
userMessageId  | Integer                             | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields
Name           | Type(value)                         | Mandatory   | Description
---------------| ------------------------------------|-------------|-------------
type           | fullOrderBook                       | M           |
timestamp      | Long                                | M           | order book update time
instrumentId   | String                              | M           | 
bids           | Array of [price, size, orderId]     | M           | Update of buy orders
asks           | Array of [price, size, orderId]     | M           | Update of sell orders

## Trade Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/ws");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "trade", "instrumentIds": ["ETH/BTC"]}';
        ws.send(data);
    };

    ws.onmessage = function (evt) {
        var received_msg = evt.data;
    };
}
```

> Sample Data

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
  "timestamp": 1546414344440
}
//channel
{
  "type": "trade",
  "instrumentId": "ETH/BTC",
  "timestamp": 1546414338729,
  "tradeId": "480252",
  "price": "0.03811",
  "size": "0.022",
  "side": "SELL"
}
```

trade data is pushed whenever a trade occurs in the system.  

### Request Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           | 
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | O           | Unique message id for this websocket session

### Response Fields
Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribed/unsubscribe         | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           | 
timestamp      | Long                           | M           | When the subscription request was accepted
instrumentIds  | Array of instrumentId Strings  | M           | 
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields
Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-------------
type             | trade           | M           | 
timestamp        | Long            | M           | Trade time
instrumentId     | String          | M           | 
tradeId   | String          | M           | 
price     | DoubleString    | M           | 
size      | DoubleString    | M           | 
side      | Enum            | M           | Buy/Sell

## Charts Channel

```javascript
function WebSocketCall() {
    var ws = new WebSocket("wss://ws-api.xxxx.com/ws");

    ws.onopen = function () {
        var data = '{"type": "subscribe", "channel": "charts", "instrumentIds": ["ETH/BTC"], "granularity": 900}';
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
  "channel": "charts",
  "instrumentIds": [
    "ETH/BTC"
  ],
  "granularity": 900
}
//response
{
  "type": "subscribed",
  "channel": "charts",
  "timestamp": 1546414351696,
  "instrumentId": "ETH/BTC",
  "granularity": 900,
  "records": [
    [
      1546414200000,
      "0.03785",
      "0.03811",
      "0.03785",
      "0.03811",
      "70.527",
      1546414338753
    ],
    [
      1546413300000,
      "0.03784",
      "0.03787",
      "0.03764",
      "0.03787",
      "33.024"
    ],
    [
      1546412400000,
      "0.03699",
      "0.03781",
      "0.03699",
      "0.03781",
      "180.927"
    ]
  ]
}
//channel
{
  "type": "charts",
  "timestamp": 1546415100061,
  "instrumentId": "ETH/BTC",
  "granularity": 900,
  "update": [
    1546414200000,
    "0.03785",
    "0.03788",
    "0.03785",
    "0.03816",
    "79.250"
  ]
}
```

### Request Fields
Name            | Type(value)                    | Mandatory   | Description
----------------| -------------------------------|-------------|-------------
type            | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel         | charts                         | M           | 
instrumentIds   | Array of instrumentId Strings  | M           | 
granularity     | Integer                        | M           | 
userMessageId   | Integer                        | O           | Unique message id for this websocket session

### Response Fields
Name            | Type(value)                                                       | Mandatory   | Description
----------------| ------------------------------------------------------------------|-------------|-------------
type            | subscribed/unsubscribed                                           | M           | Subscribe/Unsubscribe message type
channel         | charts                                                            | M           | 
timestamp       | Long                                                              | M           | When the subscription request was accepted
instrumentId    | String                                                            | M           | 
granularity     | Integer                                                           | M           |
userMessageId   | Integer                                                           | (M)         | Mandatory if userMessageId is provided in the user request
records         | Array of [startTime,open,close,low,high,volume]                   | M           | 

The first charts message will contain the array of historical data
entries with the maximum size of 300.

### Channel Fields
Name          | Type(value)                                              | Mandatory   | Description
--------------| ---------------------------------------------------------|-------------|-------------
type          | charts                                                   | M           | 
timestamp     | Long                                                     | M           | Chart update time
instrumentId  | String                                                   | M           | 
granularity   | Integer                                                  | M           |
update        | [startTime,open,close,low,high,volume]                   | M           |