# Vue.js 시작하기

날짜: 2022년 10월 18일
태그: vue

[Vue.js 시작하기 - Age of Vue.js - 인프런 | 강의](https://www.inflearn.com/course/age-of-vuejs/dashboard)

[https://github.com/joshua1988/learn-vue-js](https://github.com/joshua1988/learn-vue-js)

[Cracking Vue.js](https://joshua1988.github.io/vue-camp/)

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