
### install
```
$ npm install mongoose --save
```

### Sample - Save
- edit
```
$ nano ./mongoose1.js
```
- code
```
var mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/test', {useNewUrlParser : true, useUnifiedTopology : true});


const userSchema = new mongoose.Schema({
  name: String,
  age: Number
});

const User = mongoose.model('users', userSchema);

const kim = new User({ name: 'Kim Cheolsoo', age: 45 });

console.log( kim );

kim.save();
```
- run
```
$ node ./mongoose1.js
```
- check
  - mongo db 안에 *users* 확인 가능
