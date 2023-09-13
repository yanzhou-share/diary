# RSS App 调用实例 Nodejs

```javascript
const headers = {
    'Authorization': 'Bearer API:Token', 
    'Content-Type': 'application/json'
};

axios.post('https://api.rss.app/v1/feeds', {"url": url}, { headers })
.then(response => {
    console.log(response.data);
    var items = response.data.items
    // items = {
    //     title: '',
    //     url: '',
    //     description_text: '',
    //     thumbnail: '',
    //     date_published
    // }
    res.send({code:200, data: response.data, rss_feed_url: response.data.rss_feed_url})
})
.catch(error => {
    console.error(error);
});

注意！！！！ 有时候创建了feed，不能直接访问rss的链接，需要用API才能获取到，目前是个bug，不是必现
```