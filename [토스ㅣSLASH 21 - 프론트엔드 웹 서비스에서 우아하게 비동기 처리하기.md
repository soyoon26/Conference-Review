[토스ㅣSLASH 21 - 프론트엔드 웹 서비스에서 우아하게 비동기 처리하기](https://www.youtube.com/watch?v=FvRtoViujGg&si=qLa0UbynqrkbrYwE)

#### 웹 서비스에서 가장 다루기 어려운 부분은?

비동기 프로그래밍 : 순서가 보장되지 않는 경우
(서버의 응답만 기다리고 다른 유저 인터랙션에 반응하지 않는다면 멈춰있게 됨)
-> 다른 일을 미리 처리하며 서버 응답이 돌아오면 다시 이어서 일을 하는 것이 비동기 프로그래밍

#### JS에서는 Callback, Promise, Observable를 이용해 비동기 프로그래밍을 다루고 있음

좋은 코드란?
![](https://velog.velcdn.com/images/for24ng/post/8c9322da-21e9-44ca-b4b8-6ca892bea0de/image.png)
: 코드가 너무 복잡하고 각 프로퍼티에 접근하는 핵심 기능이 코드로 잘 드러나지 않음 => 안전하게 접근하고자 하는게 드러나지 않음

![](https://velog.velcdn.com/images/for24ng/post/ef976aeb-10cc-4a20-a293-eba1de7a3429/image.png)
: 해결한 코드

비동기호출이 많아지면 불편해진다.
React의 비동기 처리는 어렵다.

- 성공하는 경우에만 집중해 컴포넌트를 구성하기 어렵다.
- 2개 이상의 비동기 로직이 개입할 때, 비지니스 로직을 파악하기 점점 어려워진다.
  State를 사용하는 방법으로는 이렇게 간단하게 비동기 처리 할 수 없음

![](https://velog.velcdn.com/images/for24ng/post/ee087ac1-47db-4445-a6cb-0cec58740a9e/image.png)
Promise가 없던 시절 비동기를 처리하기 위해 callback을 사용한 코드
fetchUserEntity를 호출해 결과를 Callback으로 받는데 에러가 있으면 에러를 emit함.

결국, 복잡하기도 하지만 '성공하는 경우'와 '실패하는 경우'가 섞여서 처리되어 코드를 작성하는 입장에서 매번 에러 유무를 확인해야 함

![](https://velog.velcdn.com/images/for24ng/post/44d28f2b-a6fe-4d8f-b584-b458b72d27b7/image.png)
좋은 코드인 이유 : '성공하는 경우'만 다루고 '실패하는 경우'는 catch절에서 분리해 처리함. '실패하는 경우'에 대한 처리를 외부에 위임할 수 있음

### 좋은 코드의 특징

1. 성공, 실패의 경우를 분리해서 처리할 수 있음
2. 비지니스 로직을 한눈에 파악할 수 있음

![](https://velog.velcdn.com/images/for24ng/post/05bc015f-ceab-40ab-a7e1-eaf9d581edc6/image.png)
React의 비동기 처리는 어렵다. 해결하는 도구는 ?

### React Suspense for Data Fetching

데이처를 가져오기 위한 Suspense
목표는 성공한 경우에만 집중, 로딩 상태와 에러 상태가 분리, 동기와 거의 같게 사용할 수 있는 !

![](https://velog.velcdn.com/images/for24ng/post/7e7b08cd-3031-4a64-9191-4dc0af1e50b3/image.png)

🧂 : 나도 이런 걸 만들어보고 싶다. 토스팀에서 활용한 예시를 보니 더 부러워졌다. 갈수록 편리한 걸 잘 만들어내는 걸 보니 나도 잘 하고 싶다는 생각이 강하게 든다.
