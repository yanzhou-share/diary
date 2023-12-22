# twitter 接口调研

## twitter api v2

### Search Tweets
Searching for Tweets is an important feature used to surface Twitter conversations about a specific topic or event. While this functionality is present in Twitter, these endpoints provide greater flexibility and power when filtering for and ingesting Tweets so you can find relevant data for your research more easily; build out near-real-time ‘listening’ applications; or generally explore, analyze, and/or act upon Tweets related to a topic of interest. 
These endpoints will always return the most recent edit, along with any edit history. Any Tweet collected after its 30-minute edit window will represent its final version. To learn more about Edit Tweet metadata, check out the Edit Tweets fundamentals page.


#### Recent search
The recent search endpoint allows you to programmatically access filtered public Tweets posted over the last week, and is available to all developers who have a developer account and are using keys and tokens from an App within a Project.


#### Full-archive search
The v2 full-archive search endpoint is only available to Projects with Academic Research access or Enteprise access. The endpoint allows you to programmatically access public Tweets from the complete archive dating back to the first Tweet in March 2006, based on your search query.


### Filtered streams


# twitter 
* Free (API list)  
    POST /2/tweets
    DELETE /2/tweets/:id
    GET /2/users/me
* Pro price $5000/month
* Basic price $100/month
    
要获取特定用户的推文并通过邮件进行通知，可以使用 Twitter API 获取用户的最新推文，并使用电子邮件服务发送通知。以下是使用 Twitter API 和 Node.js 实现这个功能的代码示例：

1. 安装所需的依赖项：
   - 在你的项目目录中，打开终端并运行以下命令来安装 `twit` 和 `nodemailer` 库：
     ```bash
     npm install twit nodemailer
     ```

2. 编写代码获取用户的推文并发送邮件：
   - 在你喜欢的文本编辑器中创建一个名为 `twitter-notification.js` 的文件，并添加以下代码：
     ```javascript
     const Twit = require('twit');
     const nodemailer = require('nodemailer');

     // 设置 Twitter API 凭据
     const apiKey = 'YOUR_API_KEY';
     const apiSecretKey = 'YOUR_API_SECRET_KEY';
     const accessToken = 'YOUR_ACCESS_TOKEN';
     const accessTokenSecret = 'YOUR_ACCESS_TOKEN_SECRET';

     // 创建 Twitter 客户端实例
     const client = new Twit({
       consumer_key: apiKey,
       consumer_secret: apiSecretKey,
       access_token: accessToken,
       access_token_secret: accessTokenSecret
     });

     // 设置要获取推文的用户
     const targetUser = 'TARGET_TWITTER_USERNAME';

     // 设置邮件服务凭据
     const emailService = 'YOUR_EMAIL_SERVICE'; // 如 'gmail'
     const emailUser = 'YOUR_EMAIL_ADDRESS';
     const emailPass = 'YOUR_EMAIL_PASSWORD';
     const recipientEmail = 'RECIPIENT_EMAIL_ADDRESS';

     // 创建邮件传输器
     const transporter = nodemailer.createTransport({
       service: emailService,
       auth: {
         user: emailUser,
         pass: emailPass
       }
     });

     // 获取特定用户的最新推文
     client.get('statuses/user_timeline', { screen_name: targetUser, count: 5 }, (err, data, response) => {
       if (err) {
         console.error(err);
       } else {
         const tweets = data;
         tweets.forEach(tweet => {
           const text = tweet.text;

           // 发送邮件通知
           const mailOptions = {
             from: emailUser,
             to: recipientEmail,
             subject: `New Tweet from ${targetUser}`,
             text: text
           };

           transporter.sendMail(mailOptions, (error, info) => {
             if (error) {
               console.error(error);
             } else {
               console.log('Email sent: ' + info.response);
             }
           });
         });
       }
     });
     ```
   - 将 `YOUR_API_KEY`、`YOUR_API_SECRET_KEY`、`YOUR_ACCESS_TOKEN` 和 `YOUR_ACCESS_TOKEN_SECRET` 替换为你的 Twitter API 凭据。
   - 将 `TARGET_TWITTER_USERNAME` 替换为你要获取推文的目标用户的 Twitter 用户名。
   - 将 `YOUR_EMAIL_SERVICE`、`YOUR_EMAIL_ADDRESS`、`YOUR_EMAIL_PASSWORD` 替换为你的电子邮件服务提供商和邮箱凭据。
   - 将 `RECIPIENT_EMAIL_ADDRESS` 替换为接收通知的邮箱地址。
   - 运行代码：
     ```bash
     node twitter-notification.js
     ```
   - 代码将获取目标用户的最新推文，并通过指定的电子邮件服务发送通知。

