
### explain
- google material design을 지원하기 위한 F/W

### install
```
$ npx create-nuxt-app nuxt-vuetify
```
- 중간에 vuetify.js 선택

### edit
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
http://xxxxxx:8080/inspire
```

### explain
- *pages* 디렉토리에 각 페이지가 정의

### Map 그리기
- reference
  - tutorials/vue/vuetify/map.vue
- pages 밑에 넣으면 됨
- callback 함수 역할을 하는 것이 *mounted()*, 페이지가 불리는 순간 수행
- 104 page 내용 수행

### drawer 메뉴 추가
- layouts 밑의 default.vue 수정
- script의 items 항목을 보면 됨
- 추가 수정하면 마커가 안나옴 너무 많이 불리운다고 에러남
- map.vue의 스크립트가 head에 있는 것을 nuxt.config.js로 옮길 수 있음
- head 부분에 script 적고 googlemap 내용 넣으면 됨
