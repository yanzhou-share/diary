# https://rapidapi.com/ 

```javascript
const axios = require('axios');

const options = {
  method: 'GET',
  url: 'https://newslit-news-search.p.rapidapi.com/news',
  params: {q: '<REQUIRED>'},
  headers: {
    'X-RapidAPI-Key': '201a56764amsh249c63afb344efdp1005c6ajsne2a3a8806950',
    'X-RapidAPI-Host': 'newslit-news-search.p.rapidapi.com'
  }
};

try {
	const response = await axios.request(options);
	console.log(response.data);
} catch (error) {
	console.error(error);
}
```

# 需要subscribe 收费

# 提取页面数据

```javascript
const axios = require('axios');

const options = {
  method: 'POST',
  url: 'https://news-article-data-extract-and-summarization1.p.rapidapi.com/extract/',
  headers: {
    'content-type': 'application/json',
    'X-RapidAPI-Key': '201a56764amsh249c63afb344efdp1005c6ajsne2a3a8806950',
    'X-RapidAPI-Host': 'news-article-data-extract-and-summarization1.p.rapidapi.com'
  },
  data: {
    url: 'https://techcrunch.com/2022/04/18/web-scraping-legal-court/'
  }
};

try {
	const response = await axios.request(options);
	console.log(response.data);
} catch (error) {
	console.error(error);
}
```