```golang
    package main

    import (
      "encoding/xml"
      "fmt"
      "io/ioutil"
      "log"
      "net/http"
      "net/url"
      "os"
      "time"
    )

    const (
      APIEndpoint = "https://api.twitter.com/2/tweets/search/recent"
      AuthToken   = "YOUR_TWITTER_AUTH_TOKEN"
      Query       = "YOUR_SEARCH_QUERY"
      MaxResults  = 100
    )

    type Item struct {
      Title       string    `xml:"title"`
      Link        string    `xml:"link"`
      Description string    `xml:"description"`
      PubDate     time.Time `xml:"pubDate"`
    }

    type Channel struct {
      XMLName     xml.Name `xml:"channel"`
      Title       string   `xml:"title"`
      Link        string   `xml:"link"`
      Description string   `xml:"description"`
      Items       []Item   `xml:"item"`
    }

    type RSS struct {
      XMLName xml.Name `xml:"rss"`
      Version string   `xml:"version,attr"`
      Channel Channel  `xml:"channel"`
    }

    type Tweet struct {
      ID        string    `json:"id"`
      Text      string    `json:"text"`
      CreatedAt time.Time `json:"created_at"`
      User      struct {
        Name     string `json:"name"`
        Username string `json:"username"`
      } `json:"user"`
    }

    type TweetsResponse struct {
      Data []Tweet `json:"data"`
    }

    func main() {
      // 设置请求参数
      queryParams := url.Values{}
      queryParams.Set("query", Query)
      queryParams.Set("max_results", fmt.Sprintf("%d", MaxResults))
      queryParams.Set("expansions", "author_id")//如果想获取用户的user.fields必须添加此参数，否则获取不到数据

      // 创建请求
      req, err := http.NewRequest("GET", APIEndpoint, nil)
      if err != nil {
        log.Fatal("创建请求失败：", err)
      }

      // 设置请求头部
      req.Header.Set("Authorization", "Bearer "+AuthToken)
      req.Header.Set("Content-Type", "application/json")
      req.URL.RawQuery = queryParams.Encode()

      // 发送请求
      client := &http.Client{}
      resp, err := client.Do(req)
      if err != nil {
        log.Fatal("发送请求失败：", err)
      }
      defer resp.Body.Close()

      // 读取响应体
      body, err := ioutil.ReadAll(resp.Body)
      if err != nil {
        log.Fatal("读取响应体失败：", err)
      }

      // 解析JSON响应
      var tweetsData TweetsResponse
      err = json.Unmarshal(body, &tweetsData)
      if err != nil {
        log.Fatal("解析JSON失败：", err)
      }

      // 构建RSS对象
      channel := Channel{
        Title:       "Twitter Search Results"
        Link:        "https://twitter.com/search?q=" + url.QueryEscape(Query),
        Description: "Search results for: " + Query,
      }

      for _, tweet := range tweetsData.Data {
        item := Item{
          Title:       tweet.User.Name + " (@" + tweet.User.Username + ")",
          Link:        "https://twitter.com/" + tweet.User.Username + "/status/" + tweet.ID,
          Description: tweet.Text,
          PubDate:     tweet.CreatedAt,
        }
        channel.Items = append(channel.Items, item)
      }

      rss := RSS{
        Version: "2.0",
        Channel: channel,
      }

      // 将结果写入XML文件
      xmlData, err := xml.MarshalIndent(rss, "", "  ")
      if err != nil {
        log.Fatal("生成XML数据失败：", err)
      }

      err = ioutil.WriteFile("tweets.xml", xmlData, 0644)
      if err != nil {
        log.Fatal("写入XML文件失败：", err)
      }

      fmt.Println("结果已写入tweets.xml文件")
    }
```