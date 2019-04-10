# FeiXiaoHao PublicAPI

The FeiXiaoHao API is a suite of high-performance RESTful JSON endpoints that are specifically designed to meet the mission-critical demands of application developers, data scientists, and enterprise business platforms.

## Endpoint Overview

The FeiXiaoHao API only have 1 top-level category right now.

Endpoint Category |  Description  
:- | :-- 
[https://fxhapi.feixiaohao.com/public/v1/ticker/*](https://fxhapi.feixiaohao.com/public/v1/ticker) | Endpoints that return data around cryptocurrencies such as ordered cryptocurrency lists or price and volume data. 

## Quick Start

### Tickers

> Update per minute

* **Method:**

  `GET`

* **URL Params**

   **Optional:**

   `start=[integer](return results from rank "start" and above)`
   `limit=[integer](return a maximum of "limit" results, default is 100, use 0 to return all results)`
   `convert=[alphanumeric](return price, 24h volume, and market cap in terms of another currency. Valid values are: "AUD", "BRL", "CAD", "CHF", "CLP", "CNY", "CZK", "DKK", "EUR", "GBP", "HKD", "HUF", "IDR", "ILS", "INR", "JPY", "KRW", "MXN", "MYR", "NOK", "NZD", "PHP", "PKR", "PLN", "RUB", "SEK", "SGD", "THB", "TRY", "TWD", "ZAR")`

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 

    ```json
    [
        {
            "id": "bitcoin",
            "name": "Bitcoin",
            "symbol": "BTC",
            "rank": 1,
            "logo": "https://s1.bqiapp.com/coin/20181030_72_webp/bitcoin_200_200.webp",
            "logo_png": "https://s1.bqiapp.com/coin/20181030_72_png/bitcoin_200_200.png",
            "price_usd": 5225,
            "price_btc": 1,
            "volume_24h_usd": 5150321567,
            "market_cap_usd": 92163602317,
            "available_supply": 17637575,
            "total_supply": 17637575,
            "max_supply": 21000000,
            "percent_change_1h": 0.21,
            "percent_change_24h": 0.64,
            "percent_change_7d": 6,
            "last_updated": 1554886833
        },
        {
            "id": "ethereum",
            "name": "Ethereum",
            "symbol": "ETH",
            "rank": 2,
            "logo": "https://s1.bqiapp.com/coin/20181030_72_webp/ethereum_200_200.webp",
            "logo_png": "https://s1.bqiapp.com/coin/20181030_72_png/ethereum_200_200.png",
            "price_usd": 179.65,
            "price_btc": 0.0344,
            "volume_24h_usd": 2766496907,
            "market_cap_usd": 18971178569,
            "available_supply": 105598041,
            "total_supply": 105598041,
            "max_supply": 105598041,
            "percent_change_1h": 0.35,
            "percent_change_24h": 2.18,
            "percent_change_7d": 8.42,
            "last_updated": 1554886833
        }
    ]
    ```

* **Error Response:**

  * **Code:** 401/403 or 429<br />
    **Content:** `{"message":"API rate limit exceeded"}`

* **Sample Call:**

  * **CURL:** <br />
  ```bash
  curl -H "Accept: application/json" -G "https://fxhapi.feixiaohao.com/public/v1/ticker?limit=5"
  ```
  * **C#:**<br />
  ```csharp
  using System;
  using System.Net;
  using System.Web;
  
  class CSharpExample
  {
      public static void Main(string[] args)
      {
          try
          {
              Console.WriteLine(makeAPICall());
          }
          catch (WebException e)
          {
              Console.WriteLine(e.Message);
          }
      }
  
      static string makeAPICall()
      {
          var URL = new UriBuilder("https://fxhapi.feixiaohao.com/public/v1/ticker");
  
          var queryString = System.Web.HttpUtility.ParseQueryString(string.Empty);
          queryString["start"] = "5";
          queryString["limit"] = "5";
          queryString["convert"] = "USD";
  
          URL.Query = queryString.ToString();
  
          var client = new System.Net.WebClient();
          client.Headers.Add("Accepts", "application/json");
          return client.DownloadString(URL.ToString());
      }
  
  }
  
  ```
* **Java:**<br />

  ```java
  import java.io.IOException;
  import java.net.URISyntaxException;
  import java.util.ArrayList;
  import java.util.List;
  
  public class JavaExample {
  
      public static void main(String[] args) {
          String uri = "https://fxhapi.feixiaohao.com/public/v1/ticker";
          List<NameValuePair> paratmers = new ArrayList<NameValuePair>();
          paratmers.add(new BasicNameValuePair("start","5"));
          paratmers.add(new BasicNameValuePair("limit","5"));
          paratmers.add(new BasicNameValuePair("convert","USD"));
  
          try {
              String result = makeAPICall(uri, paratmers);
              System.out.println(result);
          } catch (IOException e) {
              System.out.println("Error: cannont access content - " + e.toString());
          } catch (URISyntaxException e) {
              System.out.println("Error: Invalid URL " + e.toString());
          }
      }
  
      public static String makeAPICall(String uri, List<NameValuePair> parameters)
              throws URISyntaxException, IOException {
          String response_content = "";
  
          URIBuilder query = new URIBuilder(uri);
          query.addParameters(parameters);
  
          CloseableHttpClient client = HttpClients.createDefault();
          HttpGet request = new HttpGet(query.build());
  
          request.setHeader(HttpHeaders.ACCEPT, "application/json");
  
          CloseableHttpResponse response = client.execute(request);
  
          try {
              System.out.println(response.getStatusLine());
              HttpEntity entity = response.getEntity();
              response_content = EntityUtils.toString(entity);
              EntityUtils.consume(entity);
          } finally {
              response.close();
          }
  
          return response_content;
      }
  
  }
  
  ```
  * **Golang:**<br />
  ```go
  package main
  
  import (
      "fmt"
      "io/ioutil"
      "log"
      "net/http"
      "net/url"
      "os"
  )
  
  
  func main() {
      client := &http.Client{}
      req, err := http.NewRequest("GET","https://fxhapi.feixiaohao.com/public/v1/ticker", nil)
      if err != nil {
          log.Print(err)
          os.Exit(1)
      }
  
      q := url.Values{}
      q.Add("start", "5")
      q.Add("limit", "5")
      q.Add("convert", "USD")
  
      req.Header.Set("Accepts", "application/json")
      req.URL.RawQuery = q.Encode()
  
  
      resp, err := client.Do(req);
      if err != nil {
          fmt.Println("Error sending request to server")
          os.Exit(1)
      }
      fmt.Println(resp.Status);
      respBody, _ := ioutil.ReadAll(resp.Body)
      fmt.Println(string(respBody));
  
  }
  ```

