# VueX Store 간단 예제
// main.js

```javascript
import { createApp } from 'vue';
import App from './App.vue';
import { createStore } from 'vuex';

// store 객체 만들기
const store = createStore({
  state (){
    return {
      count: 0 // 상태 Count 값 0 저장
    }
  },
  mutations: {
    increment (state) {
      state.count++   // 상태를 변경하는 'increment' 변이(mutation)
    }
  }
})

const app = createApp(App);
app.use(store);

// 같은 파일에서 호출
store.commit('increment');  // mutation incrememnt 호출/
console.log(store.state.count); // -> 1

```

```javascript
// 다른 컴포넌트에서 store 사용
methods: {
  increment() {
    this.$store.commit('increment')
    console.log(this.$store.state.count) 
  }
}
```
