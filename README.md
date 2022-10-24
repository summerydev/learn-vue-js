# Vue.js 시작하기

날짜: 2022년 10월 18일
태그: vue

[Vue.js 시작하기 - Age of Vue.js - 인프런 | 강의](https://www.inflearn.com/course/age-of-vuejs/dashboard)

[https://github.com/joshua1988/learn-vue-js](https://github.com/joshua1988/learn-vue-js)

[Cracking Vue.js](https://joshua1988.github.io/vue-camp/)

- [Vue.js 공식 문서](https://vuejs.org/v2/guide/)
- [Vue.js 스타일 가이드](https://vuejs.org/v2/style-guide/)
- [Vue.js Cookbook](https://vuejs.org/v2/cookbook/)
- [Vuex 공식 문서](https://v3.vuex.vuejs.org/)
- [VueRouter 공식 문서](https://v3.router.vuejs.org/)
- [Vue CLI 공식 문서](https://cli.vuejs.org/)

---

# 목차

---

# VueJS란

- MVVM 패턴의 뷰모델 레이어에 해당하는 View라이브러리

---

# 설치

- chrome
- vs code
- nodejs
- vue.js dev tools

### 플러그인

- Vetur
- Night Owl
- Material Icon Theme
- Live Server
- ESLint
- Prettier
- Auto Close Tag
- Atom Keymap

---

# Start

- 깃 레포지토리 다운로드 https://github.com/joshua1988/learn-vue-js
- 라이브서버 실행 후

`http://127.0.0.1:5500/getting-started/index.html`

![스크린샷 2022-10-18 오후 1.27.09.png](Vue%20js%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20ef4fe25357a542ccb34d6cd53a9c2b31/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-10-18_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_1.27.09.png)

개발자 도구 탭에서 VUE 선택 후 사용 가능

### `web-dev.html` : 기존 DOM조작 방식

- `querySelector` 로 dom에 접근해 view 컨트롤

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app"></div>
    <script>
      const div = document.querySelector("#app");
      div.innerHTML = "hi"; // 화면 hi
      let str = "hello"; // 화면 hi
      div.innerHTML = str; // 화면 hello
      str = "hello world"; // 화면 hello
      div.innerHTML = str; // 화면 hello world
    </script>
  </body>
</html>
```

### Reactivity

`Object.defineProperty()` : 객체 동작 재정의하는 api

```jsx
Object.defineProperty(대상객체, 객체속성, {정의내용})
```

```jsx
<script>
      const div = document.querySelector("#app");
      const viewModel = {};
      //   Object.defineProperty(대상객체, 객체속성, {정의내용})
      Object.defineProperty(viewModel, "str", {
        get: function () {
          console.log("접근");
        },
        set: function (newValue) {
          console.log(newValue + " 할당");
          div.innerHTML = newValue;
        },
      });
    </script>
```

- 브라우저 개발자도구에서 `viewModel.str` 로 접근 가능
- 콘솔에 접근 및 할당 로그
- 값이 할당될 때마다 div에 값 업데이트 ⇒ 데이터 바인딩

### 라이브러리화

```jsx
<script>
      var div = document.querySelector("#app");
      var viewModel = {};

      (function () {
        // 즉시 실행 함수
        function init() {
          //   Object.defineProperty(대상객체, 객체속성, {정의내용})
          Object.defineProperty(viewModel, "str", {
            get: function () {
              console.log("접근");
            },
            set: function (newValue) {
              console.log(newValue + " 할당");
              render(newValue);
            },
          });
        }

        function render(value) {
          div.innerHTML = value;
        }

        init();
      })();
    </script>
```

# Vue 인스턴스

## 인스턴스 생성

```jsx
new Vue();
```

- 인스턴스 속성 크롬 개발자 도구에서 확인 가능
    
    ```jsx
    <script>
      var vm = new Vue();
    	console.log(vm);
    </script>
    ```
    
    ![스크린샷 2022-10-19 오전 9.18.55.png](Vue%20js%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20ef4fe25357a542ccb34d6cd53a9c2b31/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-10-19_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_9.18.55.png)
    

- 화면에 표시하기 위해서 `el` 속성 필수 입력
    
    ```jsx
    		<script>
          var vm = new Vue({
            el: "#app",
            data: {
                message: "hello"
            }
          });
        </script>
    ```
    

---

# 컴포넌트

- 재사용성, 화면 영역 구분 개발
- 인스턴스 생성 → root 컴포넌트

## 전역 컴포넌트

- 등록 : `Vue.component("컴포넌트 이름", 컴포넌트 내용)`

```jsx
		<div id="app">
      <app-header></app-header>
      <app-content></app-content>
		</div>

		<script>
      // Vue.component("컴포넌트 이름", 컴포넌트 내용)
      Vue.component("app-header", {
        template: "<h1>This is Vue.component app-header</h1>",
      });

      Vue.component("app-content", {
        template: "<div>this is Vue.component app-content</div>",
      });

      new Vue({
        el: "#app",
      });
		</script>
```

## 지역 컴포넌트

- 인스턴스마다 등록 필요
- 등록 : 인스턴스 객체 리터럴 안에 `components : { "컴포넌트 이름" : 컴포넌트 내용 }`

```jsx
    <div id="app">
      <app-footer></app-footer>
    </div>

    <script>
      new Vue({
        el: "#app",
        components: {
          "app-footer": {
            template: "<footer>this is app-footer</footer>"
          },
        },
      });
    </script>
```

## 컴포넌트 통신

- 상위컴포넌트 → 프롭스 ↔ 이벤트 ← 하위컴포넌트
- 프롭스 작성 : `<app-header v-bind:프롭스 속성 이름 = "상위 컴포넌트 데이터 이름"></app-header>`

```jsx
	<body>
    <div id="app">
      <app-header v-bind:propsdata="message"></app-header>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      var appHeader = {
        template: "<h1>{{ propsdata }}</h1>",
        props: ["propsdata"],
      };

      new Vue({
        el: "#app",
        components: {
          "app-header": appHeader,
        },
        data: {
          message: "hi",
        },
      });
    </script>
  </body>
```

- props 예시

```jsx
	<body>
    <div id="app">
      <app-header v-bind:propsdata="message"></app-header>
      <app-content v-bind:propsdata="num"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
			var appHeader = {
        template: "<h1>{{ propsdata }}</h1>",
        props: ["propsdata"],
      };

      var appContent = {
        template: "<div>app-content {{ propsdata }}</div>",
        props: ["propsdata"]
      };

      new Vue({
        el: "#app",
        components: {
          "app-header": appHeader,
          "app-content": appContent,
        },
        data: {
          message: "hi",
          num : 10
        },
      });
    </script>
  </body>
```

<aside>
❗ ! component → components

! method → methods

</aside>

## event emit

- `this.$emit()` : 이벤트 발생시키는 api, 이 속성을 통해 상위 컴포넌트로 통신 가능
- `<button v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트 메서드 이름">`

```jsx
	<body>
    <div id="app">
      <app-header></app-header>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      var appHeader = {
        template: '<button v-on:click="passEvent">click me</button>',
        methods: {
          passEvent: function () {
            this.$emit('pass');
          },
        },
      };

      new Vue({
        el: "#app",
        components: {
          "app-header": appHeader,
        },
      });
    </script>
  </body>
```

- event emit으로 상위 컴포넌트의 num을 하위 컴포넌트 버튼 클릭으로 num+1 조작하기

```jsx
   <body>
    <div id="app">
      <app-header v-on:pass="logText"></app-header>
      <app-content v-on:add="addNum" v-bind:propsdata="num"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      var appHeader = {
        template: '<button v-on:click="passEvent">click me</button>',
        methods: {
          passEvent: function () {
            this.$emit("pass");
          },
        },
      };

      var appContent = {
        template:
          '<div><button v-on:click="addEvent">add</button><div>{{ propsdata }}</div></div>',
        methods: {
          addEvent: function () {
            this.$emit("add");
          },
        },
        props: ["propsdata"],
      };

      new Vue({
        el: "#app",
        components: {
          "app-header": appHeader,
          "app-content": appContent,
        },
        methods: {
          logText: function () {
            console.log("hi");
          },
          addNum: function () {
            this.num += 1;
            console.log(this.num);
          },
        },
        data: {
          num: 1,
        },
      });
    </script>
  </body>
```

## 같은 컴포넌트 레벨 간의 통신

- 올릴 땐 event, 내릴 땐 props

```jsx
	<body>
    <div id="app">
      <app-header v-bind:propsdata="num"></app-header>
      <app-content v-on:pass="deliverNum"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      var appHeader = {
        template: "<div>Header {{propsdata}}</div>",
        props: ["propsdata"],
      };

      var appContent = {
        template:
          '<div>Content<button v-on:click="passNum">pass</button></div>',
        methods: {
          passNum: function () {
            this.$emit("pass", 10);
          },
        },
      };

      new Vue({
        el: "#app",
        components: {
          "app-header": appHeader,
          "app-content": appContent,
        },
        data: {
          num: 0,
        },
        methods: {
          deliverNum: function (value) {
            this.num = value;
          },
        },
      });
    </script>
  </body>
```

# 라우터

- 라우터 선언

```jsx
var router = new VueRouter({
  routes: [
  ]
})
```

```jsx
<body>
  <div id="app">
    <div>
      <router-link to="/login">Login</router-link>
      <router-link to="/main">Main</router-link>
    </div>
    <router-view></router-view>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
  <script>
    var LoginComponent = {
      template: '<div>login</div>'
    }
    var MainComponent = {
      template: '<div>main</div>'
    }

    var router = new VueRouter({
      // 페이지의 라우팅 정보      
      routes: [
        // 로그인 페이지 정보
        {
          // 페이지의 url
          path: '/login',
          // name: 'login',
          // 해당 url에서 표시될 컴포넌트
          component: LoginComponent
        },
        // 메인 페이지 정보
        {
          path: '/main',
          component: MainComponent
        }
      ]
    });

    new Vue({
      el: '#app',
      router: router,
    });
  </script>
</body>
```

# Vue cli

- vue-cli 는 기본 vue 개발 환경을 설정해주는 도구

```bash
# check version
node -v
npm -v

# vue cli download
npm install @vue/cli

# vue vli version check
vue --version
vue --V

# create vue project
vue create [project_name]

# run server
npm run serve

# build
npm run build
```

# `filename.vue` 구성

```jsx
<template>
  <!-- html -->
</template>

<script>
export default {
  // javascript
};
</script>

<style>
/* css */
</style>
```

# v-model

[v-model의 동작 원리와 활용 방법](https://joshua1988.github.io/web-development/vuejs/v-model-usage/)

## v-model 사용법

```jsx
<input v-model="inputText">
```

```jsx
new Vue({
  data: {
    inputText: ''
  }
})
```

사용자 입력을 받는 UI요소에 `v-model` 속성을 사용하면 입력 값이 자동으로 뷰 데이터 속성에 연결된다.

리액트의 경우 UI요소에 onChange 이벤트를 걸어 state를 업데이트 하는 방식을 사용했는데, `v-model` 로 데이터 속성에 바로 접근하는 방식이 편리한 것 같다.

```jsx
<template>
  <form v-on:submit.prevent="submitForm">
    <div>
      <label for="username">id: </label>
      <input id="username" type="text" v-model="username" />
    </div>
    <div>
      <label for="password">password: </label>
      <input id="password" type="password" v-model="password" />
    </div>
    <button type="submit">login</button>
  </form>
</template>

<script>
export default {
  data: function () {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    submitForm: function () {
      console.log(this.username, this.password);
    },
  },
};
</script>

<style>
</style>
```

스크립트에 data와 input태그의 `v-model` 속성을 연결시키면 이런식으로 브라우저의 data속성에서 확인할 수 있다.

![스크린샷 2022-10-24 오전 10.25.10.png](Vue%20js%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20ef4fe25357a542ccb34d6cd53a9c2b31/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2022-10-24_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_10.25.10.png)

`v-model` 은 `v-bind`와 `v-on`의 기능의 조합으로 동작한다.

- `v-bind` : 뷰 인스턴스의 데이터 속성을 해당 HTML 요소에 연결할 때 사용
- `v-on` : 해당 HTML 요소의 이벤트를 뷰 인스턴스의 로직과 연결할 때 사용

기존 리액트에서 렌더링을 막는 `e.preventDefault()`또한 사용하지 않고, `form`태그에서 `v-on:submit` 뒤에 `.prevent`를 붙여 간단하게 동일한 동작을 구현할 수 있다.

v-model 동작 시 한국어 입력은 한 글자씩 늦게 반응하는 단점이 존재한다. 직접 이벤트와 값을 조합해 바인딩하는 대신, 인풋 컴포넌트를 별도의 컴포넌트로 분리해 `v-model`로 처리할 수 있다.

```jsx
<!-- BaseInput.vue - 싱글 파일 컴포넌트 구조-->
<template>
  <input v-bind:value="value" v-on:input="updateInput">
</template>

<script>
export default {
  props: ['value'],
  methods: {
    updateInput: function(event) {
      this.$emit('input', event.target.value);
    }
  }
}
</script>
```

```jsx
<!-- App.vue - 싱글 파일 컴포넌트 구조 -->
<template>
  <div>
    <base-input v-model="inputText"></base-input>
  </div>
</template>

<script>
import BaseInput from './BaseInput.vue';

export default {
  components: {
    'base-input': BaseInput
  },
  data: function() {
    return {
      inputText: ''
    }
  }
}
</script>
```

## 사용자 입력 폼 완성하기

- `form`태그에 `v-on` 속성을 달아 `submitForm` 동작과 연결
- `input`태그에 `v-model` 속성을 달아 data에 연결
- `submitForm` 메서드에서 `input`태그의 data를 받아 axios로 서버에 내용 전송

```jsx
<template>
  <form v-on:submit.prevent="submitForm">
    <div>
      <label for="username">id: </label>
      <input id="username" type="text" v-model="username" />
    </div>
    <div>
      <label for="password">password: </label>
      <input id="password" type="password" v-model="password" />
    </div>
    <button type="submit">login</button>
  </form>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    submitForm: function () {
      console.log(this.username, this.password);
      const url = "https://jsonplaceholder.typicode.com/users";
      const data = {
        username: this.username,
        password: this.password,
      };
      
      axios
        .post(url, data)
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
</style>
```

---