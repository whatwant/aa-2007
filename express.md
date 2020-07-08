
### install
- 실제 파일들은 *./node_modules* 디렉토리 안에 저장
```
$ mkdir express
$ cd express
$ npm install express --save
```

### Sample
```
$ nano ./express.js
$ node ./express.js
```
- 파일 내용
```
var express = require('express')

var app = express()

app.get('/', function(req, res) {
  res.send('Hello World')
})

app.get('/about', (req, res) => {
  res.send('No Hello')
})

var port = 8080

app.listen(port, function() {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
- check
```
http://localhost:8080
http://localhost:8080/about
```


### Sample - GET
- edit
```
$ nano ./db5.js
$ node ./db5.js
```
- code
```
const express = require('express')
const app = express()

app.get('/search', function(request, response) {
  const keyword = request.query.keyword
  console.log(keyword)

  if (keyword == undefined){
    response.sendFile(__dirname + '/search.html')
  }
  else {
    collection.find({ $text: { $search: keyword }}).limit(5).toArray (function(err, docs){
      response.json(docs)
    })
  }
})

var port = 8080

app.listen(port, function() {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
- run
```
http://localhost:8080/search
```
