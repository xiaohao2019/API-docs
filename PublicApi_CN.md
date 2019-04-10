# 非小号公共API

Feixiaohao API是一套高性能的RESTful接口，专门设计用于满足应用程序开发人员、数据科学家和企业业务平台的需求。

## 终结点

Feixiaohao API目前只有1个顶级目录。

目录 |  描述  
:- | :-- 
[https://fxhapi.feixiaohao.com/public/v1/ticker/*](https://fxhapi.feixiaohao.com/public/v1/ticker) | 返回加密货币数据，如有序加密货币列表或价格和数量数据。

## 快速开始

### Ticker(行情)

> 更新频率:1分钟更新一次

* **访问方式:**

  `GET`

* **URL 参数**

   **可选:**

   `start=[integer](指定结果集的开始排名)`<br />
   
   `limit=[integer](指定结果集的最大数量)`<br />
   
   `convert=[string](将返回的 price, 24h volume, 和 market cap 字段转换到指定货币单位并补充到结果对象. 可用的货币单位有: "AUD", "BRL", "CAD", "CHF", "CLP", "CNY", "CZK", "DKK", "EUR", "GBP", "HKD", "HUF", "IDR", "ILS", "INR", "JPY", "KRW", "MXN", "MYR", "NOK", "NZD", "PHP", "PKR", "PLN", "RUB", "SEK", "SGD", "THB", "TRY", "TWD", "ZAR")`

* **访问成功:**

  * **返回码:** 200 <br />
    **返回内容:** 

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

* **访问失败:**

  * **返回码:** 401/403 或者 429<br />
    **内容:** `{"message":"API rate limit exceeded"}`

* **示例请求:**

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
