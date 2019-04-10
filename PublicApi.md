# 域名：http://fxhapi.feixiaohao.com 
Ticker
Endpoint: /ticker/
Method: GET
更新频率:1分钟更新一次
Optional parameters:
(int) start - return results from rank [start] and above
(int) limit - return a maximum of [limit] results (default is 100, use 0 to return all results)
(string) convert - return price, 24h volume, and market cap in terms of another currency. Valid values are: 
"AUD", "BRL", "CAD", "CHF", "CLP", "CNY", "CZK", "DKK", "EUR", "GBP", "HKD", "HUF", "IDR", "ILS", "INR", "JPY", "KRW", "MXN", "MYR", "NOK", "NZD", "PHP", "PKR", "PLN", "RUB", "SEK", "SGD", "THB", "TRY", "TWD", "ZAR"
Example: http://fxhapi.feixiaohao.com/public/v1/ticker/
Example: http://fxhapi.feixiaohao.com/public/v1/ticker/?limit=10
Example: http://fxhapi.feixiaohao.com/public/v1/ticker/?start=100&limit=10
Example:http://fxhapi.feixiaohao.com/public/v1/ticker/?convert=EUR&limit=10

Sample Response:
[{
	"Id": "bitcoin",
	"name": "Bitcoin",
	"symbol": "BTC",
	"rank": 1,
	"price_usd": 6830.0,
	"price_btc": 1.00,
	"volume_24h_usd": 5354794610.0,
	"market_cap_usd": 115931161873.896,
	"available_supply": 16972775.0,
	"total_supply": 16972775.0,
	"max_supply": 21000000.0,
	"percent_change_1h": -1.14,
	"percent_change_24h": -0.39,
	"percent_change_7d": -0.33,
	"last_updated": 1523519698
}, {
	"Id": "ethereum",
	"name": "Ethereum",
	"symbol": "ETH",
	"rank": 2,
	"price_usd": 423.0,
	"price_btc": 0.0617,
	"volume_24h_usd": 1748244190.0,
	"market_cap_usd": 41746294075.1026,
	"available_supply": 98768678.0,
	"total_supply": 98768678.0,
	"max_supply": 98768678.0,
	"percent_change_1h": -0.71,
	"percent_change_24h": 1.44,
	"percent_change_7d": 10.47,
	"last_updated": 1523519698
}]


Ticker (Specific Currency)
Endpoint: /ticker/?code={id}
Method: GET
Optional parameters:
(string) convert - return price, 24h volume, and market cap in terms of another currency. Valid values are: 
"AUD", "BRL", "CAD", "CHF", "CLP", "CNY", "CZK", "DKK", "EUR", "GBP", "HKD", "HUF", "IDR", "ILS", "INR", "JPY", "KRW", "MXN", "MYR", "NOK", "NZD", "PHP", "PKR", "PLN", "RUB", "SEK", "SGD", "THB", "TRY", "TWD", "ZAR"
Example: http://fxhapi.feixiaohao.com/public/v1/ticker?code=bitcoin
Example: http://fxhapi.feixiaohao.com/public/v1/ticker?code=bitcoin&convert=EUR
Sample Response:
[
    {
        "id": "bitcoin",
        "name": "Bitcoin",
        "symbol": "BTC",
        "rank": "1",
        "price_usd": "573.137",
        "price_btc": "1.0",      
       "volume_24h_usd": 1748244190.0,
        "market_cap_usd": "9080883500.0",
        "available_supply": "15844176.0",
        "total_supply": "15844176.0",
        "max_supply": "21000000.0",
        "percent_change_1h": "0.04",
        "percent_change_24h": "-0.3",
        "percent_change_7d": "-0.57",
        "last_updated": "1472762067"
    }
]               

           
