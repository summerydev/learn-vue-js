# Vue.js 시작하기

날짜: 2022년 10월 18일

[Vue.js 시작하기 - Age of Vue.js - 인프런 | 강의](https://www.inflearn.com/course/age-of-vuejs/dashboard)

[https://github.com/joshua1988/learn-vue-js](https://github.com/joshua1988/learn-vue-js)

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