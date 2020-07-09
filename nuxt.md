
### install
```
$ npx create-nuxt-app nuxt
```
- Javascript 선택, 그 외에는 그냥 엔터s

### config
- localhost 주소로만 접속가능한 것을 변경
```
$ nano ./nuxt.config.js
```
```
export default {
  server: {
    port: 8080,      // default: 3000
    host: '0.0.0.0', // default: localhost,
    timing: false
  },
...
```

### run
```
$ npm run dev
```

### check
```
http://xxxxxx:8080
```
